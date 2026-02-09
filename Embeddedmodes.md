# Embedded Developers Lab – Using Ask, Edit, and Agent Modes with GitHub Copilot

## Lab Title

**Hands-on Lab: Ask, Edit, and Agent Modes for Embedded Development using GitHub Copilot**

---

## Target Audience

* Embedded Software Developers
* Firmware Engineers
* IoT / Automotive / Industrial Developers
* Embedded QA & Validation Engineers

---

## Lab Duration

90–120 minutes

---

## Prerequisites

* VS Code installed
* GitHub Copilot enabled (with Copilot Chat)
* Basic knowledge of Embedded C / C++
* Familiarity with:

  * GPIO, Timers, Interrupts
  * RTOS concepts (tasks, queues)
* Sample embedded project (bare-metal or RTOS-based)

---

## Learning Objectives

By the end of this lab, participants will be able to:

* Understand **Ask, Edit, and Agent modes** in GitHub Copilot
* Use the right Copilot mode for embedded-specific tasks
* Safely analyze, refactor, and extend firmware code
* Apply hardware, timing, and memory constraints while using Copilot
* Improve productivity without compromising reliability

---

## Why Mode Selection Matters in Embedded Development

Embedded systems are:

* Hardware-dependent
* Resource-constrained
* Safety and timing critical

Choosing the wrong Copilot mode can:

* Introduce unsafe refactors
* Break real-time behavior
* Add hidden memory usage

Correct mode usage ensures:

* Predictable firmware
* Safe refactoring
* Controlled automation

---

# Overview of GitHub Copilot Modes

## 1. Ask Mode

**Purpose:**

* Understand existing code
* Explain logic, hardware interaction, and risks

**Best for:**

* Code comprehension
* Safety analysis
* Learning unfamiliar firmware

---

## 2. Edit Mode

**Purpose:**

* Modify selected code
* Refactor with constraints

**Best for:**

* Improving readability
* Small, controlled refactors
* Fixing bugs without changing behavior

---

## 3. Agent Mode

**Purpose:**

* Perform multi-step changes
* Analyze, plan, and update multiple files

**Best for:**

* Larger embedded changes
* Driver refactoring
* RTOS integration tasks

> ⚠️ Agent mode should be used carefully in embedded systems.

---

# LAB 1: Ask Mode – Understanding Embedded Code

## Objective

Use Ask mode to safely understand firmware logic and constraints.

---

### Scenario

You are reviewing unfamiliar embedded code controlling a peripheral.

### Instructions

1. Open a driver or HAL file
2. Select a function
3. Open Copilot Chat in **Ask mode**

### Prompt

```text
Explain what this embedded C code does, including hardware interaction and timing implications
```

### Follow-up Prompts

```text
Is this code safe to run in an interrupt context?
```

```text
Are there any memory or stack usage concerns?
```

### Expected Outcome

* Clear explanation of logic
* Identification of risks
* No code changes made

---

# LAB 2: Ask Mode – Safety & Reliability Review

## Objective

Detect embedded-specific risks early.

---

### Prompt

```text
Review this code for embedded safety, race conditions, and real-time issues
```

### Expected Outcome

* Identification of blocking calls
* Shared resource risks
* Timing or ISR violations

---

# LAB 3: Edit Mode – Safe Refactoring

## Objective

Improve code quality without breaking timing or behavior.

---

### Scenario

Refactor a long function handling GPIO and delays.

### Instructions

1. Select the function
2. Switch to **Edit mode**

### Prompt

```text
Refactor this code to improve readability and maintainability without changing timing, memory usage, or behavior
```

### Expected Outcome

* Clearer structure
* Better naming
* No logic changes

---

# LAB 4: Edit Mode – Embedded Constraint-Based Changes

## Objective

Apply constrained edits safely.

---

### Context

```c
// Constraints:
// - No dynamic memory
// - ISR-safe
// - Execution time < 10us
```

### Prompt

```text
Modify the selected code to follow the above constraints
```

### Expected Outcome

* Constraint-compliant code
* No malloc/free
* Minimal logic

---

# LAB 5: Agent Mode – Multi-Step Embedded Tasks

## Objective

Use Agent mode for controlled automation.

---

### Scenario

Introduce a new sensor driver and integrate it with an RTOS task.

### Instructions

1. Switch Copilot Chat to **Agent mode**
2. Clearly describe scope and constraints

### Prompt

```text
Add a new temperature sensor driver and integrate it into the existing FreeRTOS task structure.
Constraints:
- No dynamic memory
- Use static task allocation
- Do not modify existing ISR behavior
- Follow current project coding style
```

### Expected Outcome

* New driver file
* RTOS task integration
* Minimal changes to existing code

---

# LAB 6: Agent Mode – Safe Refactor Across Files

## Objective

Perform larger refactors responsibly.

---

### Prompt

```text
Refactor the GPIO handling logic into a reusable module.
Rules:
- Preserve timing behavior
- No heap usage
- Update all call sites
- Explain changes before applying
```

### Expected Outcome

* Modularized GPIO logic
* Updated references
* Clear explanation of changes

---

# Choosing the Right Mode (Quick Guide)

| Task                | Recommended Mode |
| ------------------- | ---------------- |
| Understand firmware | Ask              |
| Safety analysis     | Ask              |
| Rename variables    | Edit             |
| Small refactor      | Edit             |
| Multi-file changes  | Agent            |
| RTOS integration    | Agent            |

---

# Embedded-Specific Best Practices

* Always **state hardware and timing constraints**
* Prefer **Ask before Edit or Agent**
* Review all Agent-generated changes carefully
* Test on target hardware after changes
* Never trust AI output blindly in safety-critical code

---

# Common Anti-Patterns

❌ "Refactor entire firmware"
❌ "Optimize everything"
❌ Using Agent mode without constraints

✅ "Explain timing risks"
✅ "Refactor selected function only"
✅ "Apply change under explicit constraints"

---

## Lab Completion Checklist

* [ ] Ask mode used to understand embedded code
* [ ] Edit mode used for safe refactoring
* [ ] Agent mode used for controlled multi-step change
* [ ] Constraints respected in all outputs
* [ ] Code reviewed and validated

---

## Key Takeaways

* Ask → Understand
* Edit → Improve safely
* Agent → Automate with guardrails

Using the right Copilot mode is critical for **safe and effective embedded development**.

---

**End of Embedded Developers Copilot Modes Lab**
