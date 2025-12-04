# Lab Instructions: Building a Node.js Application with Custom Instructions

## Lab Overview
In this lab, you will learn how to create a Node.js application following custom coding guidelines and best practices. You'll implement the custom instructions file and test whether your development environment respects these guidelines.

**Estimated Time:** 60 minutes



---

## Lab Objectives

By the end of this lab, you will be able to:
1. Use AI agents to automate project setup
2. Create a custom instructions file for project-specific guidelines
3. Set up a Node.js application with Express.js
4. Test custom instructions with various coding scenarios
5. Implement code following specific style guides and best practices
6. Validate that AI assistants follow your custom guidelines

---

## Lab Structure

### Part 0: Automated Project Setup with AI Agent (15 minutes)
### Part 1: Environment Setup (10 minutes)
### Part 2: Create Custom Instructions (15 minutes)
### Part 3: Build the Node.js Application (20 minutes)
### Part 4: Test Custom Instructions (25 minutes)
### Part 5: Validate and Review (15 minutes)

---

## Part 0: Automated Project Setup with AI Agent

Instead of manually creating files, you'll use GitHub Copilot Chat to automate the entire project setup.

### Step 0.1: Open Copilot Chat in VS Code

1. Press `Ctrl+Shift+I` (or `Cmd+Shift+I` on Mac) to open Copilot Chat
2. Or click the chat icon in the Activity Bar

### Step 0.2: Use Agent to Create Complete Project

**Prompt to use in Copilot Chat:**
```
@workspace Create a complete Node.js project with the following:
1. Project folder named "node-custom-instructions-lab"
2. Initialize package.json with proper metadata
3. Install express and nodemon as dependencies
4. Create server.js with basic Express setup including:
   - Middleware for JSON parsing
   - Health check endpoint at /health
   - Welcome endpoint at /
   - Error handling middleware
5. Create .customInstructions file with coding guidelines for:
   - Code style (camelCase, PascalCase, UPPER_CASE)
   - API design (RESTful, JSON responses, HTTP status codes)
   - Error handling (try-catch, logging, user-friendly messages)
   - Security (input validation, env variables, rate limiting)
   - Performance (async/await, caching, optimization)
6. Create .gitignore file
7. Create README.md with project documentation
8. Add npm scripts for start and dev modes
```

**Expected Output:**
The agent should create all files and structure automatically.

### Step 0.3: Verify Automated Setup

**Prompt to verify:**
```
@workspace Show me the project structure and list all created files
```

**✓ Checkpoint:** You should see:
```
node-custom-instructions-lab/
├── server.js
├── package.json
├── .customInstructions
├── .gitignore
├── README.md
└── node_modules/
```



## Part 2: Validate Custom Instructions

### Step 2.1: Review Generated Custom Instructions

**Prompt:**
```
@workspace Show me the contents of .customInstructions file
```

### Step 2.2: Enhance Custom Instructions (Optional)

**Prompt:**
```
Add these additional guidelines to .customInstructions:
- Database: Use parameterized queries to prevent SQL injection
- Logging: Use structured logging with timestamp and severity levels
- Documentation: Add JSDoc comments for all public functions
```

### Step 2.3: Verify Guidelines Are Active

**Prompt:**
```
Are you following the custom instructions from .customInstructions file?
```

**✓ Checkpoint:** Agent should confirm it's aware of your custom guidelines.

---

## Part 3: Build the Node.js Application with Agent Assistance

### Step 3.1: Add Score Calculation Feature

**Prompt:**
```
Following the custom instructions in .customInstructions, create a function to calculate user total score based on quiz, assignment, and participation scores with configurable weights
```

**Expected Outcome:**
- Function uses camelCase: `calculateUserTotalScore`
- Constants use UPPER_CASE: `DEFAULT_WEIGHTS`
- Includes JSDoc comments
- Follows single responsibility principle

### Step 3.2: Add API Endpoint for Score Calculation

**Prompt:**
```
Create a POST endpoint at /api/user/calculate-score that uses the calculateUserTotalScore function. Follow all custom instructions for API design, error handling, and validation.
```

**Expected Outcome:**
- RESTful endpoint design
- Input validation
- Try-catch error handling
- Proper HTTP status codes (200, 400, 500)
- JSON response format

### Step 3.3: Test the New Endpoint

**Prompt:**
```
@terminal Start the development server
```

Then use another prompt:
```
@terminal Test the /api/user/calculate-score endpoint with sample data using curl or provide a test command
```

**✓ Checkpoint:** Server should start and endpoint should respond correctly.

---

## Part 4: Test Custom Instructions Systematically

### Test 1: Code Style Compliance

**Prompt:**
```
Create a User class with properties for id, email, name, and createdAt. Follow the naming conventions in .customInstructions
```

**Validation Checklist:**
- [ ] Class name uses PascalCase: `User`
- [ ] Properties use camelCase: `createdAt`
- [ ] Includes constructor with validation
- [ ] Has JSDoc comments

---

### Test 2: API Design - CRUD Operations

**Prompt:**
```
Create RESTful CRUD endpoints for managing products. Include:
- GET /api/products (list all)
- GET /api/products/:id (get one)
- POST /api/products (create)
- PUT /api/products/:id (update)
- DELETE /api/products/:id (delete)
Follow all custom instructions for API design.
```

**Validation Checklist:**
- [ ] RESTful route naming
- [ ] Proper HTTP methods
- [ ] Correct status codes (200, 201, 400, 404, 500)
- [ ] JSON responses
- [ ] Input validation
- [ ] Error handling

---

### Test 3: Security Implementation

**Prompt:**
```
Add input validation and sanitization for the user registration endpoint. Validate email format, password strength (min 8 chars, 1 uppercase, 1 number, 1 special char), and sanitize name input.
```

**Validation Checklist:**
- [ ] Email regex validation
- [ ] Password strength validation
- [ ] Input sanitization
- [ ] Error messages for invalid input
- [ ] No sensitive data in error responses

---

### Test 4: Async Operations & Error Handling

**Prompt:**
```
Create an async function that fetches user data from a mock external API with proper error handling, timeout, and retry logic. Follow custom instructions for async/await and error handling.
```

**Validation Checklist:**
- [ ] Uses async/await (not callbacks)
- [ ] Try-catch block present
- [ ] Error logging with context
- [ ] User-friendly error messages
- [ ] Timeout handling

---

### Test 5: Performance Optimization

**Prompt:**
```
Implement an in-memory caching mechanism for the GET /api/products endpoint with a 5-minute TTL. Follow performance guidelines in custom instructions.
```

**Validation Checklist:**
- [ ] Cache implementation present
- [ ] TTL (Time To Live) configured
- [ ] Cache hit/miss logic
- [ ] Memory-efficient approach

---

## Part 5: Comprehensive Validation

### Exercise 5.1: Agent-Assisted Code Review

**Prompt:**
```
@workspace Review all files in this project and verify they follow the guidelines in .customInstructions. Provide a detailed report with any violations found.
```

**Expected Output:**
A comprehensive report showing compliance or violations for:
- Naming conventions
- API design patterns
- Error handling
- Security practices
- Performance optimizations

### Exercise 5.2: Auto-Generate Tests

**Prompt:**
```
Generate unit tests for the calculateUserTotalScore function following the testing guidelines in .customInstructions (aim for 80% coverage).
```

**Validation Checklist:**
- [ ] Test file created (e.g., `server.test.js`)
- [ ] Multiple test cases
- [ ] Edge cases covered
- [ ] Assertions present



### Task 5.3: Environment Configuration

**Prompt:**
```
Create a .env.example file and update the application to use environment variables for:
- PORT
- NODE_ENV
- API_TIMEOUT
- CACHE_TTL
Follow security guidelines in .customInstructions
```

---



**Congratulations!** You've completed the advanced lab on building a Node.js application using AI agents with custom instructions. You now understand how to leverage AI for automated development while maintaining code quality standards.
