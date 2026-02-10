# GitHub Copilot for CLI – Hands-on Lab

## Lab Title

**Using GitHub Copilot for CLI to Accelerate Command-Line Productivity**

---

## Target Audience

* Developers
* DevOps Engineers
* Platform Engineers
* Embedded & Cloud Engineers

---

## Lab Duration

60 minutes

---

## Prerequisites

* GitHub account with GitHub Copilot enabled
* GitHub Copilot CLI installed (`gh copilot`)
* Terminal access (Linux / macOS / Windows with WSL)
* Basic familiarity with command-line tools (git, docker, kubectl, az/aws)

---

## Learning Objectives

By the end of this lab, participants will be able to:

* Understand what GitHub Copilot for CLI is and when to use it
* Use Copilot to **generate, explain, and fix CLI commands**
* Safely execute Copilot-suggested commands
* Apply Copilot CLI for Git, Docker, Kubernetes, and Cloud workflows
* Improve productivity while maintaining command-line safety

---

## What Is GitHub Copilot for CLI?

GitHub Copilot for CLI allows you to:

* Ask for shell commands in natural language
* Get explanations of complex commands
* Debug or correct failing commands

It is especially useful when:

* You don’t remember exact flags or syntax
* You want to avoid searching documentation
* You need safe, reproducible commands quickly

---

## Copilot CLI Command Basics

Common Copilot CLI commands:

```bash
gh copilot suggest "<what you want to do>"
```

```bash
gh copilot explain "<command>"
```

```bash
gh copilot fix "<failing command>"
```

> ⚠️ Always review suggested commands before executing them.

---

# LAB SCENARIOS

---

## Lab 1: Generating Safe Shell Commands

### Objective

Use Copilot to generate correct CLI commands from intent.

---

### Task

Generate a command to list all files larger than 100MB in the current directory.

### Copilot CLI Prompt

```bash
gh copilot suggest "find files larger than 100MB in the current directory"
```

### Expected Outcome

* Correct `find` command
* Explanation of flags

---

## Lab 2: Explaining Complex Commands

### Objective

Understand unfamiliar CLI commands.

---

### Task

Explain a Docker run command.

### Copilot CLI Prompt

```bash
gh copilot explain "docker run -d -p 8080:80 --name web nginx"
```

### Expected Outcome

* Clear explanation of each flag
* Understanding of container behavior

---

## Lab 3: Fixing a Broken Command

### Objective

Debug incorrect CLI commands using Copilot.

---

### Task

Fix a failing Git command.

### Broken Command

```bash
git push origin main --force-with-leasee
```

### Copilot CLI Prompt

```bash
gh copilot fix "git push origin main --force-with-leasee"
```

### Expected Outcome

* Corrected command
* Explanation of the fix

---

## Lab 4: Git Workflow Assistance

### Objective

Use Copilot CLI for common Git tasks.

---

### Tasks & Prompts

```bash
gh copilot suggest "create a new git branch and push it to origin"
```

```bash
gh copilot suggest "undo the last commit but keep changes staged"
```

```bash
gh copilot explain "git rebase -i HEAD~3"
```

---

## Lab 5: Docker & Container Operations

### Objective

Accelerate container workflows.

---

### Tasks & Prompts

```bash
gh copilot suggest "build a docker image with tag myapp:1.0"
```

```bash
gh copilot suggest "remove all stopped docker containers"
```

```bash
gh copilot explain "docker system prune -a"
```

---

## Lab 6: Kubernetes Operations

### Objective

Generate kubectl commands safely.

---

### Tasks & Prompts

```bash
gh copilot suggest "get all pods in all namespaces"
```

```bash
gh copilot suggest "restart a deployment named api in namespace prod"
```

```bash
gh copilot explain "kubectl rollout status deployment/api -n prod"
```

---

## Lab 7: Cloud CLI Assistance

### Objective

Use Copilot with cloud CLIs.

---

### Tasks & Prompts (Examples)

```bash
gh copilot suggest "list all azure resource groups"
```

```bash
gh copilot suggest "create an s3 bucket named my-demo-bucket"
```

---

## Lab 8: Safety & Review Best Practices

### Objective

Use Copilot CLI responsibly.

---

## Guidelines

* Always review commands before execution
* Be cautious with delete, prune, or force operations
* Prefer dry-run flags when available
* Use Copilot explanations to understand impact

### Safety Prompt

```bash
gh copilot explain "rm -rf /"
```

---


## Key Takeaways

* GitHub Copilot for CLI is a **productivity accelerator**, not an autopilot
* Best used for command discovery, explanation, and correction
* Human review is essential for safety
* Especially powerful for DevOps and platform workflows

---

**End of GitHub Copilot for CLI – Hands-on Lab**
