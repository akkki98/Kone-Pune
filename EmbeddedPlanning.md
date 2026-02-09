# Embedded Developers Lab – Planning with GitHub Copilot

## Lab Title

**Planning Embedded Systems Development Using GitHub Copilot**

---

## Target Audience

* Embedded Software Developers
* Firmware Engineers
* Embedded Tech Leads / Architects

---

## Lab Duration

60–90 minutes

---

## Prerequisites

* GitHub Copilot with Copilot Chat enabled
* VS Code
* Basic knowledge of embedded systems (MCUs, peripherals, RTOS basics)
* A sample or existing embedded firmware repository

---

## Learning Objectives

By the end of this lab, participants will be able to:

* Use GitHub Copilot to **plan embedded firmware development** before writing code
* Break high-level requirements into **modules, tasks, and interfaces**
* Identify **hardware, timing, and safety constraints early**
* Create design artifacts such as architecture outlines and task breakdowns using Copilot
* Reduce rework by using Copilot as a planning and reasoning assistant

---

## Why Planning Is Critical in Embedded Systems

Unlike web or backend systems, embedded systems are constrained by:

* Limited memory and CPU
* Hardware dependencies
* Real-time and safety requirements

Poor planning can lead to:

* Tight coupling between hardware and application logic
* Timing violations
* Unsafe ISR or RTOS usage

GitHub Copilot can assist **before coding begins** by helping engineers reason, design, and validate plans.

---

## Copilot Modes Used in This Lab

| Mode       | Usage in Planning                            |
| ---------- | -------------------------------------------- |
| Ask Mode   | Architecture reasoning, constraints analysis |
| Agent Mode | Repo-wide planning and impact analysis       |
| Edit Mode  | Refining design docs and plans               |

---

# LAB SCENARIO

## Scenario Description

You are designing firmware for a **Smart Sensor Node** that:

* Reads temperature and humidity sensors
* Runs on a microcontroller with limited RAM
* Optionally uses FreeRTOS
* Sends data periodically to another system

Before writing code, you must create a **clear development plan** using GitHub Copilot.

---

# LAB 1: Requirement Understanding & Clarification

## Objective

Use Copilot to clarify requirements and assumptions.

---

## Sample Copilot Prompts (Ask Mode)

```text
Summarize the functional and non-functional requirements for this embedded sensor firmware
```

```text
What assumptions should I clarify before implementing this embedded system?
```

```text
Identify real-time, memory, and power constraints for this system
```

---

## Expected Output

* Clear list of requirements
* Identified constraints and risks

---

# LAB 2: High-Level Architecture Planning

## Objective

Design the firmware architecture before implementation.

---

## Sample Copilot Prompts

```text
Propose a high-level architecture for this embedded firmware with clear module boundaries
```

```text
Which components should be hardware-specific vs application-level?
```

```text
Suggest a layered architecture suitable for a constrained embedded system
```

---

## Expected Output

* Module list (Drivers, Services, Application)
* Separation of concerns

---

# LAB 3: Task & Execution Model Planning

## Objective

Plan execution flow (bare-metal or RTOS).

---

## Sample Copilot Prompts

```text
Should this firmware use bare-metal or an RTOS? Justify the decision
```

```text
If using FreeRTOS, propose task breakdowns and priorities
```

```text
Identify which operations should run in ISRs vs deferred tasks
```

---

## Expected Output

* Execution model decision
* Task list with priorities
* ISR boundaries

---

# LAB 4: Interface & API Planning

## Objective

Define clean interfaces before coding.

---

## Sample Copilot Prompts

```text
Define clean C/C++ APIs for the sensor driver layer
```

```text
What data structures should be exposed vs kept private?
```

```text
Suggest naming conventions for embedded firmware APIs
```

---

## Expected Output

* Proposed function signatures
* Clear ownership of data

---

# LAB 5: Risk & Constraint Analysis

## Objective

Identify potential issues early.

---

## Sample Copilot Prompts

```text
What are the major risks in this embedded firmware design?
```

```text
Identify potential timing or memory bottlenecks
```

```text
How can I design this system to be testable on host or simulator?
```

---

## Expected Output

* Risk list
* Mitigation strategies

---

# LAB 6: Planning Artifacts Generation

## Objective

Generate lightweight planning documentation.

---

## Sample Copilot Prompts

```text
Generate a development plan outlining phases and milestones for this firmware
```

```text
Create a checklist for embedded firmware readiness before coding
```

```text
Draft a README section describing the planned architecture
```

---

## Expected Output

* Development plan
* Readiness checklist
* Architecture documentation

---

# LAB 7: Agent Mode – Planning Validation

## Objective

Use Copilot Agent to validate planning decisions.

---

## Sample Copilot Prompt (Agent Mode)

```text
Review this repository and planning documents and identify gaps before implementation
```

---

## Expected Output

* Identified gaps or inconsistencies
* Improvement suggestions

---

# Best Practices for Planning with Copilot (Embedded)

* Always plan **before** generating code
* Be explicit about hardware and timing constraints
* Use Copilot to challenge assumptions
* Keep plans lightweight but precise
* Revisit plans after major requirement changes

---


## Key Takeaways

* GitHub Copilot is effective **before coding begins**
* Planning with Copilot reduces defects and rework
* Especially valuable for embedded and safety-critical systems

---

**End of Embedded Developers Planning Lab – GitHub Copilot**
