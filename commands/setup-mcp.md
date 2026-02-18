---
description: Connect the Fly Agent MCP server for this plugin
allowed-tools: Read, Write, Edit, Bash, AskUserQuestion
argument-hint: [api-key]
---

Set up the Fly Agent MCP connection so all plugin skills and commands can access Google Business Profile data. This writes the MCP server config to the user's main Claude settings, where it will be picked up on next restart.

## Step 0: Check if already connected

First, check if the `fly-agent` MCP is already available by looking for any `mcp__fly-agent__*` tools in the current session. If the tools exist and are working, tell the user:

"The Fly Agent MCP is already connected and working. No setup needed."

Then stop — no further action required.

## Step 1: Collect connection details

Ask the user for:

1. **API Key** — their Fly Agent API key
   - If $ARGUMENTS contains a value, use it as the API key
   - Otherwise ask: "Enter your Fly Agent API key (get one at https://www.fly-social.com/fly-app/settings?tab=api-keys)"

2. **MCP Server URL** (optional) — defaults to `https://fly-agent-main-681315111540.asia-south1.run.app/mcp/sse`
   - Ask: "Use the default Fly Agent server, or do you have a custom URL?"
   - Most users should use the default

## Step 2: Determine config location

Check which MCP config files exist, in order of preference:

1. `~/.claude/.mcp.json` — user-level Claude Code config
2. `.mcp.json` in the current project root — project-level config

Read whichever exists. If neither exists, create `~/.claude/.mcp.json`.

## Step 3: Write the MCP config

Merge the `fly-agent` server into the existing config (preserve any other MCP servers already configured):

```json
{
  "mcpServers": {
    "fly-agent": {
      "type": "sse",
      "url": "THE_URL_FROM_STEP_1",
      "headers": {
        "x-api-key": "THE_API_KEY_FROM_STEP_1"
      }
    }
  }
}
```

**Important**: If the file already has other `mcpServers` entries, preserve them — only add or update the `fly-agent` entry.

## Step 4: Confirm & next steps

Tell the user:

```
Fly Agent MCP configured successfully.

Server: [url]
Config: [file path where it was written]

Next steps:
1. Restart Claude Code for the MCP to connect
2. Run /setup-branding to configure your white-label identity
3. Run /daily-ops to start your first operational check
```

**Important**: The MCP will NOT connect until Claude Code is restarted. Make this clear to the user.
