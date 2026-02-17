---
description: Show a quick performance dashboard
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__get_performance_summary", "mcp__fly-agent__get_performance_comparison", "mcp__fly-agent__get_executive_kpi_summary", "mcp__fly-agent__get_workspace_performance", "mcp__fly-agent__get_location_performance_table"]
argument-hint: [workspace-name, location-name, or "all"]
---

Show a quick performance dashboard translating raw metrics into business outcomes — visibility growth, lead generation, and conversion efficiency.

**Data freshness**: Performance stats refresh daily for T to T-14 (~7 day Google reporting delay). Fly maintains temporal trends over time for contextual recommendations.

## Step 1: Establish Scope

**IMPORTANT — always ask the user to choose scope. Never assume or default without user confirmation.**

Check $ARGUMENTS first. If the user explicitly specified a workspace, location, or "all", use that. Otherwise:

### Step 1a: Choose Workspace
1. Call `mcp__fly-agent__list_workspaces` to get all workspaces
2. If multiple workspaces, ask which one. Also offer "all workspaces".
3. If only one workspace, confirm and proceed.

### Step 1b: Choose Locations
1. Call `mcp__fly-agent__list_locations` (filtered to selected workspace)
2. Ask: **"Which locations? Pick specific ones or say 'all'."** Default to all within the chosen workspace if user confirms.

Do NOT proceed until scope is confirmed.

## Step 2: Show Dashboard

**Single location:**
1. Call `mcp__fly-agent__get_performance_summary` for executive overview
2. Call `mcp__fly-agent__get_performance_comparison` with period "week" for trend

**Multiple locations within a workspace:**
1. Call `mcp__fly-agent__get_executive_kpi_summary` with period "30d" and compare_with "previous"
2. Call `mcp__fly-agent__get_location_performance_table` for per-location comparison

**All workspaces:**
1. Call `mcp__fly-agent__get_executive_kpi_summary` for overall KPIs
2. Call `mcp__fly-agent__get_workspace_performance` per workspace
3. Call `mcp__fly-agent__get_location_performance_table` for full comparison

Present dashboard with outcome-focused framing:

**Performance Verdict:**
- **Visibility**: X total impressions ([+/-]Y% vs. last period) — "How many people are discovering your business"
- **Leads Generated**: X total actions (calls + directions + website + bookings) — "Potential customers who took action"
- **Conversion Rate**: X% — "How efficiently you turn visibility into leads"
- **Top Metric Change**: Highlight the biggest positive or negative change — celebrate wins, flag concerns
- **Multi-location**: Rank by performance, highlight top performer to replicate and bottom performer to fix

**Health Verdict**: One sentence — "Your business is [growing/stable/declining] in local search with [strong/moderate/weak] lead conversion."

**Recommended Next Action**: The single most impactful action based on the data:
- Visibility declining → "Run `/seo-audit` to check profile health and `/rank-check` for ranking drops"
- High visibility but low conversion → "Improve profile quality — add photos, respond to reviews, publish offers with strong CTAs"
- Strong across the board → "Maintain momentum. Consider expanding keyword tracking or creating more content to compound growth"
