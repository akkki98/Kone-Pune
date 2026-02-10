# Lab Instructions: Unit Testing for Web Developers using GitHub Copilot

## Lab Overview

This hands-on lab is designed for **Web Developers** (Frontend & Backend) to learn how to design, write, refactor, and automate **unit tests** using **GitHub Copilot**. The lab focuses on testing business logic, APIs, UI components, mocking browser and backend dependencies, and improving test coverage using Copilot.

All coding and testing activities must be performed using **GitHub Copilot Ask, Edit, and Agent modes**.

---

## Learning Objectives

By the end of this lab, participants will be able to:

* Understand unit testing fundamentals for web applications
* Write unit tests for backend APIs and frontend components
* Mock APIs, services, and browser features
* Use GitHub Copilot to generate and refactor tests
* Improve code quality and test coverage
* Automate tests using CI pipelines

---

## Target Audience

* Web Developers
* Frontend Engineers (React / Angular / Vue)
* Backend Engineers (Node.js / Java / .NET / Python)
* Full‑Stack Developers

---

## Prerequisites

* Basic understanding of web development
* Familiarity with Git and GitHub
* GitHub Copilot enabled
* Node.js 18+ installed

---

## Lab Environment Setup

### Step 1: Clone Sample Repository

```bash
git clone https://github.com/<org>/web-unit-testing-lab.git
cd web-unit-testing-lab
npm install
```

### Step 2: Project Structure

```
web-unit-testing-lab/
├── backend/
│   ├── controllers/
│   ├── services/
│   └── routes/
├── frontend/
│   ├── components/
│   ├── pages/
│   └── hooks/
├── tests/
│   ├── backend/
│   └── frontend/
├── jest.config.js
└── README.md
```

---

## Lab 1: Understanding Testability in Web Applications

### Objective

Identify code that is difficult to unit test.

#### Copilot Prompt

```text
@workspace /explain Which parts of this web application are hard to unit test and why?
```

---

## Lab 2: Refactoring Web Code for Testability

### Objective

Improve testability through better separation of concerns.

#### Copilot Prompt

```text
#selection Refactor this code to improve testability using dependency injection and pure functions.
```

---

## Lab 3: Backend Unit Testing (API & Services)

### Objective

Write unit tests for backend logic.

#### Task

Select a service method (e.g., `createUser`).

#### Copilot Prompt

```text
Write unit tests for this backend function covering success, validation errors, and failure scenarios.
```

---

## Lab 4: Mocking Backend Dependencies

### Objective

Mock databases and external services.

#### Copilot Prompt

```text
Mock database and external API calls so these unit tests run without real dependencies.
```

---

## Lab 5: Frontend Unit Testing (UI Components)

### Objective

Test UI components in isolation.

#### Task

Select a React component.

#### Copilot Prompt

```text
Generate unit tests for this React component using React Testing Library, including user interaction tests.
```

---

## Lab 6: Mocking Browser & API Calls

### Objective

Mock browser APIs and backend calls.

#### Copilot Prompt

```text
Mock fetch, localStorage, and browser APIs for this component's unit tests.
```

---

## Lab 7: Edge Case & Negative Testing

### Objective

Validate robustness.

#### Copilot Prompt

```text
Add unit tests for edge cases, invalid inputs, and error states.
```

---

## Lab 8: Improving Test Coverage

### Objective

Identify missing tests.

#### Copilot Prompt

```text
@workspace What additional unit tests are required to improve coverage for this web module?
```

---

## Lab 9: Refactoring Unit Tests

### Objective

Improve test readability and maintainability.

#### Copilot Prompt

```text
Refactor these unit tests to reduce duplication and improve clarity.
```

---

## Lab 10: Running Unit Tests in CI

### Objective

Automate tests.

#### Copilot Prompt

```text
Create a GitHub Actions workflow to run frontend and backend unit tests on pull requests.
```

---

## Lab 11: Copilot Agent Mode (Advanced)

### Objective

End-to-end test improvement using Copilot Agent.

#### Copilot Prompt

```text
@workspace /agent Add missing unit tests, improve coverage to 85%, refactor flaky tests, and ensure all tests pass.
```

---

## Best Practices for Web Unit Testing

* Test business logic separately from UI
* Mock network and browser APIs
* Avoid testing implementation details
* Keep tests fast and isolated
* Use coverage reports as guidance, not goals

---

## Evaluation Criteria

* Quality of unit tests
* Coverage improvement
* Code refactoring quality
* CI pipeline success
* Effective usage of GitHub Copilot

---

## Bonus Challenges

* Add contract tests between frontend and backend
* Introduce TDD using GitHub Copilot
* Add coverage thresholds in CI

---

## Lab Completion

Participants should submit:

* Backend and frontend unit tests
* Coverage report
* CI pipeline screenshot

---

**End of Lab**
