# GitHub MCP Server Lab Instructions

## Overview
This lab demonstrates how to use the GitHub MCP (Model Context Protocol) server with GitHub Copilot in Visual Studio Code to interact with GitHub repositories, issues, branches, pull requests, and more through natural language commands.



---

## Prerequisites

Before starting this lab, ensure you have:

- ✅ **Visual Studio Code** installed (latest version)
- ✅ **GitHub Copilot** extension installed with active subscription
- ✅ **Node.js** (v18 or higher) and npm installed
- ✅ **Git** installed and configured with your GitHub account
- ✅ A **GitHub repository** to work with (can be any existing repo)
- ✅ Internet connection for API calls

---

## Project Setup

### Step 1: Create a New Node.js Project

Open a terminal in your workspace folder:

```powershell
# Create project directory
mkdir github-mcp-demo
cd github-mcp-demo

# Initialize Node.js project
npm init -y

# Install dependencies
npm install express
npm install --save-dev nodemon
```

### Step 2: Create Application Files

Create `index.js`:

```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.json());

app.get('/', (req, res) => {
  res.json({ 
    message: 'GitHub MCP Demo API',
    timestamp: new Date().toISOString()
  });
});

app.get('/health', (req, res) => {
  res.json({ status: 'healthy' });
});

app.listen(PORT, () => {
  console.log(`✅ Server running on http://localhost:${PORT}`);
});
```




---

## MCP Server Configuration

### Step 1: Create .vscode Folder Structure

```powershell
# Create .vscode directory if it doesn't exist
New-Item -ItemType Directory -Force -Path .vscode
```

### Step 2: Create MCP Configuration File

Create `.vscode/mcp.json`:

```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

### Step 3: Verify File Structure

Your project should now look like this:

```
github-mcp-demo/
├── .vscode/
│   └── mcp.json
├── node_modules/
├── index.js
├── package.json
└── package-lock.json
```

---

## Connecting to GitHub MCP

### Step 1: Open GitHub Copilot Chat

- Press `Ctrl+Alt+I` (Windows) or `Cmd+Alt+I` (Mac)
- Or click the GitHub Copilot icon in the Activity Bar

### Step 2: Verify GitHub Copilot Extension

1. Open Extensions (`Ctrl+Shift+X`)
2. Search for **"GitHub Copilot"**
3. Ensure it shows "Installed" and is enabled
4. Check that you're signed in to your GitHub account

### Step 3: Connect to MCP Server

1. Open Command Palette (`Ctrl+Shift+P`)
2. Type: `Copilot: Connect to MCP Server`
3. Select **github** from the server list
4. Authenticate with GitHub if prompted
5. Wait for confirmation message

### Step 4: Verify Connection

In Copilot Chat, try:
```
Show my GitHub profile
```

If you see your profile information, the connection is successful! ✅

---

## Basic MCP Commands

### Repository Information

```plaintext
# View repository details
Show repository information for this project
List all files in the repository
Show repository statistics

# Search within repository
Search for files containing 'express' in this repository
Find all JavaScript files
Show me the contents of package.json
```

### Branch Management

```plaintext
# List branches
List all branches in this repository
Show active branches
List branches that haven't been merged

# Branch operations
Create a new branch called 'feature/add-logging'
Show me the latest commit on the main branch
Get branch protection rules for main
```

### Issues Management

```plaintext
# View issues
List all open issues
Show issues labeled 'bug'
Display issues assigned to me
Show closed issues from the last week

# Create and modify issues
Create an issue titled 'Add error handling' with label 'enhancement'
Add a comment to issue #5 saying 'Working on this'
Close issue #3 with comment 'Fixed in PR #10'
```

### Pull Requests

```plaintext
# View pull requests
List all open pull requests
Show PRs created by me
Display PR #7 details
Show the diff for PR #3

# PR operations
Create a pull request from feature/new-api to main
Review pull request #5
Merge pull request #8
```

### Commits and History

```plaintext
# View commits
Show me the last 10 commits
Get details of commit abc123def
List commits from the last 7 days
Show commits by author 'username'

# Commit information
Show files changed in the latest commit
Display commit message for commit xyz789
```

Congratulations! 🎉 You've completed the GitHub MCP Server lab.

