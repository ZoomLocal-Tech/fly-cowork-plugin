---
description: Run weekly Local SEO operational routine
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__refresh_all_rankings", "mcp__fly-agent__get_local_rankings", "mcp__fly-agent__get_ranking_trends", "mcp__fly-agent__get_visibility_score", "mcp__fly-agent__get_review_sentiment", "mcp__fly-agent__get_performance_comparison", "mcp__fly-agent__get_performance_summary", "mcp__fly-agent__get_citation_health_report", "mcp__fly-agent__get_content_suggestions", "mcp__fly-agent__generate_post_content", "mcp__fly-agent__create_post_draft", "mcp__fly-agent__publish_post", "mcp__fly-agent__get_post_drafts", "mcp__fly-agent__get_workspace_performance", "mcp__fly-agent__get_workspace_rankings", "mcp__fly-agent__get_workspace_review_summary", "mcp__fly-agent__get_upcoming_holidays", "mcp__fly-agent__generate_report_pdf", "mcp__fly-agent__send_report_email", "mcp__fly-agent__bulk_refresh_rankings", "mcp__fly-agent__get_workspace_ranking_overview", "mcp__fly-agent__get_workspace_performance_comparison", "mcp__fly-agent__get_workspace_content_health"]
argument-hint: [workspace-name, location-name, or "all"]
---

Execute the weekly Local SEO operations routine. Covers ranking checks, sentiment analysis, content publishing, and performance snapshots — all tied to measurable business outcomes.

**Data freshness**: Weekly ops are best run after Monday when Fly's backend refreshes local rankings and search insights. Performance stats refresh daily (T to T-14). Fly injects all temporal trends and historical context — use this data to make contextual, data-driven recommendations.

**Outcome focus**: Every weekly check must connect to visibility, rank, leads, or brand strength. Present changes in business terms ("5 more calls this week" not just "+12% actions").

## Step 1: Establish Scope

**IMPORTANT — always ask the user to choose scope. Never assume or default without user confirmation.**

Check $ARGUMENTS first. If the user explicitly specified a workspace, location, or "all", use that. Otherwise follow this two-step selection:

### Step 1a: Choose Workspace
1. Call `mcp__fly-agent__list_workspaces` to get all workspaces
2. If the user has multiple workspaces, ask: **"Which workspace would you like to run weekly ops on?"** and list them. Also offer "all workspaces" as an option.
3. If the user has only one workspace, confirm it and proceed.

### Step 1b: Choose Locations
1. Call `mcp__fly-agent__list_locations` (filtered to the selected workspace)
2. Ask: **"Which locations within [workspace name]? You can pick specific locations or say 'all'."** Default to all locations within the chosen workspace if the user confirms.
3. If the user picks specific locations, note them for the remaining steps.

Do NOT proceed until both workspace and location scope are confirmed.

## Step 2: Ranking Refresh & Analysis

**Use aggregate tools** to refresh and analyze rankings across all locations in bulk:
1. Call `mcp__fly-agent__bulk_refresh_rankings` to trigger fresh rank scans across all workspace locations at once (async — scans run in background, batched 5 at a time)
2. Call `mcp__fly-agent__get_workspace_ranking_overview` to get per-location ranking data including keywords tracked, top-3 counts, first-page counts, visibility scores, trend direction, and top keywords — all in one call

For workspace-wide aggregates, also call `mcp__fly-agent__get_workspace_rankings`.

**Fallback**: For a single location, use `refresh_all_rankings` → `get_local_rankings` → `get_ranking_trends` → `get_visibility_score` individually.

Present an outcome-focused ranking summary:
- Keywords in top 3 (these capture ~70% of local clicks)
- Keywords improving (momentum building)
- Keywords declining (needs attention — each drop = fewer leads finding you)
- Visibility score change from last week
- **Business impact**: "X keywords in top 3 = strong local search presence" or "Y keywords dropped — this may reduce inbound calls/visits"

## Step 3: Sentiment Analysis

For each location in scope:
1. Call `mcp__fly-agent__get_review_sentiment` with days=7 for the past week's sentiment
2. Flag any locations with declining sentiment or negative spikes
3. Compare to 30-day trend

## Step 4: Performance Snapshot

**Use aggregate tool** to get performance across all locations in one call:
1. Call `mcp__fly-agent__get_workspace_performance_comparison` with period "week" — returns current vs previous period comparison for impressions, clicks, calls, and directions across all workspace locations
2. Highlight significant changes (>10% up or down) in any metric

For additional workspace-wide view, call `mcp__fly-agent__get_workspace_performance`.

**Fallback**: For a single location, use `get_performance_comparison` with period "week" individually.

## Step 5: Citation Health Check

For each location in scope:
1. Call `mcp__fly-agent__get_citation_health_report` for NAP consistency score
2. Flag any locations with scores below 80%

## Step 6: Content Planning & Publishing

**Use aggregate tool** to identify content gaps before generating:
1. Call `mcp__fly-agent__get_workspace_content_health` to see post activity, content gaps, and last-post dates across all locations — identifies which locations need content most urgently
2. Call `mcp__fly-agent__get_upcoming_holidays` with days_ahead=14 for timely content opportunities
3. For locations identified as needing content, call `mcp__fly-agent__get_content_suggestions` for strategic content ideas
4. Check `mcp__fly-agent__get_post_drafts` for any ready-to-publish drafts
5. Offer to generate and publish 1-2 posts per location using `generate_post_content` → `create_post_draft` → `publish_post`

## Step 7: Load Branding & Weekly Summary

Before presenting the summary, load the white-label branding config:
1. Read `${CLAUDE_PLUGIN_ROOT}/config/branding.json` (or workspace-specific variant `config/branding-{workspace-name}.json`)
2. If branding is configured, apply brand_name as the report header and footer_text as the sign-off
3. If no branding is configured, proceed without it but mention `/setup-branding` is available

Present a consolidated weekly report branded with the user's identity. Lead with outcomes:

**Weekly Scorecard:**
- **Visibility**: Visibility score X (trend: +/-Y from last week) — "Your local search presence is [growing/stable/declining]"
- **Rankings**: X keywords in top 3, Y improved, Z declined — "Top 3 rankings drive ~70% of local search clicks"
- **Leads this week**: Total actions (calls + directions + website clicks) vs. last week — "X more potential customers took action this week"
- **Conversion rate**: Actions/Impressions — "X% of people who see you are taking action"
- **Sentiment**: Score and direction — "Customer sentiment is [positive/mixed/concerning]"
- **Citation health**: NAP consistency % — "Consistent citations strengthen your local authority"
- **Content**: Posts published this week / target — "Regular posting keeps your profile active in search"

**Top 3 Actions for Next Week** (ranked by impact on visibility and leads):
1. [Most impactful action based on this week's data]
2. [Second most impactful]
3. [Third most impactful]

Always frame recommendations in terms of expected business impact: "Fixing X could increase Y by Z%."

## Step 8: Client Update (for agencies/freelancers)

Ask the user: **"Would you like to send a weekly report to your client?"**

If yes:
1. Read branding config: `${CLAUDE_PLUGIN_ROOT}/config/branding.json` (or workspace-specific `branding-{workspace-name}.json`)
2. Call `mcp__fly-agent__generate_report_pdf` with report_type "custom" to create a PDF of the weekly summary
3. Ask for the client's email address (or use a previously provided one)
4. Call `mcp__fly-agent__send_report_email` passing branding params from config:
   - `brand_name` from branding.json
   - `brand_color` from branding.json
   - `logo_url` from branding.json
   - `footer_text` from branding.json (or compose: "{brand_name} | {website_url} | {contact_email}")
5. Alternatively, present the summary in a copy-friendly format for email/chat/WhatsApp
