
# **GitHub Copilot Lab --- Ask, Edit & Agent Mode for Node.js**

## **Objective**

This lab teaches how to use GitHub Copilot's **Ask**, **Edit**, and
**Agent Mode** features to build and enhance a Node.js Express
application.

## **Prerequisites**

-   Visual Studio Code\
-   GitHub Copilot enabled (Chat + Agent mode)\
-   Node.js LTS installed\
-   GitHub Copilot Chat extension installed

# **SECTION 1 --- Using Copilot ASK**

## **Goal:** Learn how to use *Ask* to generate and understand code.

### **Task 1: Create a Node.js Project**

#### **Prompt (Ask Mode)**

Create a Node.js project with Express including a health check endpoint
`/health` returning status: ok. Provide the folder structure, commands,
and code.

### **Task 2: Understand Code**

#### **Prompt (Ask Mode)**

Explain how `app.listen()` works in Express and how request routing is
processed internally.

# **SECTION 2 --- Using Copilot EDIT**

## **Goal:** Modify existing code using Edit instructions.

### **Task 1: Add a Users Endpoint**

#### **Prompt (Edit Mode)**

Add a new route `/users` that returns a list of users from an in-memory
array. Format the response as JSON. Don't change the existing `/health`
endpoint.

### **Task 2: Add Request Logging Middleware**

#### **Prompt (Edit Mode)**

Add middleware that logs the HTTP method and URL for every request.
Apply it globally.

### **Task 3: Generate Unit Tests**

#### **Prompt (Ask/Edit Mode)**

Generate Jest tests for the `/users` endpoint including status code,
array length, and JSON structure.

# **SECTION 3 --- Using Copilot AGENT MODE**

## **Goal:** Use Copilot as an autonomous coding agent to perform multi-step tasks.

### **Task 1: Refactor Project into Modular Architecture**

#### **Prompt (Agent Mode)**

You are my coding agent. Refactor this Node.js Express app into a
modular architecture with: - /routes folder - /controllers folder -
/services folder Move the `/users` logic into users.controller.js and
users.service.js. Update imports and ensure the app runs exactly as
before. Explain what you changed after refactoring. Begin only after
confirming you understand the task.

### **Task 2: Add Error Handling Automatically**

#### **Prompt (Agent Mode)**

Add centralized error handling with a global error middleware. Update
the `/users` service to throw an error if the user list is empty. Modify
the controller to catch and forward errors. Ensure the app returns JSON
error responses with status and message.

### **Task 3: Add Search Feature End-to-End**

#### **Prompt (Agent Mode)**

Add a new endpoint `/users/search?name=` that returns users matching the
search query. Implement this in the service and controller layers.
Update routes and Jest tests. Validate by running tests.

# **Summary**

This lab covered how to use GitHub Copilot features to enhance Node.js
development.
