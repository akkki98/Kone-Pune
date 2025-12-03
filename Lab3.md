Lab: Backend Development with Node.js Using GitHub Copilot
API Endpoints • Database Operations • Error Handling • Logging • Unit Tests
Using Ask • Edit • Inline Suggestions • Agent Mode
🚀 Objective

Learn how to use GitHub Copilot to accelerate backend development in Node.js by generating:

REST API endpoints

Database CRUD logic

Centralized error handling and logging

Unit tests
You will use all Copilot modes: Ask, Edit, Inline Suggestions, and Agent mode.

🧰 Prerequisites

VS Code

GitHub Copilot Chat / Copilot Enterprise

Node.js LTS

A blank folder (no GitHub repo needed)

📦 Setup

Create a folder: backend-lab

Open in VS Code

Run:

npm init -y
npm install express mongoose winston jest supertest


Create folders:

/src
/src/routes
/src/models
/tests

🔥 LAB PART 1 — Generate API Endpoints with Copilot
STEP 1 — Create server.js using Inline Suggestions

Create src/server.js
Type the comment:

// Create an Express server with JSON middleware and a health check route


👉 Copilot will auto-generate the server setup.

If Copilot doesn't generate properly, press:

Tab (inline complete)

Ctrl+Enter (Copilot Chat: Ask)

Try prompts:

“Create an Express server with /health API and export the app.”

“Add CORS middleware and a global prefix /api.”

STEP 2 — Generate API Routes Using Copilot Chat

Create src/routes/userRoutes.js

Ask Copilot:

“Generate CRUD routes for users using Express Router. Only structure, no DB logic.”

It should produce GET, POST, PUT, DELETE route handlers.

STEP 3 — Connect Routes to Server (Copilot Edit)

Open server.js
Select the code
Ask:

“Add the userRoutes and mount them at /api/users.”

Copilot Edit will patch your file.

🔥 LAB PART 2 — Database Operations Using Copilot
STEP 4 — Create a Mongoose User Model (Inline + Ask)

Create: src/models/User.js
Write:

// Create a mongoose User schema with name, email, password, timestamps


Copilot generates model code.

Try variations:

“Make email unique.”

“Add schema validation for password length.”

“Add a virtual method fullName.”

STEP 5 — Add DB Logic in Routes Using Agent Mode

Open userRoutes.js
Ask:

“Convert these routes to use the Mongoose User model for CRUD operations.”

Copilot Agent modifies your file.

Try:

“Add pagination for GET /users.”

“Add try/catch and return proper HTTP status codes.”

🔥 LAB PART 3 — Error Handling & Logging Using Copilot
STEP 6 — Create a Centralized Error Middleware

Create: src/middleware/errorHandler.js

Prompt:

// Create an Express error-handling middleware returning JSON with message and stack in dev mode


Try variations:

“Hide stack trace in production.”

“Convert Mongoose errors to readable messages.”

STEP 7 — Integrate Winston Logger (Ask Mode)

Create:

src/logger.js

Ask Copilot:

“Create a Winston logger with levels: info, warn, error, timestamp formatting, and log file rotation.”

Then integrate it into server:

“Add logger middleware to log all incoming requests with method, URL, and response time.”

🔥 LAB PART 4 — Unit Tests with Jest & Supertest
STEP 8 — Create a test for GET /api/users

Create: tests/userRoutes.test.js

Ask Copilot:

“Write unit tests for GET /api/users using Jest and Supertest. Mock the User model.”

STEP 9 — Add Tests for POST, PUT, DELETE

Ask:

“Generate tests for POST, PUT, and DELETE /api/users following best practices.”

Try:

“Add negative test cases.”

“Mock error scenarios for database failures.”

STEP 10 — Add Jest Configuration

Ask Copilot:

“Generate jest.config.js for Node environment and use Babel or ESM support.”
