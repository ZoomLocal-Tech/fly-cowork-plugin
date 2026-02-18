# Connectors

## How MCP configuration works

This plugin connects to the Fly Agent MCP server via environment variables. Claude Code expands `${VAR}` references in the plugin's `.mcp.json` at startup, so you just need to set two environment variables before launching Claude Code.

## Required Environment Variables

| Variable | Description | Where to Get It |
|----------|-------------|-----------------|
| `FLY_AGENT_URL` | Fly Agent MCP server URL | Your Fly dashboard — typically `https://fly-agent-main-681315111540.asia-south1.run.app/mcp/sse` |
| `FLY_AGENT_API_KEY` | Your Fly Agent API key | Generate at [fly-social.com/fly-app/settings?tab=api-keys](https://www.fly-social.com/fly-app/settings?tab=api-keys) |

### Setting the variables

**macOS / Linux** — add to your `~/.zshrc` or `~/.bashrc`:

```bash
export FLY_AGENT_URL="https://fly-agent-main-681315111540.asia-south1.run.app/mcp/sse"
export FLY_AGENT_API_KEY="your_api_key_here"
```

Then restart your terminal (or run `source ~/.zshrc`) before launching Claude Code.

**Windows** — set via System Environment Variables or PowerShell:

```powershell
[Environment]::SetEnvironmentVariable("FLY_AGENT_URL", "https://fly-agent-main-681315111540.asia-south1.run.app/mcp/sse", "User")
[Environment]::SetEnvironmentVariable("FLY_AGENT_API_KEY", "your_api_key_here", "User")
```

Then restart your terminal.

## About the Fly Agent MCP

This plugin is built around the Fly Agent MCP server, which provides comprehensive Google Business Profile management capabilities including:

- Profile management and optimization
- Review monitoring and response
- Performance analytics and reporting
- Local keyword rank tracking
- Citation management
- Content creation and publishing
- Microsite/landing page management
- Traffic insights and analysis
- Multi-workspace and multi-location support

## Setting Up the Fly Agent Connection

### Step 1: Create a Fly Account

Sign up at [fly-social.com/fly-app](https://www.fly-social.com/fly-app) if you don't have an account, then connect your Google Business Profile.

### Step 2: Get Your API Key

1. Go to **Settings > API Keys**: [fly-social.com/fly-app/settings?tab=api-keys](https://www.fly-social.com/fly-app/settings?tab=api-keys)
2. Click **Create New Key**
3. Copy and save your API key securely

### Step 3: Set Environment Variables

Add the two environment variables to your shell profile (see above), then restart your terminal and Claude Code.

The plugin's `.mcp.json` will automatically pick up your values — no manual file editing needed.

## Security Notes

- Your API key is stored as an environment variable, not in any committed file
- Never commit `.mcp.json` files containing real credentials to version control
- Rotate your API key periodically from the Settings page
- Each team member should use their own API key for proper access control
