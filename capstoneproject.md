# User Onboarding Workflow System

## GitHub Copilot–Driven Full‑Stack Application Lab

---

## Problem Statement

Build a **secure User Onboarding and Approval Platform** where:

* End users can **self-register**
* Newly registered users are placed in **PENDING** state
* An **administrator** can approve or reject users
* Only **approved users** can authenticate and access the system

The system must enforce strong security practices, clean architecture, and scalability principles, and **the entire application must be developed using GitHub Copilot**.

---

## Ultimate Requirement

> ⚠️ **All code, configuration, Docker files, and documentation must be created using GitHub Copilot (Chat, Edit, Agent modes).**

---

## Technology Stack

| Layer            | Technology                               |
| ---------------- | ---------------------------------------- |
| Frontend         | React.js                                 |
| Backend          | .NET / Node.js / Java / Python (any one) |
| Database         | SQL Database                             |
| Containerization | Docker                                   |
| Auth             | JWT-based Authentication                 |

---

## High-Level Architecture

* **Frontend (React)** – User & Admin UI
* **Backend API** – Authentication, onboarding workflow, approval logic
* **Database** – User persistence
* **Containers** – Backend & Frontend containerized
* **Secrets** – Provided only via environment variables

Key Principles:

* Stateless backend
* Clear separation of concerns
* Horizontally scalable design

---

# Scenario 1: Backend Development Using GitHub Copilot

## Objective

Create a secure backend that supports user onboarding, approval workflow, and authentication.

---

## Functional Requirements

### User Lifecycle

1. **User Registration**

   * Input validation
   * Password hashing
   * User stored with status = `PENDING`

2. **Admin Review**

   * Admin can view all pending users
   * Admin can approve or reject users

3. **Authentication**

   * Only `APPROVED` users can log in
   * Invalid state transitions must be blocked

---

## Required API Endpoints

| Method | Endpoint            | Description          |
| ------ | ------------------- | -------------------- |
| POST   | /auth/register      | Register new user    |
| POST   | /auth/login         | Login approved users |
| GET    | /admin/pending      | List pending users   |
| POST   | /admin/approve/{id} | Approve user         |
| POST   | /admin/reject/{id}  | Reject user          |

---

## Sample GitHub Copilot Prompts (Backend)

```text
Create a secure user registration endpoint with password hashing and status=PENDING
```

```text
Prevent login if user status is not APPROVED
```

```text
Implement admin-only middleware to approve or reject users
```

```text
Validate state transitions in the user lifecycle
```

---

## Success Criteria (Backend)

* ✅ Valid registration creates user with status=PENDING
* ✅ GET /admin/pending lists pending users
* ✅ Approve/reject updates status correctly
* ✅ Approved users can authenticate
* ❌ Invalid state transitions are blocked

---

# Scenario 2: Frontend Development Using React + Copilot

## Objective

Create a role-aware frontend UI for users and administrators.

---

## Functional Requirements

### Regular User

* Register with client-side validation
* Login and view personalized status
* See **“Awaiting Approval”** if pending

### Admin User

* Login securely
* View list of pending users
* Approve or reject users
* UI updates immediately after action

> Non-admin users must **never** see admin controls.

---

## Sample GitHub Copilot Prompts (Frontend)

```text
Create a React registration form with validation and error handling
```

```text
Show conditional UI based on user role and approval status
```

```text
Build an admin dashboard to approve or reject users
```

```text
Update UI immediately after backend approval action
```

---

## Success Criteria (Frontend)

* ✅ Registration with validation
* ✅ Pending users see correct status
* ✅ Admin can approve/reject users
* ✅ UI reflects changes instantly
* ❌ Non-admin users cannot access admin features

---

# Scenario 3: Containerization Using GitHub Copilot

## Objective

Containerize backend and frontend using Docker with production-ready practices.

---

## Requirements

* Multi-stage Docker build
* Non-root runtime user
* Secrets passed via environment variables
* No hardcoded credentials
* Backend and frontend in separate containers

---

## Sample GitHub Copilot Prompt (Backend Dockerfile)

```text
Create a production-ready multi-stage Dockerfile for a .NET 8 Web API backend that restores, builds, and publishes the app in a build stage (using the official .NET 8 SDK image), then runs it in a runtime stage (using the official .NET 8 ASP.NET image) as a non-root user, exposes port 8080, and expects all secrets (like DB connection string, JWT secret, and Service Bus key) to be provided via environment variables at runtime. Also, provide a .dockerignore file to exclude bin, obj, .git, node_modules, and local config files, and include example docker build and docker run commands showing how to pass required environment variables.
```

---

## Example Docker Commands

```bash
# Build image
docker build -t onboarding-backend .

# Run container
docker run -p 8080:8080 \
  -e DB_CONNECTION_STRING=... \
  -e JWT_SECRET=... \
  -e SERVICE_BUS_KEY=... \
  onboarding-backend
```

---

## Success Criteria (Containerization)

* ✅ Backend and frontend run in containers
* ✅ No secrets in source code
* ✅ Environment variables used correctly
* ✅ Application is stateless and scalable

---


## Key Takeaways

* GitHub Copilot can drive **end-to-end application development**
* Strong prompts lead to secure, scalable designs
* Copilot supports not just coding, but architecture and DevOps

---

**End of User Onboarding Workflow System – Copilot Lab**
