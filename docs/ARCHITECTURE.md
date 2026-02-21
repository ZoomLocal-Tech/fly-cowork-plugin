# How It All Works

This document walks you through the full lifecycle — from first install to daily operations — and shows how skills, commands, tools, and self-service links connect at each stage.

## The Big Picture

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

## Step 1: One-Time Setup (~15 minutes)

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

## Step 2: Daily Operations (~10 minutes)

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

## Step 3: Weekly Operations (~30 minutes)

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

## Step 4: Monthly Operations (~60 minutes)

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

## On-Demand: Anytime Actions

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

## How Skills, Commands, and Tools Connect

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

## Multi-Location: How Scope Works

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
