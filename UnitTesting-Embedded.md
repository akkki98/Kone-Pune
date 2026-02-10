# Lab Instructions: Unit Testing for Embedded Developers using GitHub Copilot

## Lab Overview

This hands-on lab is designed for **Embedded Developers** to learn how to design, write, refactor, and automate **unit tests** for embedded software using **GitHub Copilot**. The lab focuses on testability of low-level code, hardware abstraction, mocking, and continuous integration best practices.

All coding, test generation, and refactoring activities must be performed **using GitHub Copilot (Chat, Inline, and Agent modes)**.

---

## Learning Objectives

By the end of this lab, participants will be able to:

* Understand unit testing challenges in embedded systems
* Apply test-driven thinking to embedded C/C++ code
* Use GitHub Copilot to generate unit tests
* Mock hardware dependencies effectively
* Improve test coverage and maintainability
* Integrate unit tests into CI pipelines

---

## Target Audience

* Embedded Software Engineers
* Firmware Developers
* Automotive / IoT / Industrial Control Developers

---

## Prerequisites

* Basic knowledge of Embedded C/C++
* Familiarity with Git and GitHub
* GitHub Copilot enabled (Business or Enterprise)
* Toolchain installed (one of the following):

  * GCC / ARM-GCC
  * PlatformIO
  * CMake
* Unit testing framework:

  * Unity / CMock
  * GoogleTest (for C++)

---

## Lab Environment Setup

### Step 1: Clone Sample Repository

```bash
git clone https://github.com/<org>/embedded-unit-testing-lab.git
cd embedded-unit-testing-lab
```

### Step 2: Project Structure

```
embedded-unit-testing-lab/
├── src/              # Production code
├── include/          # Header files
├── drivers/          # Hardware-dependent code
├── tests/            # Unit tests
├── mocks/            # Mocked hardware interfaces
├── CMakeLists.txt
└── README.md
```

---

## Lab 1: Understanding Testability in Embedded Code

### Objective

Identify code that is hard to test due to hardware coupling.

### Task

Open `drivers/temperature_sensor.c`.

#### Copilot Prompt (Chat)

```text
@workspace /explain Why is this embedded code hard to unit test?
```

#### Expected Outcome

* Identify tight coupling to hardware registers
* Lack of interfaces or abstractions
* Global state usage

---

## Lab 2: Refactoring Code for Unit Testing

### Objective

Improve code structure to make it testable.

### Task

Refactor sensor logic to separate hardware access from business logic.

#### Copilot Prompt

```text
#selection Refactor this code to separate hardware access using interfaces suitable for unit testing.
```

#### Deliverables

* Introduce HAL (Hardware Abstraction Layer)
* Move logic into pure functions

---

## Lab 3: Generating Unit Tests with GitHub Copilot

### Objective

Use Copilot to generate unit tests.

### Task

Create tests for `calculate_temperature()`.

#### Copilot Prompt

```text
Write unit tests using Unity framework for the selected function, covering normal, boundary, and error cases.
```

#### Expected Tests

* Valid sensor values
* Out-of-range values
* Error conditions

---

## Lab 4: Mocking Hardware Dependencies

### Objective

Mock hardware interactions.

### Task

Mock ADC and GPIO drivers.

#### Copilot Prompt

```text
Generate mock functions for the ADC driver so that unit tests can run without hardware.
```

#### Expected Outcome

* Mocked return values
* Deterministic test execution

---

## Lab 5: Improving Test Coverage

### Objective

Increase coverage using Copilot recommendations.

### Task

Analyze uncovered code paths.

#### Copilot Prompt

```text
@workspace What additional unit tests should be added to improve code coverage?
```

---

## Lab 6: Negative and Fault Injection Testing

### Objective

Validate robustness under failure conditions.

### Task

Simulate sensor failures.

#### Copilot Prompt

```text
Create unit tests that simulate hardware failure scenarios and validate error handling.
```

---

## Lab 7: Test Refactoring and Maintainability

### Objective

Improve test readability and reuse.

#### Copilot Prompt

```text
Refactor these unit tests to reduce duplication and improve readability.
```

---

## Lab 8: Running Unit Tests in CI

### Objective

Automate unit testing.

### Task

Add a CI pipeline.

#### Copilot Prompt

```text
Create a GitHub Actions workflow to build the embedded project and run unit tests using CMake.
```

---

## Lab 9: Copilot Agent Mode (Advanced)

### Objective

End-to-end test automation using Copilot Agent.

#### Copilot Prompt

```text
@workspace /agent Create missing unit tests, add mocks, improve coverage to at least 80%, and ensure all tests pass.
```

---

## Best Practices for Embedded Unit Testing

* Avoid hardware access in unit tests
* Use dependency injection
* Keep tests fast and deterministic
* Prefer pure functions
* Separate unit tests from integration tests

---

## Evaluation Criteria

* Code testability improvements
* Test coverage percentage
* Quality of mocks
* CI pipeline success
* Effective use of GitHub Copilot

---

## Bonus Challenges

* Convert legacy embedded code to testable design
* Introduce TDD workflow using Copilot
* Add static analysis alongside unit tests

---

## Lab Completion

Participants should submit:

* Refactored source code
* Unit test files
* CI configuration
* Screenshot of passing pipeline

---

**End of Lab**
