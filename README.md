# Local SEO Pro Plugin

Comprehensive Local SEO management suite powered by Fly Agent. Built for marketing agencies, freelancers, and multi-location brands who manage Google Business Profiles at scale.

## What It Does

This plugin provides end-to-end Local SEO workflows through 10 specialized skills, 10 slash commands, and 2 autonomous agents — all designed to work across multiple workspaces and locations, with full white-label branding support.

## Installation

In your terminal, run:

```bash
claude plugin marketplace add https://github.com/ZoomLocal-Tech/fly-cowork-plugin.git
claude plugin install fly-cowork-plugin@zoomlocal-marketplace
```

## Quick Setup

1. Get your API key from [fly-social.com/fly-app/settings?tab=api-keys](https://www.fly-social.com/fly-app/settings?tab=api-keys)
2. Customize the plugin — you'll be asked for your MCP server URL and API key (see [CONNECTORS.md](CONNECTORS.md) for full details)
3. Run `/setup-branding` to configure your white-label identity (name, logo, colors, footer)
4. Run `/daily-ops` to start your first operational check

## Components

### Skills (10)

| Skill | Trigger Phrases | What It Does |
|-------|----------------|--------------|
| **GBP Audit & Optimize** | "audit my profile", "optimize my GBP", "check SEO score" | Full profile audit, SEO scoring, optimization, competitor analysis |
| **Review Command Center** | "manage reviews", "respond to reviews", "review sentiment" | Review response, sentiment analysis, auto-responder setup, QR codes |
| **Performance & Analytics** | "show my analytics", "KPI dashboard", "compare performance" | Performance tracking, device/source breakdowns, regional analysis |
| **Rank Tracker** | "keyword rankings", "visibility score", "track keywords" | Keyword management, rank scanning, competitor analysis |
| **Citation Scanner** | "scan citations", "NAP consistency", "directory listings" | Citation discovery, NAP auditing, opportunity identification |
| **Content Engine** | "create a post", "content calendar", "trending topics" | Content ideation, creation, scheduling, publishing |
| **Microsite Manager** | "create microsite", "landing page", "store locator" | Microsite creation, theming, sections, custom domains, analytics |
| **Traffic Insights** | "search traffic", "keyword traffic", "traffic trends" | Search traffic analysis, category breakdowns, keyword performance |
| **Reporting Hub** | "monthly report", "PDF report", "email report" | Report generation, PDF export, email delivery, white-labeled |
| **Workspace & Account Ops** | "switch workspace", "list locations", "subscription" | Multi-workspace navigation, account management, branding setup |

### Commands (10)

| Command | Description |
|---------|-------------|
| `/setup-branding` | Configure white-label branding (name, logo, colors) for all reports and emails |
| `/daily-ops` | Run daily operational checks: reviews, protection alerts, failed posts |
| `/weekly-ops` | Weekly routine: rankings refresh, sentiment, content, performance |
| `/monthly-ops` | Monthly review: full reports, re-audit, traffic, content gaps |
| `/seo-audit` | Quick SEO audit on one or all locations |
| `/respond-reviews` | Batch-respond to all unreplied reviews |
| `/rank-check` | Check keyword rankings or scan a new keyword |
| `/citation-scan` | Run a full citation discovery scan |
| `/quick-post` | Generate and publish a GBP post |
| `/performance` | Quick performance dashboard |

### Agents (2)

| Agent | When It's Used |
|-------|---------------|
| **Workspace Orchestrator** | Bulk operations across multiple workspaces/locations (audits, reports, comparisons) |
| **Review Responder** | Systematic batch review response with tone-appropriate replies |

### MCP Integration

This plugin connects to the Fly Agent MCP server for Google Business Profile management. Authentication is configured during plugin customization — your API key and MCP server URL are stored in the plugin's `.mcp.json`. See `CONNECTORS.md` for full setup instructions and manual MCP setup if needed.

## White-Label Branding

All reports, emails, and generated summaries can carry your brand identity instead of Fly's. Run `/setup-branding` to configure:

- **Brand / Agency Name** — appears on all report headers and email subjects
- **Logo URL** — included in PDF report headers and email templates
- **Website & Contact Email** — shown in footers and used as reply-to identity
- **Brand Color** — applied to report accents and chart elements
- **Tagline & Footer Text** — custom sign-off for all client-facing output

For agencies managing multiple clients, per-workspace branding is supported — each client workspace can have its own branding config, so reports go out under the right identity.

## Who Is This For?

### Marketing Agencies
- Manage multiple client brands from a single interface
- Run daily/weekly/monthly ops across all clients efficiently
- Generate and deliver white-labeled reports per client
- Workspace-per-client organization with per-client branding

### Freelancers & Consultants
- Streamlined workflows for a handful of clients
- Quick-action commands for common tasks
- Automated operational routines to save time
- Professional branded reporting to demonstrate value

### Multi-Location Brands
- Cross-location performance comparison
- Regional analysis (zone, state, city breakdowns)
- Consistent brand management across all locations
- Store locator and microsite management at scale

## Daily/Weekly/Monthly Routine

The operational commands are designed to be your rhythm:

- **Every day**: `/daily-ops` — respond to reviews, check alerts, recover failed posts (~10 min)
- **Every week**: `/weekly-ops` — refresh rankings, check sentiment, publish content, review performance (~30 min)
- **Every month**: `/monthly-ops` — full reporting, re-audit, traffic analysis, content planning (~60 min)

All ops commands include an optional client delivery step — generate a branded PDF and email it directly to your client at the end of each routine.

## Scope Selection

Every command asks you to choose scope before proceeding:

1. **Choose workspace** — which client/brand to operate on
2. **Choose locations** — which locations within that workspace (specific or all)

Nothing runs on "all" unless you explicitly say so. This keeps operations safe and intentional for multi-client setups.

## Version

0.6.0

## Author

ZoomLocal Tech Private Limited
