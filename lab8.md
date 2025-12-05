# CI/CD Pipeline Lab: GitHub Actions & GitLab CI/CD with GitHub Copilot


---


**Learning Objectives:**
- Create and configure GitHub Actions workflows
- Build GitLab CI/CD pipelines
- Leverage GitHub Copilot for rapid pipeline development
- Implement testing, security, and deployment stages
- Troubleshoot common CI/CD issues

---

## Lab Setup

### Step 1: Verify GitHub Copilot Installation

1. Open VS Code
2. Check for Copilot icon in the status bar
3. Test Copilot by opening Command Palette (`Ctrl+Shift+P`)
4. Type "GitHub Copilot: Open Chat"

### Step 2: Clone/Initialize Repository

```bash
# If starting fresh
cd c:\Users\AkshayKS\source\repos\node2
git init

# If cloning existing repo
git clone <your-repo-url>
cd <repo-name>
```

### Step 3: Verify Node.js Project

Ensure you have a `package.json` file. If not, create one:

```bash
npm init -y
```

Add basic scripts to `package.json`:

```json
{
  "scripts": {
    "test": "echo \"Running tests...\" && exit 0",
    "lint": "echo \"Running linter...\" && exit 0",
    "build": "echo \"Building application...\" && exit 0",
    "start": "node index.js"
  }
}
```

---

## Part 1: GitHub Actions Workflow

### 1.1 Create Workflow Directory Structure

```bash
mkdir -p .github/workflows
```

### 1.2 Basic CI Workflow with Copilot

**Step-by-Step Instructions:**

1. Create file `.github/workflows/ci.yml`
2. Open the file in VS Code
3. Type the following comment and let Copilot autocomplete:

```yaml
# GitHub Actions CI workflow for Node.js application with install, test, and build stages
```

4. Press `Tab` to accept Copilot suggestions
5. Review and modify the generated workflow

**Expected Output (using Copilot):**

```yaml
name: CI Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [18.x, 20.x]
    
    steps:
    - name: Checkout repository
      uses: actions/checkout@v4
    
    - name: Setup Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v4
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run linter
      run: npm run lint
    
    - name: Run tests
      run: npm test
    
    - name: Build application
      run: npm run build
```

### 1.3 Add Test Coverage Reporting

Ask GitHub Copilot Chat:
```
Add code coverage reporting with Istanbul/nyc to the GitHub Actions workflow
```

Copilot should suggest adding:

```yaml
    - name: Generate coverage report
      run: npm run test:coverage
    
    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v3
      with:
        files: ./coverage/coverage-final.json
        flags: unittests
        name: codecov-umbrella
        fail_ci_if_error: true
```

### 1.4 Add Security Scanning

Type this comment in your workflow file:
```yaml
# Add npm audit security scanning job
```

Let Copilot generate:

```yaml
  security:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Run security audit
      run: npm audit --audit-level=moderate
```

### 1.5 Add Docker Build Stage

Ask Copilot Chat:
```
Add a Docker build and push stage to this GitHub Actions workflow
```

Expected addition:

```yaml
  docker:
    needs: build
    runs-on: ubuntu-latest
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v3
    
    - name: Login to Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}
    
    - name: Build and push
      uses: docker/build-push-action@v5
      with:
        context: .
        push: true
        tags: ${{ secrets.DOCKER_USERNAME }}/node-app:latest
```

### 1.6 Add Deployment Stage

```yaml
  deploy:
    needs: [build, security, docker]
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    environment:
      name: production
      url: https://your-app.com
    
    steps:
    - name: Deploy to production
      run: |
        echo "Deploying to production server"
        # Add deployment commands here
```

---

## Part 2: GitLab CI/CD Pipeline

### 2.1 Create GitLab CI Configuration

Create `.gitlab-ci.yml` in your project root.

### 2.2 Basic Pipeline with Copilot

Type this comment:
```yaml
# GitLab CI/CD pipeline for Node.js with stages: install, test, build, deploy
```

Let Copilot generate the base structure:

```yaml
image: node:20

stages:
  - install
  - test
  - build
  - deploy

variables:
  npm_config_cache: "$CI_PROJECT_DIR/.npm"

cache:
  key: ${CI_COMMIT_REF_SLUG}
  paths:
    - .npm/
    - node_modules/

install_dependencies:
  stage: install
  script:
    - npm ci
  artifacts:
    paths:
      - node_modules/
    expire_in: 1 hour
```

### 2.3 Add Test Jobs

```yaml
lint:
  stage: test
  dependencies:
    - install_dependencies
  script:
    - npm run lint
  allow_failure: false

unit_tests:
  stage: test
  dependencies:
    - install_dependencies
  script:
    - npm test
  coverage: '/All files[^|]*\|[^|]*\s+([\d\.]+)/'
  artifacts:
    reports:
      junit: junit.xml
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml

integration_tests:
  stage: test
  dependencies:
    - install_dependencies
  script:
    - npm run test:integration
  allow_failure: true
```

### 2.4 Add Security and Quality Checks

Ask Copilot:
```
Add security scanning and code quality checks to GitLab CI pipeline
```

Expected output:

```yaml
security_scan:
  stage: test
  dependencies:
    - install_dependencies
  script:
    - npm audit --audit-level=high
    - npm run security:check
  allow_failure: true

code_quality:
  stage: test
  image: docker:stable
  services:
    - docker:stable-dind
  script:
    - docker run --rm -v "$PWD":/code codeclimate/codeclimate analyze -f json > codeclimate.json
  artifacts:
    reports:
      codequality: codeclimate.json
```

### 2.5 Add Build Stage

```yaml
build_application:
  stage: build
  dependencies:
    - install_dependencies
  script:
    - npm run build
    - echo "Build completed successfully"
  artifacts:
    paths:
      - dist/
      - build/
    expire_in: 1 week
  only:
    - main
    - develop
```

### 2.6 Add Deployment Stages

```yaml
deploy_staging:
  stage: deploy
  dependencies:
    - build_application
  script:
    - echo "Deploying to staging environment"
    - npm run deploy:staging
  environment:
    name: staging
    url: https://staging.example.com
    on_stop: stop_staging
  only:
    - develop

deploy_production:
  stage: deploy
  dependencies:
    - build_application
  script:
    - echo "Deploying to production environment"
    - npm run deploy:production
  environment:
    name: production
    url: https://example.com
  only:
    - main
  when: manual

stop_staging:
  stage: deploy
  script:
    - echo "Stopping staging environment"
  environment:
    name: staging
    action: stop
  when: manual
  only:
    - develop
```

---

## Part 3: Advanced Copilot Usage

### 3.1 Using Copilot Chat for Complex Scenarios

#### Example 1: Multi-Platform Matrix Builds

Open Copilot Chat and ask:
```
Create a matrix build strategy for GitHub Actions that tests Node.js 18, 20, and 22 on Ubuntu, Windows, and macOS
```

#### Example 2: Conditional Pipeline Execution

Ask Copilot:
```
Add conditional logic to skip deployment if commit message contains [skip-deploy]
```

Expected for GitHub Actions:
```yaml
jobs:
  deploy:
    if: "!contains(github.event.head_commit.message, '[skip-deploy]')"
```

Expected for GitLab:
```yaml
deploy_production:
  rules:
    - if: '$CI_COMMIT_MESSAGE =~ /\[skip-deploy\]/'
      when: never
    - if: '$CI_COMMIT_BRANCH == "main"'
      when: manual
```

#### Example 3: Parallel Job Execution

Ask Copilot:
```
Split tests into parallel jobs to run unit, integration, and e2e tests concurrently
```

### 3.2 Optimizing Pipelines with Copilot

#### Cache Optimization

Ask Copilot:
```
Optimize caching strategy for faster pipeline execution in both GitHub Actions and GitLab CI
```

#### Dependency Caching (GitHub Actions):
```yaml
- name: Cache node modules
  uses: actions/cache@v3
  with:
    path: ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-node-
```

#### Artifact Optimization:
```yaml
artifacts:
  paths:
    - dist/
  expire_in: 30 days
  when: on_success
```

### 3.3 Adding Notifications

Ask Copilot:
```
Add Slack notifications for pipeline success and failure
```

**GitHub Actions:**
```yaml
- name: Slack Notification
  uses: 8398a7/action-slack@v3
  with:
    status: ${{ job.status }}
    text: 'Pipeline ${{ job.status }}'
    webhook_url: ${{ secrets.SLACK_WEBHOOK }}
  if: always()
```

**GitLab CI:**
```yaml
notify_slack:
  stage: .post
  script:
    - 'curl -X POST -H "Content-type: application/json" --data "{\"text\":\"Pipeline $CI_PIPELINE_STATUS\"}" $SLACK_WEBHOOK_URL'
  when: always()
```

---



**End of Lab Instructions**
