# Local SEO Pro Plugin

Comprehensive Local SEO management suite powered by Fly Agent. Built for marketing agencies, freelancers, and multi-location brands who manage Google Business Profiles at scale.

## What It Does

This plugin gives you end-to-end Local SEO management through natural conversation. Ask Claude to audit your profile, respond to reviews, publish posts, track rankings, or generate reports — it handles the rest. Everything works across multiple workspaces and locations, with full white-label branding support.

**10 specialized skills** | **11 slash commands** | **2 autonomous agents** | **150+ MCP tools** | **16 self-service link types**

## How It All Works

This section walks you through the full lifecycle — from first install to daily operations — and shows how skills, commands, tools, and self-service links connect at each stage.

### The Big Picture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        YOUR WORKFLOW                                │
│                                                                     │
│   SETUP (one-time)                                                  │
│   /setup-mcp  →  /setup-branding  →  /seo-audit                    │
│       │               │                  │                          │
│       ▼               ▼                  ▼                          │
│   Connect MCP     Set your brand     Baseline audit                 │
│   server          identity           for all locations              │
│                                                                     │
│   DAILY RHYTHM                                                      │
│   /daily-ops  ─────────────────────────────────────────────────     │
│       │                                                             │
│       ├── Review new customer reviews → AI-generate replies         │
│       ├── Check profile protection → Enable if off                  │
│       └── Recover failed posts → Retry or alert                     │
│                                                                     │
│   WEEKLY RHYTHM                                                     │
│   /weekly-ops  ────────────────────────────────────────────────     │
│       │                                                             │
│       ├── Refresh keyword rankings → Track movement                 │
│       ├── Analyze review sentiment → Spot trends                    │
│       ├── Publish fresh content → Keep profile active               │
│       └── Compare performance → Week-over-week changes              │
│                                                                     │
│   MONTHLY RHYTHM                                                    │
│   /monthly-ops  ───────────────────────────────────────────────     │
│       │                                                             │
│       ├── Generate full reports → PDF + email to clients            │
│       ├── Re-audit all profiles → Catch drift                       │
│       ├── Analyze traffic trends → Where customers come from        │
│       └── Plan next month's content → Fill gaps                     │
│                                                                     │
│   ON-DEMAND (anytime)                                               │
│   /respond-reviews  /quick-post  /rank-check  /citation-scan       │
│   /performance      /seo-audit   "ask anything"                     │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Step 1: One-Time Setup (~15 minutes)

You only do this once. It connects the plugin to your Google Business Profile data and sets your brand identity.

```
/setup-mcp                              /setup-branding
    │                                        │
    ▼                                        ▼
Connect Fly Agent MCP server             Set agency name, logo,
(writes config to Claude settings)       colors, tagline, email
    │                                        │
    ▼                                        ▼
Plugin can now call 150+ tools           All reports and emails
to read/write your GBP data             carry your brand identity
```

**What happens under the hood:**
- `/setup-mcp` writes the MCP server config to your Claude settings file, giving the plugin access to all Fly Agent tools
- `/setup-branding` saves your agency's identity (name, logo, colors) so every report, PDF, and email goes out under your brand
- Both are slash commands that walk you through the process interactively

**After setup, run your first audit:**

```
/seo-audit
    │
    ├── Pulls your GBP profile data          ← get_gbp_profile
    ├── Scores SEO completeness              ← get_profile_audit, get_seo_score_breakdown
    ├── Checks category & service gaps       ← get_category_suggestions, get_available_services
    ├── Verifies profile protection          ← get_profile_protection_status
    │
    ▼
    Baseline scores + prioritized recommendations
    (what to fix first for maximum impact)
```

### Step 2: Daily Operations (~10 minutes)

Run `/daily-ops` every morning. It handles the three things that can't wait.

```
/daily-ops
    │
    ▼
┌─ REVIEWS ──────────────────────────────────────────────────┐
│  get_reviews_needing_reply → find unreplied reviews        │
│  generate_review_response  → AI writes tone-matched reply  │
│  post_selected_reply       → post after your approval      │
│                                                            │
│  Skills used: Review Command Center                        │
│  Outcome: reply rate up, reputation protected              │
└────────────────────────────────────────────────────────────┘
    │
    ▼
┌─ PROTECTION ───────────────────────────────────────────────┐
│  get_profile_protection_status → is monitoring active?     │
│  enable_profile_protection     → turn on if off            │
│                                                            │
│  Skills used: GBP Audit & Optimize                         │
│  Outcome: catch unauthorized edits before they hurt you    │
└────────────────────────────────────────────────────────────┘
    │
    ▼
┌─ FAILED POSTS ─────────────────────────────────────────────┐
│  get_failed_posts  → any scheduled posts that didn't go?   │
│  retry_failed_post → retry or alert you                    │
│                                                            │
│  Skills used: Content Engine                               │
│  Outcome: no silent content failures                       │
└────────────────────────────────────────────────────────────┘
```

### Step 3: Weekly Operations (~30 minutes)

Run `/weekly-ops` once a week. It covers the metrics that move on a weekly cycle.

```
/weekly-ops
    │
    ▼
┌─ RANKINGS ─────────────────────────────────────────────────┐
│  refresh_all_rankings  → scan all tracked keywords         │
│  get_local_rankings    → current positions on the map grid │
│  get_ranking_trends    → up, down, or steady?              │
│                                                            │
│  Skills used: Rank Tracker                                 │
│  Outcome: know exactly where you stand in local search     │
└────────────────────────────────────────────────────────────┘
    │
    ▼
┌─ SENTIMENT & PERFORMANCE ─────────────────────────────────┐
│  get_performance_comparison → week-over-week metrics       │
│  get_review_stats           → rating trends, volume        │
│                                                            │
│  Skills used: Performance & Analytics, Review Center       │
│  Outcome: spot problems before they become trends          │
└────────────────────────────────────────────────────────────┘
    │
    ▼
┌─ CONTENT ──────────────────────────────────────────────────┐
│  get_content_suggestions → what to post this week          │
│  generate_post_content   → AI writes the post              │
│  publish_post            → goes live on your GBP           │
│                                                            │
│  Skills used: Content Engine                               │
│  Outcome: consistent posting cadence (4-8 posts/month)     │
└────────────────────────────────────────────────────────────┘
```

### Step 4: Monthly Operations (~60 minutes)

Run `/monthly-ops` at the start of each month. This is your deep-dive review and client delivery step.

```
/monthly-ops
    │
    ▼
┌─ REPORTING ────────────────────────────────────────────────┐
│  generate_monthly_report → full month performance          │
│  compare_months          → month-over-month trends         │
│  generate_report_pdf     → white-labeled PDF               │
│  send_report_email       → email to client inbox           │
│                                                            │
│  Skills used: Reporting Hub                                │
│  Outcome: professional branded report in your client's     │
│  inbox, showing growth and ROI                             │
└────────────────────────────────────────────────────────────┘
    │
    ▼
┌─ RE-AUDIT ─────────────────────────────────────────────────┐
│  get_profile_audit       → has the score improved?         │
│  get_seo_score_breakdown → what's still missing?           │
│  compare_audit_scores    → before vs. after                │
│                                                            │
│  Skills used: GBP Audit & Optimize                         │
│  Outcome: measure optimization progress, catch drift       │
└────────────────────────────────────────────────────────────┘
    │
    ▼
┌─ TRAFFIC & CONTENT PLANNING ──────────────────────────────┐
│  get_traffic_insights    → how customers find you          │
│  get_content_gaps        → what's missing from your feed   │
│  get_keyword_performance → which searches drive traffic    │
│                                                            │
│  Skills used: Traffic Insights, Content Engine             │
│  Outcome: data-driven content plan for next month          │
└────────────────────────────────────────────────────────────┘
```

### On-Demand: Anytime Actions

These aren't part of a routine — use them whenever you need something specific.

```
┌───────────────────────────────────────────────────────────────────┐
│                                                                   │
│  QUICK ACTIONS (slash commands)                                   │
│  ──────────────────────────────                                   │
│  /respond-reviews  → handle a batch of new reviews right now      │
│  /quick-post       → write and publish a post in 2 minutes        │
│  /rank-check       → check a specific keyword position            │
│  /citation-scan    → find your listings across the web            │
│  /performance      → pull up a quick metrics dashboard            │
│  /seo-audit        → audit a specific location on demand          │
│                                                                   │
│  NATURAL LANGUAGE (skills activate automatically)                  │
│  ────────────────────────────────────────────────                  │
│  "Create a landing page for my business"     → Microsite Manager  │
│  "What keywords drive traffic to my profile?" → Traffic Insights  │
│  "Generate a PDF report for this month"       → Reporting Hub     │
│  "Set up auto-responder for reviews"          → Review Center     │
│  "Show me my subscription status"             → Workspace Ops     │
│  "Scan citations for NAP consistency"         → Citation Scanner  │
│                                                                   │
│  SELF-SERVICE LINKS (when you want to do it in the UI)            │
│  ─────────────────────────────────────────────                    │
│  "Give me a link to upload photos"            → Photos link       │
│  "I want to optimize my profile myself"       → Optimize link     │
│  "Send me a link to manage reviews"           → Review Responder  │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

### How Skills, Commands, and Tools Connect

Every action you take follows the same pattern — whether you use a slash command, ask naturally, or request a self-service link:

```
┌──────────────┐     ┌──────────────┐     ┌──────────────────┐
│  YOU type or  │     │  Skill or    │     │  MCP Tools       │
│  say something│ ──▶ │  Command     │ ──▶ │  (150+ actions)  │
│              │     │  activates   │     │                  │
│  /seo-audit  │     │  GBP Audit & │     │  get_gbp_profile │
│  "audit me"  │     │  Optimize    │     │  get_profile_audit│
│              │     │              │     │  get_seo_score...│
└──────────────┘     └──────────────┘     └──────────────────┘
                                                   │
                           ┌───────────────────────┤
                           │                       │
                           ▼                       ▼
                   ┌──────────────┐     ┌──────────────────┐
                   │  AI handles  │     │  Self-service     │
                   │  it directly │     │  link generated   │
                   │  (primary)   │     │  (fallback)       │
                   │              │     │                   │
                   │  Updates your│     │  Opens a mobile-  │
                   │  profile,    │     │  friendly UI for  │
                   │  posts reply,│     │  you to review    │
                   │  publishes   │     │  and do it        │
                   │  content     │     │  yourself         │
                   └──────────────┘     └──────────────────┘
```

**The rule is simple:**
1. The AI tries to do it directly using tools (fastest, fully automated)
2. If the action needs a UI (photo uploads, visual editing) or you want manual control, it generates a self-service link
3. You're always in control — say "do it" or "give me a link" at any point

### Multi-Location: How Scope Works

Every command starts by asking you to choose what to operate on. Nothing runs on "all" unless you say so.

```
Start any command
    │
    ▼
"Which workspace?"          ← list_workspaces
    │
    ├── Client A
    ├── Client B            ← you pick one (or "all")
    └── Client C
         │
         ▼
"Which locations?"          ← list_locations
    │
    ├── Location 1 - Mumbai
    ├── Location 2 - Delhi  ← you pick specific ones (or "all")
    └── Location 3 - Pune
         │
         ▼
Command runs on your selected scope
    │
    ├── Single location  → runs tools directly
    └── Multiple/All     → Workspace Orchestrator agent
                           handles it in bulk with
                           aggregate API calls
```

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

## Version

0.8.0

## Author

ZoomLocal Tech Private Limited
