# Embedded Developer Lab – Prompt Engineering Best Practices with GitHub Copilot

## Lab Title

**Prompt Engineering Best Practices for Embedded Developers using GitHub Copilot**

---

## Target Audience

* Embedded Software Developers
* Firmware Engineers
* Embedded QA / Validation Engineers
* IoT & Automotive Software Engineers

---

## Lab Duration

60 minutes

---

## Prerequisites

* VS Code installed
* GitHub Copilot enabled (with Copilot Chat)
* Basic knowledge of:

  * C / C++ (or Embedded C)
  * Microcontroller concepts (GPIO, timers, interrupts)
  * Bare-metal or RTOS-based systems
* Sample embedded project (HAL / driver-level code preferred)

---

## Learning Objectives

By the end of this lab, participants will be able to:

* Apply **prompt engineering best practices** tailored for embedded systems
* Use GitHub Copilot effectively with **hardware constraints in mind**
* Generate safer, more predictable firmware code
* Improve code readability, modularity, and testability
* Avoid common pitfalls when using AI for embedded development

---

## Why Prompt Engineering Matters for Embedded Development

Embedded systems are:

* Resource-constrained (memory, CPU, power)
* Hardware-dependent
* Safety- and reliability-critical

Poor prompts may lead to:

* Dynamic memory misuse
* Blocking delays
* Unsafe ISR logic
* Non-deterministic behavior

Well-engineered prompts help Copilot:

* Respect hardware constraints
* Follow real-time and safety rules
* Generate production-quality embedded code

---

# Core Prompt Engineering Principles (Embedded Context)

## 1. Single (One Responsibility)

Focus on **one hardware or software task at a time**.

### ❌ Poor Prompt

```text
Write full firmware for sensor, UART, logging, and error handling
```

### ✅ Good Prompt

```text
Write a function to read temperature from I2C sensor
```

---

## 2. Specific (Hardware-Aware)

Always include **hardware details and constraints**.

### ❌ Vague Prompt

```text
Initialize timer
```

### ✅ Specific Prompt

```text
Initialize TIM2 for 1ms periodic interrupt on STM32 using HAL, no dynamic memory
```

---

## 3. Short (Concise & Intent-Driven)

Avoid long narratives. Let context do the work.

### ❌ Long Prompt

```text
Create a function that toggles an LED connected to a GPIO pin every time a button is pressed while ensuring debounce logic
```

### ✅ Short Prompt

```text
Toggle LED on button press with debounce
```

---

## 4. Surround (Context Is Critical)

Use comments, existing code, and hardware rules.

```c
// Constraints:
// - No malloc/free
// - Must be ISR-safe
// - Execution < 10us
```

### Prompt

```text
Implement function based on above constraints
```

---

# LAB 1: Peripheral Driver Development

## Objective

Use Copilot to generate clean, hardware-safe driver code.

---

### Scenario

Create a GPIO driver for LED control.

### Context

```c
// Target: STM32
// GPIO: PA5
// Mode: Output push-pull
// No dynamic allocation
```

### Prompt

```text
Initialize GPIO PA5 for LED output
```

### Expected Outcome

* HAL-compliant code
* No heap usage
* Clear initialization sequence

---

# LAB 2: Interrupt Service Routine (ISR) Prompting

## Objective

Generate ISR-safe code.

---

### Context

```c
// ISR rules:
// - No blocking calls
// - No printf/logging
// - Minimal logic
```

### Prompt

```text
Implement timer interrupt handler following above ISR rules
```

### Expected Outcome

* Short ISR
* Deferred processing pattern (flags / queues)

---

# LAB 3: RTOS-Aware Prompting

## Objective

Ensure Copilot respects RTOS constraints.

---

### Context

```c
// RTOS: FreeRTOS
// Use static task allocation
// Avoid delays in critical tasks
```

### Prompt

```text
Create FreeRTOS task to read sensor every 100ms
```

### Expected Outcome

* xTaskCreateStatic usage
* vTaskDelayUntil
* Deterministic behavior

---

# LAB 4: Improving Embedded Code Readability & Maintainability

## Objective

Refactor firmware code safely.

---

### Prompt

```text
@workspace /explain How can I improve the readability of this embedded C code?
```

### Follow-up Prompt

```text
Refactor the selected code to improve maintainability without changing timing behavior
```

### Expected Outcome

* Better naming
* Clear separation of HAL vs application logic
* No timing regressions

---

# LAB 5: Safety & Reliability Prompting

## Objective

Identify unsafe patterns in embedded code.

---

### Prompt

```text
Review the selected code for embedded safety and reliability issues
```

### Follow-up Prompts

```text
Identify any race conditions or shared resource risks
```

```text
Check if this code is safe to run in an interrupt context
```

---

# LAB 6: Memory & Performance Awareness

## Objective

Ensure efficient use of resources.

---

### Prompt

```text
Analyze this code for stack, heap, and CPU usage concerns
```

### Expected Outcome

* Reduced stack usage
* No dynamic allocation
* Efficient loops

---

# Common Embedded Prompt Anti-Patterns

❌ "Optimize this code"
❌ "Make it faster"
❌ "Handle everything"

✅ "Optimize for no heap usage and deterministic timing"
✅ "Reduce stack usage below 256 bytes"
✅ "Handle error paths only"

---

# Best Practices Checklist

* [ ] Hardware and MCU specified
* [ ] Timing and memory constraints provided
* [ ] ISR/RTOS rules stated explicitly
* [ ] One responsibility per prompt
* [ ] Context provided using comments

---

## Key Takeaways

* Embedded prompting must be **constraint-driven**
* Surrounding context dramatically improves Copilot output
* Always review AI-generated firmware for safety
* Copilot is a **co-developer**, not a hardware expert

---



**End of Embedded Developer Prompt Engineering Lab**
