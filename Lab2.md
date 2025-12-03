# 🧪 Prompt Engineering for GitHub Copilot — Node.js Edition

## 🎯 Objective

Learn to craft high-quality prompts using the **4S Method (Single, Specific, Short, Surround)** while building a Node.js application using **GitHub Copilot Ask, Edit & Chat**.

---

## 📦 SECTION 1 — Setup

### ✅ Prerequisites

* Visual Studio Code
* GitHub Copilot Chat or Copilot Enterprise
* Node.js LTS
* Sample folder on desktop
* GitHub Copilot extension enabled

### ▶️ Initialize Node.js Project

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

## 📚 SECTION 2 — Understanding the 4 Principles (4S)

### **1. Single** – Ask Copilot to perform *one* task.

### **2. Specific** – Provide exact instructions.

### **3. Short** – Keep prompts concise and readable.

### **4. Surround** – Give context (files, code blocks, filenames).

Each exercise focuses on one principle.

---

## 🧪 SECTION 3 — Lab Exercises

### **Exercise 1 — SINGLE Prompt Principle**

**Goal:** Ask Copilot to perform *only one* task.

❌ **Bad Prompt:**

```
Create a /health endpoint, add logging, and convert the project to ES modules. Also write tests.
```

Now run:

✅ **Good Prompt:**

```
Add a new endpoint `/health` that returns { status: "ok" } as JSON.
```

✔️ *Expected:* Copilot updates only the route—no extra changes.

---

### **Exercise 2 — SPECIFIC Prompt Principle**

**Goal:** Provide explicit, detailed instructions.

❌ **Bad Prompt:**

```
Improve the API.
```

Now run:

✅ **Good Prompt:**

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

❌ **Bad Prompt:** Too wordy.

```
I want you to create a Node.js controller function... (long description)
```

Now send:

✅ **Good Prompt:**

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

✔️ Copilot uses the surrounding context to generate correct code.

---

## 🏁 SECTION 4 — Final Challenge (All 4 Principles)

**Goal:** Combine all 4 principles.

Open `index.js`, `users.service.js`, `users.controller.js`.

Run this prompt:

````
Add a new search endpoint `/users/search?name=`.
Context:
- Use users from users.service.js
- Match by case-insensitive partial name
- Return [] if no match
- Put logic in users.controller.js as `searchUsers`
- Wire it into index.js usi# Lab: Prompt Engineering for GitHub Copilot — Node.js Edition

##  **Objective**
Learn to craft high-quality prompts using the **4S Principles**:
- **Single** – One clear task
- **Specific** – Detailed instructions
- **Short** – Concise and readable
- **Surround** – Provide context (files, code, filenames)

You will apply these principles directly in **Visual Studio Code** while building a small **Node.js Express application** using GitHub Copilot (Ask, Edit & Chat).

---

# ------------------------------------------------------------
# **SECTION 1 — Setup**
# ------------------------------------------------------------

##  **Prerequisites**
- Visual Studio Code
- GitHub Copilot Chat or GitHub Copilot Enterprise
- Node.js LTS installed
- A sample folder on desktop
- GitHub Copilot extension enabled

##  **Initialize Node.js Project**
Open VS Code → Terminal:
```bash
mkdir prompt-lab-node
cd prompt-lab-node
npm init -y
npm install express
````

Create `index.js` with this boilerplate:

```javascript
const express = require("express");
const app = express();
app.get("/", (req, res) => res.send("Hello"));
app.listen(3000);
```

---

# ------------------------------------------------------------

# **SECTION 2 — Understanding the 4 Principles (4S)**

# ------------------------------------------------------------

### **1. SINGLE** – One clear task per prompt.

### **2. SPECIFIC** – Provide detailed instructions.

### **3. SHORT** – Keep it concise.

### **4. SURROUND** – Give context (file names, code blocks, open files).

You will now practice each principle individually.

---

# ------------------------------------------------------------

# **SECTION 3 — Lab Exercises**

# ------------------------------------------------------------

##  **Exercise 1 — SINGLE Prompt Principle**

Goal: Ask Copilot to perform *one* task.

###  **Bad Prompt (Multiple tasks)**

```
Create a /health endpoint, add logging, and also convert the project to ES modules. Also write tests.
```

###  **Good Prompt (Single Task)**

```
Add a new endpoint `/health` that returns { status: "ok" } as JSON.
```

### *What to Observe*

* Copilot performs only one change.
* No unrelated modifications.

---

##  **Exercise 2 — SPECIFIC Prompt Principle**

Goal: Provide explicit instructions.

###  **Bad Prompt (Not specific)**

```
Improve the API.
```

###  **Good Prompt (Specific)**

```
Add request-logging middleware that logs the HTTP method and URL in the format:
"[METHOD] /path"
Apply this middleware globally before all routes.
```

###  *Expected Output*

```javascript
app.use((req, res, next) => {
  console.log(`[${req.method}] ${req.url}`);
  next();
});
```

---

## **Exercise 3 — SHORT Prompt Principle**

Goal: Reduce prompt size without losing clarity.

###  **Bad Prompt (Too verbose)**

```
I want you to create a Node.js controller function that will fetch a user by ID and then I want that function to also validate the ID and then return proper status codes. Ensure the parsing and validation is done correctly including error messages and follow best practices.
```

### **Good Prompt (Short)**

```
Create a GET `/users/:id` route.
- Validate id is a number
- If invalid → return 400
- If not found → return 404
- Otherwise return user object
```

---

##  **Exercise 4 — SURROUND Principle**

Goal: Provide full context.

Create `users.service.js`:

```javascript
const users = [
  { id: 1, name: "Akshay" },
  { id: 2, name: "Pavan" }
];

module.exports = { users };
```

Open **users.service.js** and **users.controller.js** side-by-side.

### Prompt:

```
Based on the code in `users.service.js`, generate a controller function `getAllUsers` in `users.controller.js` that returns the users array as JSON.
```

### *Expected:* Copilot uses workspace context correctly.

---

# ------------------------------------------------------------

# **SECTION 4 — Final Challenge (All 4 Principles)**

# ------------------------------------------------------------

Goal: Apply **Single + Specific + Short + Surround** together.

### Open these files:

* `index.js`
* `users.service.js`
* `users.controller.js`

### Run this final prompt:

```
Add a new search endpoint `/users/search?name=`.

Context:
- Use users from users.service.js
- Match by case-insensitive partial name
- Return [] if no match
- Put logic in users.controller.js in a function `searchUsers`
- Wire it in index.js using Express routing
```

---

# 🎉 **Lab Completed!**

You now have a single unified Markdown instruction file for the **Node.js Prompt Engineering Lab** using GitHub Copilot.
