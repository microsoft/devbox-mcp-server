# 🏢 Dev Box MCP Server

[![Install with NPX in VS Code](https://img.shields.io/badge/VS_Code-Install_Dev_Box_MCP_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=DevBox&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40microsoft%2Fdevbox-mcp%40latest%22%5D%7D) [![Install with NPX in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_Dev_Box_MCP_Server-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=DevBox&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40microsoft%2Fdevbox-mcp%40latest%22%5D%7D&quality=insiders)

This is a Model Context Protocol (MCP) server for [Microsoft Dev Box](https://azure.microsoft.com/en-us/products/dev-box), providing seamless integration between AI agents and Microsoft Dev Box services. This server enables natural language interactions for developer-focused operations like managing Dev Boxes, configurations, and pools.

## 🔌 Getting Started

### Prerequisites

1. **Node.js 18 or newer**

2. **Azure Resources**

    - Azure subscription
    - Dev Center provisioned
    - At least one Dev Center project created
    - Appropriate RBAC permissions on Dev Center resources

3. **MCP Client**

-   Install your [MCP host/client](https://modelcontextprotocol.io/introduction#general-architecture) of choice
-   Recommended MCP clients include:
    -   [Visual Studio Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_add-an-mcp-server) with GitHub Copilot extension
    -   [Visual Studio 2022](https://learn.microsoft.com/en-us/visualstudio/ide/mcp-servers?view=vs-2022) version 17.14 or later

### Installation

Dev Box MCP Server can be installed on any MCP clients, such as Visual Studio or Visual Studio Code (VS Code). Below are the detailed steps for installing on Visual Studio Code.

For installation steps on Visual Studio, see [here](https://learn.microsoft.com/en-us/visualstudio/ide/mcp-servers?view=vs-2022)

#### ✨ One-Click Install on VS Code

Click one of these buttons to install the Dev Box MCP Server for VS Code or VS Code Insiders.

[![Install with NPX in VS Code](https://img.shields.io/badge/VS_Code-Install_Dev_Box_MCP_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=DevBox&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40microsoft%2Fdevbox-mcp%40latest%22%5D%7D) [![Install with NPX in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_Dev_Box_MCP_Server-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=DevBox&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40microsoft%2Fdevbox-mcp%40latest%22%5D%7D&quality=insiders)

Just one click, and you're ready to go! 🎉

#### 🔧 Manual Install on VS Code

For a step-by-step installation, follow one of the following instructions:

1. Add `.vscode/mcp.json` to your workspace:

```json
{
    "servers": {
        "DevBox": {
            "command": "npx",
            "args": ["-y", "@microsoft/devbox-mcp@latest"]
        }
    }
}
```

2. Alternatively, add to your [user settings.json](https://code.visualstudio.com/docs/getstarted/personalize-vscode#_configure-settings):

```json
{
    "mcp": {
        "servers": {
            "DevBox": {
                "command": "npx",
                "args": ["-y", "@microsoft/devbox-mcp@latest"]
            }
        }
    }
}
```

3. You can also add Dev Box MCP programmatically using VS Code CLI:

```bash
# For VS Code
code --add-mcp '{"name":"DevBox","command":"npx","args":["-y","@microsoft/devbox-mcp@latest"]}'
```

For detailed MCP installation steps on VS Code, see [here](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).

## VSCode Installation Demo

![VSCode Installation Demo](docs/MCP-Install-Works.gif)

## ❓ FAQ

### Tool call failed with 'Tool xxx does not have an implementation registered' or 'I apologize for the technical issue'

If you encounter this error, it's likely due to an invalid tool cache issue in GitHub Copilot Agent mode. To resolve the issue:

1. Press `Ctrl+Shift+P` to open the command palette
2. Run `MCP: Reset cached tools`
3. Restart the MCP server

For more details, see [GitHub issue #177](https://github.com/github/github-mcp-server/issues/177)

### Error: Cannot find module '../build/Release/keytar.node'

If you encounter this error, try running `npx clear-npx-cache`.

If you encounter other errors when starting the MCP server, you may also try the command above.

## 🛠️ Currently Supported Tools

The Dev Box MCP provides tools for interacting with the following Microsoft Dev Box resources:

### 💻 Dev Box Lifecycle

-   **DevBox Resource**: Unified tool for DevBox management using scope patterns
    -   List all DevBoxes across projects: `/projects/*/users/me/devboxes/*` (operation: `read`)
    -   List DevBoxes in specific project: `/projects/ProjectName/users/me/devboxes/*` (operation: `read`)
    -   Get specific DevBox details: `/projects/ProjectName/users/me/devboxes/DevBoxName` (operation: `read`)
    -   Query DevBox by name across projects: `/projects/*/users/me/devboxes/DevBoxName` (operation: `read`)
    -   Create new DevBox: `/projects/ProjectName/users/me/devboxes/NewDevBoxName` (operation: `create`)
    -   Delete existing DevBox: `/projects/ProjectName/users/me/devboxes/DevBoxName` (operation: `delete`)

### 📂 Projects

-   **Project Resource**: Unified tool for Project management using scope patterns
    -   List all projects: `/projects/*` (operation: `read`)
    -   Get specific project details: `/projects/projectName` (operation: `read`)

### 🏊 Dev Box Pools

-   **List Pools By Project**: View all available Dev Box pools in a project

### 🎯 Actions & Schedules

-   **DevBox Action**: Unified tool for DevBox power management using scope patterns

    -   Start DevBox: `/projects/ProjectName/users/userId/devboxes/DevBoxName` (action: `start`)
    -   Stop DevBox: `/projects/ProjectName/users/userId/devboxes/DevBoxName` (action: `stop`)
    -   Restart DevBox: `/projects/ProjectName/users/userId/devboxes/DevBoxName` (action: `restart`)
    -   Repair DevBox: `/projects/ProjectName/users/userId/devboxes/DevBoxName` (action: `repair`)
    -   Get Remote Connection: `/projects/ProjectName/users/userId/devboxes/DevBoxName` (action: `getRemoteConnection`)

-   **Schedule Resource**: Unified tool for DevBox schedule management using scope patterns
    -   List all schedules: `/projects/ProjectName/users/userId/devboxes/DevBoxName` (action: `listAll`)
    -   Delay all scheduled actions: `/projects/ProjectName/users/userId/devboxes/DevBoxName` (action: `delayAll`)
    -   Skip all scheduled actions: `/projects/ProjectName/users/userId/devboxes/DevBoxName` (action: `skipAll`)

### 📦 Customization

-   **List Customization Task Definitions By Project**: View available customization tasks in a project
-   **Get Customization Task Definitions**: Get details of a specific customization task
-   **Validate Customization Tasks**: Validate a list of customization tasks
-   **List Customization Groups**: View all customization groups for a Dev Box
-   **Get Customization Group**: Get details of a specific customization group
-   **Create Customization Group**: Apply customizations to a Dev Box
-   **Get Imaging Task Log**: View logs for an imaging build task
-   **Run Tasks On Dev Box**: Install packages or run commands on a Dev Box
-   **Get Customization Task Log**: View logs for a customization task
-   **Set Dev Box Theme**: Change the visual theme (dark/light) for a Dev Box

### 🔄 Operations

-   **Get Operation Status**: Check status of long-running operations

### 🤔 Thinking

-   **DevBox Think**: Provides context for understanding and performing Dev Box operations

## 🔑 Authentication

The Dev Box MCP Server uses [DefaultAzureCredential](https://learn.microsoft.com/en-us/javascript/api/@azure/identity/defaultazurecredential?view=azure-node-latest) and [WAM (Web Account Manager)](https://learn.microsoft.com/en-us/entra/identity-platform/scenario-desktop-acquire-token-wam) based brokered authentication for seamless Azure integration.

Authentication follows this credential chain order:

1. **Environment Variables** (`EnvironmentCredential`)
2. **Managed Identity** (`ManagedIdentityCredential`)
3. **Visual Studio Code** (`VisualStudioCredential`)
4. **Azure CLI** (`AzureCliCredential`)
5. **Azure PowerShell** (`AzurePowerShellCredential`)
6. **Azure Developer CLI** (`AzureDeveloperCliCredential`)
7. **Windows SSO (Single Sign-On)** (WAM - Web Account Manager)

The credential chain will attempt each method in order until a successful authentication is achieved. WAM provides seamless single sign-on experience on Windows platforms, automatically using your existing Windows credentials when available.

If you encounter authentication errors, try:

1. Make sure you're logged in to Windows SSO (Single Sign-On) or Azure CLI
2. Verify you have the necessary permissions in your Azure subscription
3. Check if you need to specify a specific tenant using `az login --tenant <tenant-id>`

## 🛡️ License

Copyright (c) Microsoft Corporation. All rights reserved.
