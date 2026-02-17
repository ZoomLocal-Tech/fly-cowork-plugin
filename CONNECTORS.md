# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user
connects in that category. Plugins are tool-agnostic — they describe
workflows in terms of categories rather than specific products.

## Connectors for this plugin

| Category | Placeholder | Included servers | Other options |
|----------|-------------|-----------------|---------------|
| Local SEO Platform | `~~local-seo-platform` | Fly Agent (fly-social.com) | Any MCP-compatible GBP management platform |

## Customization Points

During plugin customization, the user will be asked to provide:

| Placeholder | Description | Where to Get It |
|-------------|-------------|-----------------|
| `~~local-seo-platform` | Fly Agent MCP server URL | Fly dashboard or API key settings page |
| `~~fly-agent-api-key` | Your Fly Agent API key for authenticating MCP requests | Generate at [fly-social.com/fly-app/settings?tab=api-keys](https://www.fly-social.com/fly-app/settings?tab=api-keys) |

Both values are configured in the plugin's `.mcp.json` file during customization — no environment variables needed.

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
3. Copy and save your API key securely — you'll need it during plugin customization

### Step 3: Customize the Plugin

Run the plugin customizer in Cowork. You'll be asked to provide:

1. **MCP Server URL** — your Fly Agent MCP endpoint (provided in your Fly dashboard)
2. **API Key** — the key you generated in Step 2

The customizer will inject both values into the plugin's `.mcp.json` automatically.

## Security Notes

- Your API key is stored in the plugin's local `.mcp.json` config file
- Never share your plugin config file publicly or commit it to version control
- Rotate your API key periodically from the Settings page
- Each team member should use their own API key for proper access control
