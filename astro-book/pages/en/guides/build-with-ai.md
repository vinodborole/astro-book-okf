---
type: Web Page
title: Building Astro sites with AI tools | Docs
description: Resources and tips for building Astro sites with AI assistance
resource: https://docs.astro.build/en/guides/build-with-ai
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Building Astro sites with AI tools

AI-powered editors and agentic coding tools generally have good knowledge of Astro’s core APIs and concepts. However, some may use older APIs and may not be aware of newer features or recent changes to the framework.

This guide covers how to enhance AI tools with up-to-date Astro knowledge and provides best practices for building Astro sites with AI assistance.

## Astro Docs MCP Server

Section titled “Astro Docs MCP Server”You can ensure your AI tools have current Astro knowledge through the Astro Docs MCP (Model Context Protocol) server. This provides real-time access to the latest documentation, helping AI tools avoid outdated recommendations and ensuring they understand current best practices.

Model Context Protocol (MCP) is a standardized way for AI tools to access external tools and data sources.

Unlike AI models trained on static data, the MCP server provides access to the latest Astro documentation. The server is free, open-source, and runs remotely with nothing to install locally.

The Astro Docs MCP server uses the kapa.ai API to maintain an up-to-date index of the Astro documentation.

### Server Details

Section titled “Server Details”- **Name**: Astro Docs
- **URL**:- `https://mcp.docs.astro.build/mcp`
- **Transport**: Streamable HTTP

### Installation

Section titled “Installation”The setup process varies depending on your AI development tool. You may see some tools refer to MCP servers as connectors, adapters, extensions, or plugins.

#### Manual setup

Section titled “Manual setup”Many tools support a common JSON configuration format for MCP servers. If there are not specific instructions for your chosen tool, you may be able to add the Astro Docs MCP server by including the following configuration in your tool’s MCP settings:

#### Claude Code CLI

Section titled “Claude Code CLI”Claude Code is an agentic coding tool that runs on the command line. Enabling the Astro Docs MCP server allows it to access the latest documentation while generating Astro code.

Install using the terminal command:

More info on using MCP servers with Claude Code

#### Claude Code GitHub Action

Section titled “Claude Code GitHub Action”Claude Code also provides a GitHub Action that can be used to run commands in response to GitHub events. Enabling the Astro Docs MCP server allows it to access the latest documentation while answering questions in comments or generating Astro code.

You can configure it to use the Astro Docs MCP server for documentation access by adding the following to the workflow file:

More info on using MCP servers with the Claude Code GitHub Action

#### Codex CLI

Section titled “Codex CLI”Codex CLI is a command-line AI coding tool that can use the Astro Docs MCP server to access documentation while generating Astro code.

You can configure MCP servers at the global level in the `~/.codex/config.toml` file, or in a `.codex/config.toml` file in a project root.

More info on using MCP servers with Codex CLI

#### Cursor

Section titled “Cursor”Cursor is an AI code editor. Adding the Astro Docs MCP server allows Cursor to access the latest Astro documentation while performing development tasks.

Install by clicking the button below:

Add to CursorMore info on using MCP servers with Cursor

#### Visual Studio Code

Section titled “Visual Studio Code”Visual Studio Code supports MCP servers when using Copilot Chat. Adding the Astro Docs MCP server allows VS Code to access the latest Astro documentation when answering questions or performing coding tasks.

Install by clicking the button below:

Add to VS CodeMore info on using MCP servers with VS Code

Warp (formerly Warp Terminal) is an agent development environment built for coding with multiple AI agents. Adding the Astro Docs MCP server allows Warp to access the latest Astro documentation when answering questions or performing coding tasks.

- Open your Warp settings and go to AI > MCP Servers > Manage MCP Servers.
- Click “Add”.
- Enter the following configuration. You can optionally configure the Astro MCP server to activate on startup using the `start_on_launch`flag:
- Click “Save”.

More info on using MCP servers with Warp

#### Claude.ai / Claude Desktop

Section titled “Claude.ai / Claude Desktop”Claude.ai is a general-purpose AI assistant. Adding the Astro Docs MCP server allows it to access the latest documentation when answering Astro questions or generating Astro code.

- Navigate to the Claude.ai connector settings.
- Click “Add custom connector”. You may need to scroll down to find this option.
- Enter the server URL: `https://mcp.docs.astro.build/mcp`.
- Set the name to “Astro docs”.

More info on using MCP servers with Claude.ai

#### Windsurf

Section titled “Windsurf”Windsurf is an AI-powered agentic coding tool, available as editor plugins or a standalone editor. It can use the Astro Docs MCP server to access documentation while performing coding tasks.

Windsurf doesn’t support streaming HTTP, so it requires a local proxy configuration:

- 
Open `~/.codeium/windsurf/mcp_config.json`in your editor.
- 
Add the following configuration to your Windsurf MCP settings: 
- 
Save the configuration and restart Windsurf. 

More info on using MCP servers with Windsurf

#### Gemini CLI

Section titled “Gemini CLI”Gemini CLI is a command-line AI coding tool that can use the Astro Docs MCP server to access documentation while generating Astro code.

You can configure MCP servers at the global level in the `~/.gemini/settings.json` file, or in a `.gemini/settings.json` file in a project root.

More info on using MCP servers with Gemini CLI

#### Google Antigravity

Section titled “Google Antigravity”Google Antigravity is an agentic development platform.

- Open `~/.gemini/antigravity/mcp_config.json`by following the Connecting Custom MCP Servers guide.
- Add the following configuration to `mcp_config.json`:
- Save the file and click “Refresh” in the “Manage MCPs” tab.

Zed supports MCP servers when using its AI capabilities. It can use the Astro Docs MCP server to access documentation while performing coding tasks.

- 
Open `~/.config/zed/settings.json`in your editor.
- 
Add the following configuration to your Zed MCP settings: 
- 
Save the configuration. 

More info on using MCP servers with Zed

#### ChatGPT

Section titled “ChatGPT”Refer to the OpenAI MCP documentation for specific setup instructions.

#### Raycast

Section titled “Raycast”Raycast can connect to MCP servers to enhance its AI capabilities. Adding the Astro Docs MCP server allows Raycast to access the latest Astro documentation while answering questions.

Install by clicking the button below:

Add to RaycastMore info on using MCP servers with Raycast

#### Opencode AI

Section titled “Opencode AI”Opencode AI is an open-source, terminal-based AI coding tool that can use the Astro Docs MCP server to access documentation while generating Astro code.

You can configure MCP servers in your Opencode configuration file, typically named `opencode.json`, located in your project root or your global configuration directory (e.g. `~/.config/opencode/opencode.json`).

More info on using Opencode AI

#### GitHub Copilot Coding Agent

Section titled “GitHub Copilot Coding Agent”GitHub Copilot can be used as a coding agent powered by GitHub Actions. Enabling the Astro Docs MCP server allows it to access the latest Astro documentation when answering questions or performing coding tasks.

You can configure it to use the Astro Docs MCP server for documentation access by adding the following to your repository’s Copilot coding agent settings available at `https://github.com/<your-org>/<your-repo>/settings/copilot/coding_agent`:

Learn more about extending GitHub Copilot coding agent with MCP servers.

Once configured, you can ask your AI tool questions about Astro, and it will retrieve information directly from the latest docs. Coding agents will be able to consult the latest documentation when performing coding tasks, and chatbots will be able to accurately answer questions about Astro features, APIs, and best practices.

The Astro Docs MCP server provides access to current documentation, but your AI tools are still responsible for interpretation and code generation. AI makes mistakes, so always review generated code carefully and test thoroughly.

### Troubleshooting

Section titled “Troubleshooting”If you encounter issues:

- Verify that your tool supports streamable HTTP transport.
- Check that the server URL is correct: `https://mcp.docs.astro.build/mcp`.
- Ensure your tool has proper internet access.
- Consult your specific tool’s MCP integration documentation.

If you are still having problems, open an issue in the Astro Docs MCP Server repository.

## Discord AI Support

Section titled “Discord AI Support”The same technology that powers Astro’s MCP server is also available as a chatbot in the Astro Discord for self-serve support. Visit the `#support-ai` channel to ask questions about Astro or your project code in natural language. Your conversation is automatically threaded, and you can ask an unlimited number of follow-up questions.

**Conversations with the chatbot are public, and are subject to the same server rules for language and behavior as the rest of our channels**, but they are not actively visited by our volunteer support members. For assistance from the community, please create a thread in our regular `#support` channel.

## Background mode

Section titled “Background mode”
	**Added in:**
	`astro@7.0.0`
	New
	

When an AI coding agent is detected, `astro dev` automatically starts the dev server as a detached background process. This prevents the dev server from blocking the agent’s terminal and allows it to continue working while the server runs.

A lock file (`.astro/dev.json`) is written when the dev server starts, recording the server’s URL, port, and PID. This prevents duplicate servers from being started for the same project.

If you are not using an AI coding agent, `astro dev` starts in the foreground process and logs to the terminal.

To opt out of automatic background mode, set the `ASTRO_DEV_BACKGROUND` environment variable before running `astro dev`:

`astro dev` flags and subcommands.
### Health endpoint

Section titled “Health endpoint”The dev server exposes a `/_astro/status` endpoint that returns `{"ok": true}` as JSON. This allows agents and other tools to check programmatically whether the dev server is ready to accept requests. This endpoint is only available in the dev server and does not exist in production builds.

## Tips for AI-Powered Astro Development

Section titled “Tips for AI-Powered Astro Development”- **Start with templates**: Rather than building from scratch, ask AI tools to start with an existing Astro template or use- `npm create astro@latest`with a template option.
- **Use**: Ask AI tools to use- `astro add`for integrations- `astro add`for official integrations (e.g.- `astro add tailwind`,- `astro add react`). For other packages, install using the command for your preferred package manager rather than editing- `package.json`directly.
- **Verify current APIs**: AI tools may use outdated patterns. Ask them to check the latest documentation, especially for newer features like sessions and actions. This is also important for features that have seen significant changes since their initial launch, such as content collections, or previously experimental features that may no longer be experimental.
- **Use project rules**: If your AI tool supports it, set up project rules to enforce best practices and coding standards, such as the ones listed above.

# Citations

1. Source page: https://docs.astro.build/en/guides/build-with-ai
