# Lab Instructions: Adding Microsoft Learn MCP Server

## Objective
Configure your Visual Studio Code workspace to include the Microsoft Learn MCP (Model Context Protocol) server for accessing Microsoft documentation and learning resources.

## Prerequisites
- Visual Studio Code installed
- GitHub Copilot extension installed
- Workspace folder open: `c:\Users\AkshayKS\source\repos\node2`
- Active internet connection

## Steps

### 1. Locate the MCP Configuration File
The MCP configuration file is already present at:
```
c:\Users\AkshayKS\source\repos\node2\.vscode\mcp.json
```

### 2. Update the Configuration
Add the Microsoft Learn MCP server to your existing configuration in `mcp.json`:

```json
{
  "servers": {
    "microsoft.docs.mcp": {
      "type": "http",
      "url": "https://learn.microsoft.com/api/mcp"
    }
  }
}
```

### 3. Save the File
Press `Ctrl+S` to save the changes to `mcp.json`.

### 4. Reload VS Code Window
To apply the new MCP configuration:
1. Press `Ctrl+Shift+P` to open the Command Palette
2. Type "Reload Window" and select **Developer: Reload Window**

### 5. Verify the Configuration
After reloading, the Microsoft Learn MCP server should now be available to provide documentation context.

## Testing Examples

Test the Microsoft Learn MCP server integration by asking Copilot the following questions in the chat:

### Example 1: Azure Services
```
@workspace What are the best practices for deploying an Azure Function App?
```
**Expected**: Copilot should provide information from Microsoft Learn about Azure Functions deployment.

### Example 2: .NET Documentation
```
@workspace How do I implement dependency injection in ASP.NET Core?
```
**Expected**: Copilot should reference official Microsoft documentation for ASP.NET Core DI.

### Example 3: TypeScript/JavaScript
```
@workspace What are the TypeScript configuration options for strict mode?
```
**Expected**: Copilot should provide details from Microsoft's TypeScript documentation.

### Example 4: Visual Studio Code
```
@workspace How do I create a custom VS Code extension?
```
**Expected**: Copilot should reference VS Code extension development documentation.

### Example 5: Azure SDK
```
@workspace Show me how to use Azure Blob Storage SDK in Node.js
```
**Expected**: Copilot should provide code examples using the official Azure SDK.

### Example 6: Azure Static Web Apps
```
@workspace What are the deployment options for Azure Static Web Apps?
```
**Expected**: Copilot should provide information about SWA deployment methods and best practices.

## What You've Accomplished
You've successfully configured the Microsoft Learn MCP server in your workspace, enabling:
- **Enhanced Documentation Access**: Copilot can now reference official Microsoft documentation
- **Better Context**: More accurate answers for Microsoft technologies
- **Learning Resources**: Access to tutorials and best practices from Microsoft Learn
- **Azure Integration**: Improved support for Azure development workflows

