# DevOps Capstone Project – GitHub Copilot Driven IaC & CI/CD

## Capstone Title

**End-to-End Cloud Infrastructure & CI/CD Automation using GitHub Copilot**

---

## Target Audience

* DevOps Engineers
* Platform Engineers
* Cloud Engineers
* SREs

---

## Capstone Duration
4 Hours

---

## Problem Statement

Your organization is launching a **cloud-native application platform** that must be deployed, secured, and operated using **Infrastructure as Code (IaC)** and **automated CI/CD pipelines**.

The current environment suffers from:

* Manual infrastructure provisioning
* Inconsistent environments (Dev/Test/Prod)
* Lack of pipeline standards and security controls
* Poor visibility into deployments and failures

Your mission is to design and implement a **production-grade DevOps platform** using:

* IaC for infrastructure provisioning
* CI/CD pipelines for build, test, and deploy
* GitHub Copilot as the primary assistant for authoring, reviewing, and improving code

All infrastructure, pipelines, policies, and documentation must be created **with the help of GitHub Copilot**.

---

## Ultimate Requirement

> ⚠️ All IaC code, pipeline YAML, scripts, policies, and documentation must be authored using **GitHub Copilot (Chat, Edit, Agent, PR features)**.

---

## Technology Stack (Choose One Cloud)

* **Cloud Provider**: Azure / AWS / GCP
* **IaC**: Terraform / Bicep / ARM
* **CI/CD**: GitHub Actions or Azure DevOps Pipelines
* **Containerization**: Docker
* **Security**: Secrets via Key Vault / Secrets Manager
* **Monitoring**: Cloud-native monitoring

---

## High-Level Architecture

* Git Repository (IaC + App + Pipelines)
* CI Pipeline (Build, Test, Scan)
* CD Pipeline (Deploy to Dev → Stage → Prod)
* Cloud Infrastructure (Network, Compute, DB)
* Secrets Manager
* Monitoring & Alerts

Key Principles:

* Everything as Code
* Idempotent deployments
* Secure-by-default
* Reusable modules

---

# CAPSTONE TASKS & CHALLENGES

---

## Task 1: Repository & Copilot Instructions Setup

### Goal

Establish standards and guardrails for Copilot-generated DevOps code.

### Tasks

* Create `.github/copilot-instructions.md`
* Define rules for:

  * IaC standards (naming, modules)
  * Pipeline YAML best practices
  * Secrets handling (no hardcoded values)
  * Environment separation

### Copilot Prompt

```text
What DevOps and IaC standards should I enforce using copilot-instructions for this repository?
```

### Success Criteria

* Instructions file exists
* Copilot follows standards automatically

---

## Task 2: Infrastructure as Code (IaC) – Core Platform

### Goal

Provision foundational cloud infrastructure using IaC.

### Tasks

Use Copilot to:

* Create reusable IaC modules for:

  * Virtual Network / VPC
  * Compute (VMs / App Service / ECS / AKS)
  * Database (SQL)
  * Storage
* Support multiple environments (Dev/Test/Prod)

### Copilot Prompts

```text
Create a reusable Terraform module for a virtual network with environment-based naming
```

```text
Refactor this IaC code to improve modularity and reusability
```

### Success Criteria

* Infrastructure deploys successfully
* No duplicated code
* Environment-specific variables supported

---

## Task 3: Secure Secrets Management

### Goal

Eliminate secrets from code and pipelines.

### Tasks

Use Copilot to:

* Integrate Key Vault / Secrets Manager
* Reference secrets securely in pipelines

### Copilot Prompts

```text
Modify this pipeline to retrieve secrets from a cloud key vault instead of environment files
```

### Success Criteria

* No secrets in repo
* Pipelines retrieve secrets securely

---

## Task 4: CI Pipeline – Build & Quality Gates

### Goal

Create a robust CI pipeline using GitHub Actions or Azure DevOps.

### Tasks

Use Copilot to:

* Build application
* Run unit tests
* Run security scans (SAST)
* Publish artifacts

### Copilot Prompts

```text
Create a GitHub Actions workflow to build, test, and publish artifacts
```

```text
Add quality gates to fail the pipeline on test or scan failures
```

### Success Criteria

* Pipeline runs on PRs
* Failures block merges

---

## Task 5: CD Pipeline – Automated Deployments

### Goal

Implement progressive delivery using CD pipelines.

### Tasks

Use Copilot to:

* Deploy to Dev → Stage → Prod
* Add manual approval for Prod
* Support rollback

### Copilot Prompts

```text
Create a multi-stage deployment pipeline with approvals for production
```

### Success Criteria

* Controlled promotion between environments
* Rollback supported

---

## Task 6: Containerization & Image Management

### Goal

Standardize application packaging.

### Tasks

Use Copilot to:

* Create production-ready Dockerfiles
* Push images to container registry

### Copilot Prompts

```text
Create a secure multi-stage Dockerfile for this application following best practices
```

---

## Task 7: Monitoring, Logging & Alerts

### Goal

Ensure operational visibility.

### Tasks

Use Copilot to:

* Enable metrics and logs
* Configure alerts for failures

### Copilot Prompts

```text
Enable monitoring and alerting for this infrastructure using IaC
```

---

## Task 8: Copilot Agent Mode – Platform Review

### Goal

Use Copilot Agent for cross-repo analysis.

### Tasks

Ask Copilot Agent to:

* Review IaC and pipelines
* Identify security and reliability gaps

### Copilot Prompt

```text
Act as a DevOps architect and review this repository for security, scalability, and reliability issues
```

---

## Task 9: Pull Request Automation with Copilot

### Goal

Professional DevOps PR workflows.

### Tasks

* Create PRs for IaC and pipelines
* Use Copilot to generate:

  * PR summaries
  * Risk analysis
  * Deployment impact

### Copilot Prompts

```text
Generate a PR summary explaining infrastructure changes, risks, and rollback strategy
```

```text
Perform a DevOps-focused code review for this PR
```




## Deliverables

* IaC codebase
* CI/CD pipeline YAML
* Copilot Instructions file
* Pull Requests with Copilot summaries & reviews

---

## Key Takeaways

* GitHub Copilot accelerates DevOps workflows end-to-end
* Strong prompts lead to reliable IaC and pipelines
* Copilot enhances not just coding, but reviews, security, and operations

---

**End of DevOps Capstone Project – GitHub Copilot**
