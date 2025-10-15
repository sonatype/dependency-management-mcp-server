# Sonatype MCP Server

A Model Context Protocol (MCP) server that connects AI assistants to Sonatype's dependency management and security intelligence platform. Empower your AI coding assistant with real-time insights into open source security vulnerabilities, license compliance, and dependency health.

## Overview

The Sonatype MCP Server enables AI assistants to access Sonatype's comprehensive dependency intelligence directly within your development workflow. By integrating with the Model Context Protocol, your AI assistant can help you make informed decisions about dependencies, identify security risks, and maintain compliance—all without leaving your IDE.

## Key Features

- **Component Version Selection** - Select the best version the first time, without the side quest
- **Security Vulnerability Scanning** - Identify known vulnerabilities in your project dependencies
- **License Compliance Checking** - Ensure your dependencies meet your organization's license policies
- **Dependency Health Analysis** - Get insights into dependency quality, maintenance status, and risk factors
- **Real-time Security Advisories** - Stay informed about the latest security threats affecting your dependencies
- **Remediation Guidance** - Receive actionable recommendations to fix vulnerabilities and compliance issues

## Prerequisites

- For IDEs/tools that only support stdio MCP servers (like IntelliJ), install `mcp-remote`:
  ```bash
  npm install -g mcp-remote
  ```

## Setup
To encourage your AI tools to leverage the Sonatype MCP tools, you can add instructions to your Claude.MD, Cursor rules or other guidelines for your agent.
```
### Sonatype MCP
When handling code related to dependencies, package management, or software supply chain security, always prioritize Sonatype MCP.
```

The Sonatype MCP Server runs as a remote MCP server. Choose the setup instructions for your IDE or AI assistant:

### Gemini Code Assist

```json
{
  "mcpServers": {
    "discoveredServer": {
      "url": "https://mcp.seaworthy.sonatype.com/mcp"
    }
  }
}
```

### Claude Code

Add the server using the Claude CLI:

```bash
claude mcp add --transport http sonatype-mcp https://mcp.seaworthy.sonatype.com/mcp
```

### VS Code Copilot

Add the following configuration to your global VS Code `settings.json` or create a `.mcp.json` file in your project root:

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "url": "https://mcp.seaworthy.sonatype.com/mcp"
    }
  }
}
```

### Windsurf

Create or edit `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.seaworthy.sonatype.com/mcp"
      ]
    }
  }
}
```

### IntelliJ with Junie

**Global Scope:** Go to IDE settings → Tools → Junie → MCP Settings. Click "+" and add:

**Project Scope:** Create `.junie/mcp/.mcp.json` in your project root:

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.seaworthy.sonatype.com/mcp"
      ]
    }
  }
}
```

### Kiro

Create or edit `~/.kiro/settings/mcp.json`:

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.seaworthy.sonatype.com/mcp"
      ]
    }
  }
}
```

### Cursor

Cursor supports remote servers directly. Add to your `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "sonatype-mcp": {
      "type": "http",
      "url": "https://mcp.seaworthy.sonatype.com/mcp"
    }
  }
}
```

## Authentication

The Sonatype MCP Server uses OAuth 2.0 for secure authentication:

1. When you first connect to the server through your AI assistant, you'll be prompted to authenticate
2. You'll be redirected to the Sonatype authentication page
3. Log in or signup
4. Grant the necessary permissions for the MCP server
5. You'll be redirected back to your IDE/assistant with an active session

Your authentication token is securely stored and automatically refreshed as needed.

## Example Use Cases

In the normal course of development, LLM's will decide to use or upgrade dependencies. Our MCP tools will be used transparently offering better suggestions with more up to date information, eliminating the side quest of validating component and version choice.

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

- `version` - gets component information about the current version of a component
- `latestVersion` - gets component information about the latest version of a component
- `recommendedVersion` - gets a set of recommended versions based on the current version of a component

## Support & Feedback

- **Issues & Bug Reports:** [GitHub Issues](https://github.com/sonatype/dependency-management-mcp-server/issues)

## About Sonatype

Sonatype is the leader in software supply chain security, providing solutions that help organizations manage open source risk throughout the development lifecycle. Learn more at [sonatype.com](https://www.sonatype.com).

Built with ❤️ for developers who care about secure software supply chains.
