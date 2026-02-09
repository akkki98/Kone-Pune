# Embedded Developers Lab – GitHub Copilot Instructions File

## Lab Title

**Using GitHub Copilot Instructions for Embedded Development**

---

## Target Audience

* Embedded Software Developers
* Firmware Engineers
* IoT / Automotive / Industrial Developers
* Embedded QA & Validation Engineers

---

## Lab Duration

60–90 minutes

---

## Prerequisites

* VS Code installed
* GitHub Copilot enabled (with Copilot Chat)
* Basic knowledge of Embedded C / C++
* Familiarity with:

  * Microcontrollers (GPIO, Timers, Interrupts)
  * Bare-metal or RTOS-based systems
* An embedded project repository (sample or real)

---

## Learning Objectives

By the end of this lab, participants will be able to:

* Understand the purpose of **GitHub Copilot Instructions**
* Create and maintain a `.github/copilot-instructions.md` file
* Guide Copilot to generate **safe, predictable embedded firmware**
* Enforce embedded constraints such as memory, timing, and safety
* Reduce repetitive prompting by using repository-level context

---

## Why Copilot Instructions Matter for Embedded Systems

Embedded systems are:

* Resource constrained (RAM, Flash, CPU)
* Hardware dependent
* Often safety or real-time critical

Without guidance, Copilot may:

* Use dynamic memory unintentionally
* Introduce blocking delays
* Generate ISR-unsafe logic

A **Copilot Instructions file** acts as a persistent guardrail for all Copilot interactions in the repository.

---

## What Is a Copilot Instructions File?

A Copilot Instructions file provides **project-wide rules** that GitHub Copilot must follow when generating or modifying code.

**File location:**

```text
.github/copilot-instructions.md
```

---

# LAB 1: Creating the Copilot Instructions File

## Step 1: Create the Folder Structure

At the root of your repository:

```text
.github/
  copilot-instructions.md
```

---

## Step 2: Base Template for Embedded Projects

Add the following content:

```md
# GitHub Copilot Instructions – Embedded Project

## General Rules
- Generate production-ready embedded C/C++ code
- Do not change functional behavior unless explicitly requested
- Prefer clarity and determinism over clever optimizations

## Memory Constraints
- Do NOT use malloc, free, new, or delete
- Prefer static or stack allocation
- Minimize stack usage

## Timing & Real-Time Constraints
- Avoid blocking delays (busy-wait, sleep) unless specified
- Ensure deterministic execution
- Keep critical sections short

## Interrupt Safety
- ISR code must:
  - Avoid blocking calls
  - Avoid logging or printf
  - Access shared data safely

## Hardware Awareness
- Respect MCU and peripheral constraints
- Use existing HAL/driver patterns in the project

## Error Handling
- Handle all error paths explicitly
- Do not silently ignore failures

## Code Style
- Use clear, descriptive names
- Keep functions small and focused
- Separate hardware abstraction from application logic

## Testing & Validation
- Generate unit-testable logic where possible
- Do not assume availability of dynamic mocking frameworks
```

---

# LAB 2: Backend (Firmware) Instructions Validation

## Objective

Verify that Copilot follows embedded constraints automatically.

---

## Hands-on Task

### Task

Create a GPIO initialization function.

### Prompt

```text
Initialize GPIO for LED output
```

### Expected Outcome

* No dynamic memory usage
* HAL-compliant initialization
* Clear and readable code

> Notice that constraints are applied **without restating them in the prompt**.

---

# LAB 3: ISR-Specific Instructions

## Objective

Ensure Copilot generates ISR-safe code.

---

## Update Instructions File

Add the following section:

```md
## ISR-Specific Rules
- Keep ISR logic minimal
- Defer processing using flags or queues
- Do not allocate memory
```

---

## Hands-on Task

### Prompt

```text
Implement timer interrupt handler
```

### Expected Outcome

* Minimal ISR
* Deferred processing
* No blocking calls

---

# LAB 4: RTOS-Aware Instructions

## Objective

Guide Copilot when working with an RTOS.

---

## Update Instructions File

```md
## RTOS Rules
- RTOS: FreeRTOS
- Prefer static task creation
- Use vTaskDelayUntil for periodic tasks
- Avoid delays in high-priority tasks
```

---

## Hands-on Task

### Prompt

```text
Create a FreeRTOS task to read a sensor every 100ms
```

### Expected Outcome

* Static task allocation
* Deterministic periodic execution
* RTOS best practices followed

---

# LAB 5: Using Copilot Instructions with Ask & Edit Modes

## Objective

Combine instructions with Copilot modes.

---

### Ask Mode Prompt

```text
Explain this code and identify any violations of the copilot instructions
```

### Edit Mode Prompt

```text
Refactor this code to comply with the copilot instructions without changing behavior
```

### Expected Outcome

* Instruction-aware analysis
* Safe, compliant refactoring

---

# Best Practices for Embedded Copilot Instructions

* Keep rules **clear and enforceable**
* Avoid vague guidance like "optimize" or "improve"
* Update instructions as hardware or RTOS changes
* Review Copilot output regularly
* Treat instructions as **coding standards**, not suggestions

---

# Common Mistakes to Avoid

❌ Overly generic rules
❌ Missing ISR or RTOS constraints
❌ Allowing behavior changes by default

---

## Lab Completion Checklist

* [ ] `.github/copilot-instructions.md` created
* [ ] Memory and timing constraints defined
* [ ] ISR and RTOS rules added
* [ ] Copilot output respects instructions
* [ ] Code reviewed for safety

---

## Key Takeaways

* Copilot Instructions provide **persistent guardrails**
* Especially critical for embedded and safety-sensitive projects
* Reduce repetitive prompting
* Improve consistency and reliability of AI-generated firmware

---

**End of Embedded Developers Copilot Instructions Lab**
