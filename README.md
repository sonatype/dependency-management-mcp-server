# Sonatype MCP Server

A Model Context Protocol (MCP) server that connects AI assistants to Sonatype's dependency management and security intelligence platform. Empower your AI coding assistant with real-time insights into open source security vulnerabilities, license compliance, and dependency health.

## Overview

The Sonatype MCP Server enables AI assistants to access Sonatype's comprehensive dependency intelligence directly within your development workflow. By integrating with the Model Context Protocol, your AI assistant can help you make informed decisions about dependencies, identify security risks, and maintain compliance — all without leaving your IDE.

## Key Features

- **Component Version Selection** - Select the best version the first time, without the side quest
- **Security Vulnerability Scanning** - Identify known vulnerabilities in your project dependencies
- **License Compliance Checking** - Ensure your dependencies meet your organization's license policies
- **Dependency Health Analysis** - Get insights into dependency quality, maintenance status, and risk factors
- **Real-time Security Advisories** - Stay informed about the latest security threats affecting your dependencies
- **Remediation Guidance** - Receive actionable recommendations to fix vulnerabilities and compliance issues

## Prerequisites

- For IDEs or tools that only support stdio MCP servers (like IntelliJ), install `mcp-remote`:
  ```bash
  npm install -g mcp-remote
  ```

## Setup

The Sonatype MCP Server runs as a remote MCP server. Choose the setup instructions for your IDE or AI assistant:

### Gemini Code Assist

Replace `<your-token>` with your personal API token generated at https://guide.sonatype.com/settings/tokens

```json
{
  "mcpServers": {
    "discoveredServer": {
      "httpUrl": "https://mcp.guide.sonatype.com/mcp",
      "headers": {
        "Authorization": "Bearer <your-token>"
      }
    }
  }
}
```

### Claude Code

Add the server using the Claude CLI:

Replace `<your-token>` with your personal API token generated at https://guide.sonatype.com/settings/tokens

```bash
claude mcp add --transport http --scope user sonatype-mcp https://mcp.guide.sonatype.com/mcp --header "Authorization: Bearer <your-token>"
```

### VS Code Copilot

Add the following configuration to your global VS Code `mcp.json` or create a `.vscode/mcp.json` file in your workspace:

Replace `<your-token>` with your personal API token generated at https://guide.sonatype.com/settings/tokens

```json
{
  "servers": {
		"sonatype-mcp": {
			"url": "https://mcp.guide.sonatype.com/mcp",
			"type": "http",
			"headers": {
				"Authorization": "Bearer <your-token>"
			}
		}
	}
}
```

### Windsurf

Create or edit `~/.codeium/windsurf/mcp_config.json`:

Replace `<your-token>` with your personal API token generated at https://guide.sonatype.com/settings/tokens

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.guide.sonatype.com/mcp",
        "--header",
        "Authorization: Bearer <your-token>"
      ]
    }
  }
}
```

### IntelliJ with Junie

**Global Scope:** Go to IDE settings → Tools → Junie → MCP Settings. Click "+" and add:

**Project Scope:** Create `.junie/mcp/.mcp.json` in your project root:

Replace `<your-token>` with your personal API token generated at https://guide.sonatype.com/settings/tokens

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.guide.sonatype.com/mcp",
        "--header",
        "Authorization: Bearer <your-token>"
      ]
    }
  }
}
```

### Kiro

Create or edit `~/.kiro/settings/mcp.json`:

Replace `<your-token>` with your personal API token generated at https://guide.sonatype.com/settings/tokens

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.guide.sonatype.com/mcp",
        "--header",
        "Authorization: Bearer <your-token>"
      ]
    }
  }
}
```

### Cursor

Cursor supports remote servers directly. Add to your `~/.cursor/mcp.json`:

Replace `<your-token>` with your personal API token generated at https://guide.sonatype.com/settings/tokens

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "type": "http",
      "url": "https://mcp.guide.sonatype.com/mcp",
      "headers": {
        "Authorization": "Bearer <your-token>"
      }
    }
  }
}
```

### Codex (IDE Plugin & CLI)
For both methods below, define an environment variable SONATYPE_GUIDE_MCP_TOKEN for your personal API token generated at https://guide.sonatype.com/settings/tokens.

Method 1:
Using CLI command: `codex mcp add sonatype-mcp --url https://mcp.guide.sonatype.com/mcp --bearer-token-env-var SONATYPE_GUIDE_MCP_TOKEN`

Method 2:
Create or edit `~/.codex/config.toml`:

```toml
[mcp_servers.sonatype-mcp]
url = "https://mcp.guide.sonatype.com/mcp"
bearer_token_env_var = "SONATYPE_GUIDE_MCP_TOKEN"
```

## Authentication

The Sonatype MCP Server uses API token authentication:

1. Create a Sonatype Guide account and generate your personal API token at https://guide.sonatype.com/settings/tokens
2. Add the token to your MCP configuration using the `Authorization: Bearer <your-token>` header format
3. Replace `<your-token>` with your actual token in the configuration examples above

Your API token authenticates all requests automatically. Keep your token secure and never commit it to version control.

## Configuring AI Assistant Rules

To maximize the effectiveness of the Sonatype MCP Server, configure your AI assistant to prioritize using Sonatype MCP tools when working with dependencies, packages, or software supply chain security. Below are instructions for each supported IDE or tool.

### Claude Code

Create custom instructions using CLAUDE.md files:

**Global (all projects):** Create `~/.claude/CLAUDE.md`

**Project (specific repository):** Create `.claude/CLAUDE.md` in your project root

Add the following instruction:

```markdown
## Sonatype MCP

When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP tools. Use the available MCP tools to research versions, check for vulnerabilities, and get recommendations before adding or updating any dependencies.
```

### Cursor

Create a `.cursorrules` file in your project root:

**Project (specific repository):** Create `.cursorrules` in your project root

Add the following instruction:

```markdown
## Sonatype MCP

When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP tools. Use the available MCP tools to research versions, check for vulnerabilities, and get recommendations before adding or updating any dependencies.
```

### VS Code Copilot

Create custom instructions using a `.github/copilot-instructions.md` file:

**Project (specific repository):** Create `.github/copilot-instructions.md` in your project root

Add the following instruction:

```markdown
## Sonatype MCP

When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP tools. Use the available MCP tools to research versions, check for vulnerabilities, and get recommendations before adding or updating any dependencies.
```

### Windsurf

Create rules using Windsurf's Customizations feature:

**Global (all projects):**
1. Click the "Rules, Memories & Workflows" icon in the top right of Cascade Code or search Rules in Windsurf Settings
2. Navigate to "Rules"
3. Click "+ Global" to create a new global rule
4. Add the following content:

```markdown
## Sonatype MCP

When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP tools. Use the available MCP tools to research versions, check for vulnerabilities, and get recommendations before adding or updating any dependencies.
```

**Project (specific repository):** 
Follow the instructions for Global but click "+ Workspace" or create `.windsurf/rules/sonatype.md` in your project root:

```markdown
## Sonatype MCP

When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP tools. Use the available MCP tools to research versions, check for vulnerabilities, and get recommendations before adding or updating any dependencies.
```

### IntelliJ with Junie

Create custom guidelines using a `.junie/guidelines.md` file:

**Project (specific repository):** Create `.junie/guidelines.md` in your project root

Add the following instruction:

```markdown
## Sonatype MCP

When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP tools. Use the available MCP tools to research versions, check for vulnerabilities, and get recommendations before adding or updating any dependencies.
```

### Kiro

Create steering files in the `.kiro/steering/` directory:

**Project (specific repository):** Create `.kiro/steering/sonatype.md` in your project root

Add YAML front matter to make it always included:

```markdown
---
inclusion: always
---

## Sonatype MCP

When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP tools. Use the available MCP tools to research versions, check for vulnerabilities, and get recommendations before adding or updating any dependencies.
```

### Gemini Code Assist

Create custom instructions using GEMINI.md files:

**Global (all projects):** Create `~/.gemini/GEMINI.md`

**Project (specific repository):** Create `GEMINI.md` in your project root

Add the following instruction:

```markdown
## Sonatype MCP

When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP tools. Use the available MCP tools to research versions, check for vulnerabilities, and get recommendations before adding or updating any dependencies.
```

## Example Use Cases

In the normal course of development, LLMs will decide to use or upgrade dependencies. Our MCP tools will be used transparently, offering better suggestions with more up-to-date information, eliminating the side quest of validating component and version choices.

Here are some ways to leverage the Sonatype MCP Server explicitly in your development workflow:

### Analyze a Specific Version

Ask your AI assistant:
> "Get detailed security information for react 18.2.0"

The assistant will return comprehensive details including CVEs with CVSS scores, license information, categories, end-of-life status, and catalog date.

### Find the Latest Stable Version

Ask your AI assistant:
> "What's the latest stable version of spring-boot?"

The assistant will return the latest version with full security analysis, policy violations, licenses, risk scores, and upgrade recommendations.

### Security Assessment Workflow

The assistant can use both tools to compare your current version with the latest and provide actionable security guidance.

## Available Tools

The Sonatype MCP Server provides three powerful tools for AI assistants:

- `getComponentVersion` - Gets component information about a specific version of a component
- `getLatestComponentVersion` - Gets component information about the latest version of a component
- `getRecommendedComponentVersions` - Gets a set of recommended versions to upgrade to based on the current version of a component. If no version is provided, gets a set of recommended versions to start with for the component

## Support & Feedback

- **Issues & Bug Reports:** [GitHub Issues](https://github.com/sonatype/dependency-management-mcp-server/issues)

## About Sonatype

Sonatype is the leader in software supply chain security, providing solutions that help organizations manage open source risk throughout the development lifecycle. Learn more at [sonatype.com](https://www.sonatype.com).

Built with ❤️ for developers who care about secure software supply chains.
