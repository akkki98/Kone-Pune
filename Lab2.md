#  Prompt Engineering for GitHub Copilot — Node.js Edition

##  Objective

Learn to craft high-quality prompts using the **4S Method (Single, Specific, Short, Surround)** while building a Node.js application using **GitHub Copilot Ask, Edit & Chat**.

---

##  SECTION 1 — Setup

###  Prerequisites

* Visual Studio Code
* GitHub Copilot Chat or Copilot Enterprise
* Node.js LTS
* Sample folder on desktop
* GitHub Copilot extension enabled

###  Initialize Node.js Project

Open VS Code terminal and run:

```
mkdir prompt-lab-node
cd prompt-lab-node
npm init -y
npm install express
```

Create **index.js**:

```js
const express = require("express");
const app = express();
app.get("/", (req, res) => res.send("Hello"));
app.listen(3000);
```

---

##  SECTION 2 — Understanding the 4 Principles (4S)

### **1. Single** – Ask Copilot to perform *one* task.

### **2. Specific** – Provide exact instructions.

### **3. Short** – Keep prompts concise and readable.

### **4. Surround** – Give context (files, code blocks, filenames).

Each exercise focuses on one principle.

---

## 🧪 SECTION 3 — Lab Exercises

### **Exercise 1 — SINGLE Prompt Principle**

**Goal:** Ask Copilot to perform *only one* task.

 **Bad Prompt:**

```
Create a /health endpoint, add logging, and convert the project to ES modules. Also write tests.
```

Now run:

**Good Prompt:**

```
Add a new endpoint `/health` that returns { status: "ok" } as JSON.
```

 *Expected:* Copilot updates only the route—no extra changes.

---

### **Exercise 2 — SPECIFIC Prompt Principle**

**Goal:** Provide explicit, detailed instructions.

 **Bad Prompt:**

```
Improve the API.
```

Now run:

 **Good Prompt:**

```
Add request-logging middleware that logs: "[METHOD] /path".
Apply it globally before all routes.
```

Expected Copilot output:

```js
app.use((req, res, next) => {
  console.log(`[${req.method}] ${req.url}`);
  next();
});
```

---

### **Exercise 3 — SHORT Prompt Principle**

**Goal:** Make prompts concise but clear.

 **Bad Prompt:** Too wordy.

```
I want you to create a Node.js controller function... (long description)
```

Now send:

 **Good Prompt:**

```
Create a GET `/users/:id` route.
- Validate id is a number
- If invalid → 400
- If not found → 404
- Otherwise return user
```

---

### **Exercise 4 — SURROUND Principle**

**Goal:** Provide context with open files + code.

Create **users.service.js**:

```js
const users = [
  { id: 1, name: "Akshay" },
  { id: 2, name: "Pavan" }
];
module.exports = { users };
```

Open **users.service.js** and **users.controller.js**.

Now prompt:

```
Based on `users.service.js`, generate a controller function `getAllUsers` in `users.controller.js` that returns the users array as JSON.
```

 Copilot uses the surrounding context to generate correct code.

---



# 🎉 **Lab Completed!**

You now have a single unified Markdown instruction file for the **Node.js Prompt Engineering Lab** using GitHub Copilot.
