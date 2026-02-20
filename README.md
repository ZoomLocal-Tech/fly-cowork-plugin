# Local SEO Pro Plugin

Comprehensive Local SEO management suite powered by Fly Agent. Built for marketing agencies, freelancers, and multi-location brands who manage Google Business Profiles at scale.

## What It Does

This plugin gives you end-to-end Local SEO management through natural conversation. Ask Claude to audit your profile, respond to reviews, publish posts, track rankings, or generate reports — it handles the rest. Everything works across multiple workspaces and locations, with full white-label branding support.

**10 specialized skills** | **11 slash commands** | **2 autonomous agents** | **150+ MCP tools** | **16 self-service link types**

## Installation

In your terminal, run:

```bash
claude plugin marketplace add https://github.com/ZoomLocal-Tech/fly-cowork-plugin.git
claude plugin install fly-cowork-plugin@zoomlocal-marketplace
```

## Quick Setup

1. Get your API key from [fly-social.com/fly-app/settings?tab=api-keys](https://www.fly-social.com/fly-app/settings?tab=api-keys)
2. Run `/setup-mcp` to connect the Fly Agent MCP server (or configure it during plugin customization)
3. Restart Claude Code, then run `/setup-branding` to configure your white-label identity
4. Run `/daily-ops` to start your first operational check

If you already have the `fly-agent` MCP configured in your Claude settings, skip step 2 — the plugin will use it automatically.

## Skills (10)

Skills activate automatically when you ask naturally. No need to memorize commands — just describe what you want.

### GBP Audit & Optimize
> Try: "audit my profile", "optimize my GBP", "check SEO score"

- Run a full profile audit with SEO scoring
- Get AI-generated business descriptions optimized for local search
- Update categories and services using Google's validated taxonomy
- Enable profile protection against unauthorized edits
- Compare before/after audit scores to measure improvement

### Review Command Center
> Try: "manage reviews", "respond to reviews", "review sentiment"

- Respond to all unreplied reviews in bulk with tone-appropriate AI replies (friendly for 5-star, apologetic for 1-star)
- Set up an auto-responder for hands-free 100% reply rate
- Generate QR codes and review collection links to get more reviews
- Track review sentiment trends over time

### Performance & Analytics
> Try: "show my analytics", "KPI dashboard", "compare performance"

- See views, clicks, calls, and direction requests across all locations
- Compare performance across time periods (week-over-week, month-over-month)
- Get executive KPI summaries for quick decision-making
- Break down metrics by device type, source, and region

### Rank Tracker
> Try: "keyword rankings", "visibility score", "track keywords"

- Track up to 5 keywords per location with grid-based map positioning
- Run on-demand rank scans to see where you appear right now
- See ranking trends over time to measure SEO progress
- Analyze competitor positions for your target keywords
- Get a visibility score summarizing your local search presence

### Citation Scanner
> Try: "scan citations", "NAP consistency", "directory listings"

- Discover your business listings across online directories
- Audit NAP (Name, Address, Phone) consistency across all citations
- Identify missing citation opportunities on high-authority directories
- Get a prioritized fix list with health scores

### Content Engine
> Try: "create a post", "content calendar", "trending topics"

- Generate post ideas from trending topics and upcoming holidays
- Create posts with AI-written copy tailored to your business
- Schedule or publish immediately to Google Business Profile
- Manage drafts and track which content performs best
- Identify content gaps and plan your posting cadence

### Microsite Manager
> Try: "create microsite", "landing page", "store locator"

- Build a branded landing page or multi-location store locator in minutes
- Choose from templates and customize theme, colors, and fonts
- Manage page sections (hero, services, reviews, map, and more)
- Set up a custom domain for a professional URL
- Track visitor analytics to measure page performance

### Traffic Insights
> Try: "search traffic", "keyword traffic", "traffic trends"

- Understand how customers find you on Google Search and Maps
- See traffic by category: branded, transactional, navigational, informational
- Track individual keyword performance and growth rates
- Compare traffic across periods to spot trends
- Identify growing and declining search terms

### Reporting Hub
> Try: "monthly report", "PDF report", "email report"

- Generate monthly performance reports with key metrics and trends
- Compare month-over-month to highlight growth and areas needing attention
- Export as white-labeled PDFs with your agency's branding
- Email reports directly to clients from within Claude

### Workspace & Account Ops
> Try: "switch workspace", "list locations", "subscription"

- Navigate between client workspaces and locations
- Check account details and subscription status
- Track onboarding progress for new locations
- Generate self-service links for any action
- Upload photos and brand reference images

## Commands (11)

Slash commands are quick shortcuts for common workflows. Type them directly to jump into action.

### Setup
- **`/setup-mcp`** — Connect the Fly Agent MCP server to your Claude settings. Required for all other commands to work.
- **`/setup-branding`** — Configure your agency's white-label identity (name, logo, colors, tagline) used in all reports and emails.

### Operational Routines
- **`/daily-ops`** — Daily check (~10 min): respond to new reviews, verify profile protection is active, recover any failed posts.
- **`/weekly-ops`** — Weekly routine (~30 min): refresh keyword rankings, check review sentiment trends, publish fresh content, compare performance week-over-week.
- **`/monthly-ops`** — Monthly review (~60 min): generate full reports with month-over-month comparisons, re-audit all profiles, analyze traffic trends, plan next month's content.

### On-Demand Actions
- **`/seo-audit`** — Run a quick SEO audit on one or all locations. Get a completeness score, category & service gap analysis, and prioritized optimization recommendations.
- **`/respond-reviews`** — Batch-respond to all unreplied reviews across selected locations with AI-generated, tone-appropriate replies. Review and approve before posting.
- **`/rank-check`** — Check current keyword rankings or scan a new keyword. See your position on the local map grid and track changes over time.
- **`/citation-scan`** — Run a full citation discovery scan. Find where your business is listed, check NAP accuracy, and identify directories where you're missing.
- **`/quick-post`** — Generate and publish a GBP post in minutes. Provide a topic or get AI suggestions, review the copy, then publish to one or all locations.
- **`/performance`** — Quick performance dashboard showing views, clicks, calls, and direction requests with period-over-period comparison.

## Agents (2)

Autonomous agents handle complex multi-step workflows that span multiple locations.

### Workspace Orchestrator
Bulk operations across all your locations in a single pass:
- Run audits on every profile at once
- Compare performance across locations to find top and bottom performers
- Generate workspace-wide reports and email them to clients
- Refresh rankings and traffic insights everywhere
- Uses workspace-level aggregate API calls — 50 locations take one call, not 50

### Review Responder
Systematic review response across all locations:
- Prioritizes negative reviews first so urgent issues get handled quickly
- Generates tone-appropriate replies (apologetic for 1-star, professional for 3-star, friendly for 5-star)
- Presents all responses for your approval before posting — nothing goes out without your OK
- Reports on reply rate improvement and rating impact when done

## Self-Service Links (16 types)

Every workflow follows an "automation first" approach — the AI handles things directly when possible. But when you want to review something yourself or the action needs a UI (like uploading photos), you can request a mobile-friendly self-service link.

| Link Type | What it opens |
|-----------|--------------|
| **Onboarding** | Guided setup wizard for new locations |
| **Optimize** | Step-by-step profile optimization (categories, services, hours, attributes) |
| **Review Generator** | Shareable link for collecting customer reviews |
| **Review Responder** | UI for reviewing and responding to customer reviews |
| **New Post** | Create and publish a GBP post with AI content suggestions |
| **Templates** | Browse and apply post templates |
| **Content Ideas** | Get AI-generated content ideas and plan posts |
| **Photos** | Upload and manage GBP photos |
| **Reference Images** | Upload brand reference images for AI-generated visuals |
| **Services** | Add or edit services listed on your profile |
| **Attributes** | Set business attributes (Wi-Fi, accessibility, seating, etc.) |
| **Microsite** | Edit your landing page or store locator |
| **Custom Domain** | Set up a custom domain for your microsite |
| **Dashboard** | View your location's performance dashboard |
| **Credits Purchase** | Buy additional credits for AI features |
| **Account** | Manage account settings and connected Google account |

Say "give me a link to..." followed by any of these to get a shareable URL you can open on any device.

## MCP Tools (150+)

The plugin connects to the Fly Agent MCP server, which exposes 150+ tools organized into these categories:

| Category | Example tools | What they let you do |
|----------|--------------|---------------------|
| **Profile Management** | `get_gbp_profile`, `update_profile_field`, `get_profile_audit` | Read and update any field on your Google Business Profile |
| **Category & Service Validation** | `get_category_suggestions`, `update_profile_categories`, `get_available_services`, `update_services` | Update categories and services using Google's validated taxonomy — no more failed updates from invalid values |
| **Review Operations** | `get_reviews_needing_reply`, `generate_review_response`, `post_selected_reply`, `setup_review_responder` | Fetch unreplied reviews, generate AI responses, post replies, configure auto-responders |
| **Content & Publishing** | `generate_post_content`, `create_post_draft`, `publish_post`, `schedule_post` | Create, draft, schedule, and publish GBP posts |
| **Rankings & Visibility** | `get_local_rankings`, `run_on_demand_scan`, `get_visibility_score`, `suggest_keywords` | Track keyword positions, run scans, monitor visibility trends |
| **Performance & Traffic** | `get_performance_summary`, `get_traffic_insights`, `get_keyword_performance` | Access views, clicks, calls, traffic sources, and keyword performance data |
| **Microsites** | `generate_microsite`, `set_theme`, `update_hero`, `setup_custom_domain` | Build landing pages, customize themes, manage sections, set up domains |
| **Reporting** | `generate_monthly_report`, `generate_report_pdf`, `send_report_email` | Generate, export, and email white-labeled reports |
| **Citations** | `run_citation_scan`, `get_citation_health_report`, `get_all_citations` | Discover, audit, and manage directory listings |
| **Workspace Aggregates** | `get_workspace_summary`, `get_workspace_review_summary`, `bulk_refresh_rankings` | Workspace-wide operations in a single API call |
| **Shareable Links** | `generate_shareable_link`, `get_available_links` | Generate mobile-friendly self-service links for 16 action types |
| **Protection & Setup** | `enable_profile_protection`, `get_setup_progress`, `create_onboarding_link` | Monitor profile changes, track setup completion, generate onboarding links |

Run `/setup-mcp` to configure the connection, or if you already have `fly-agent` in your Claude MCP settings, the plugin uses it automatically. See `CONNECTORS.md` for details.

## White-Label Branding

All reports, emails, and generated summaries carry your brand identity instead of Fly's. Run `/setup-branding` to configure:

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

0.8.0

## Author

ZoomLocal Tech Private Limited
