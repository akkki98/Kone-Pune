# Lab: Creating an Optimized Production Dockerfile for Node.js


**Learning Objectives:**
- Create production-ready Dockerfiles using GitHub Copilot
- Implement multi-stage builds for optimization
- Apply security best practices
- Minimize Docker image size
- Optimize build performance with layer caching


---

## Prerequisites

### Required Software
- ✅ Docker Desktop for Windows
  ```bash
  docker --version
  # Should show Docker version 20.x or higher
  ```
- ✅ Visual Studio Code with GitHub Copilot extension
- ✅ Node.js v18 or higher
- ✅ Git

### Required Knowledge
- Basic Docker concepts (images, containers, layers)
- Understanding of Node.js applications
- Familiarity with YAML/configuration files

### Project Setup
Ensure you have a Node.js project with:
```
node2/
├── package.json
├── package-lock.json
├── index.js (or server.js)
└── src/ (optional)
```

---

## Step 1: Choose the Right Base Image

### 1.1 Understanding Base Image Options

**Node.js Base Image Variants:**

| Image | Size | Use Case |
|-------|------|----------|
| `node:20` | ~1GB | Development, full OS |
| `node:20-slim` | ~200MB | Production, fewer tools |
| `node:20-alpine` | ~120MB | Production, minimal |
| `node:20-bullseye-slim` | ~230MB | Production, Debian-based |

### 1.2 Choosing Alpine for Production

**Why Alpine Linux?**
- ✅ Smallest size (~5MB base)
- ✅ Security-focused
- ✅ Fast builds
- ✅ Active maintenance
- ⚠️ Uses musl libc (may have compatibility issues with some native modules)

### 1.3 Using Copilot to Select Base Image

**Prompt for Copilot:**
```dockerfile
# Select the best Node.js 20 base image for production with minimal size
```


```

### 1.4 Pinning Specific Versions

**Best Practice: Use Specific Versions**

Ask Copilot:
```
Why should I use specific version tags for Docker base images?
```


---

## Step 2: Understand Multi-Stage Builds

### 2.1 What Are Multi-Stage Builds?

Multi-stage builds allow you to:
- Separate build-time dependencies from runtime
- Reduce final image size
- Keep build tools out of production
- Improve security

### 2.2 Multi-Stage Build Structure

```dockerfile
# Stage 1: Build stage (includes dev dependencies, build tools)
FROM node:20-alpine AS builder
# ... install all dependencies
# ... run tests
# ... build application

# Stage 2: Production stage (only runtime dependencies)
FROM node:20-alpine AS production
# ... copy only what's needed from builder
# ... install production dependencies only
```

### 2.3 Benefits Comparison

**Without Multi-Stage:**
```dockerfile
FROM node:20-alpine
COPY package*.json ./
RUN npm install  # Installs dev + prod dependencies
COPY . .
# Final image: ~400MB
```

**With Multi-Stage:**
```dockerfile
FROM node:20-alpine AS builder
RUN npm install  # All dependencies

FROM node:20-alpine AS production
RUN npm ci --only=production  # Production only
# Final image: ~180MB
```

**Size Reduction: ~55%**

---

## Step 3: Create Basic Production Dockerfile

### 3.1 Initial Dockerfile Structure

Create a new file named `Dockerfile` and use Copilot:

**Type this comment:**
```dockerfile
# Production Dockerfile for Node.js Express application with multi-stage build
```

**Press Enter and let Copilot suggest:**

````dockerfile
// filepath: c:\Users\AkshayKS\source\repos\node2\Dockerfile
# Production Dockerfile for Node.js Express application with multi-stage build

# Build stage
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install all dependencies (including dev dependencies for build)
RUN npm ci

# Copy application source
COPY . .

# Run build step if needed (TypeScript, webpack, etc.)
RUN npm run build --if-present

# Production stage
FROM node:20-alpine AS production

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install only production dependencies
RUN npm ci --only=production

# Copy application files from builder
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/index.js ./

# Expose application port
EXPOSE 3000

# Set Node

 Final Production Dockerfile
6.1 Combining All Optimizations
Ask GitHub Copilot:
Create an optimized production Dockerfile for Node.js with all best practices: multi-stage build, Alpine base, non-root user, health checks, security updates, and optimized caching
