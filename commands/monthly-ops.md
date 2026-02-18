---
description: Run monthly Local SEO review and reporting
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__generate_monthly_report", "mcp__fly-agent__get_monthly_summary", "mcp__fly-agent__generate_workspace_report", "mcp__fly-agent__compare_months", "mcp__fly-agent__generate_report_pdf", "mcp__fly-agent__send_report_email", "mcp__fly-agent__get_profile_audit", "mcp__fly-agent__get_seo_score_breakdown", "mcp__fly-agent__get_executive_kpi_summary", "mcp__fly-agent__get_regional_performance", "mcp__fly-agent__get_performance_trends", "mcp__fly-agent__get_traffic_insights", "mcp__fly-agent__get_keyword_performance", "mcp__fly-agent__get_monthly_trends", "mcp__fly-agent__get_content_gaps", "mcp__fly-agent__get_best_performing_content", "mcp__fly-agent__get_citation_health_report", "mcp__fly-agent__get_workspace_citations_overview", "mcp__fly-agent__get_location_performance_table", "mcp__fly-agent__refresh_traffic_insights", "mcp__fly-agent__get_workspace_seo_audit_summary", "mcp__fly-agent__get_workspace_traffic_overview", "mcp__fly-agent__bulk_refresh_traffic_insights", "mcp__fly-agent__get_workspace_content_health", "mcp__fly-agent__get_workspace_onboarding_status"]
argument-hint: [workspace-name, location-name, or "all"]
---

Execute the monthly Local SEO review. Comprehensive analysis that proves ROI and sets the strategy for the next month — covering visibility growth, lead generation, ranking progress, brand health, and actionable next steps.

**Data freshness**: Monthly reports and content strategy refresh on the **7th of each month** via Fly's backend. Best run after the 7th for complete data. Fly injects all temporal trends and historical context — use this rich dataset to make data-driven, outcome-focused recommendations.

**Outcome focus**: This is the ROI proof point for agencies and the strategic compass for brands. Every metric must be framed in business terms: more visibility, better rank, more leads, stronger brand recognition. End with a prioritized action plan for the coming month.

## Step 1: Establish Scope & Period

**IMPORTANT — always ask the user to choose scope. Never assume or default without user confirmation.**

Check $ARGUMENTS first. If the user explicitly specified a workspace, location, "all", or month/year, use that. Otherwise follow this selection:

### Step 1a: Choose Workspace
1. Call `mcp__fly-agent__list_workspaces` to get all workspaces
2. If the user has multiple workspaces, ask: **"Which workspace would you like the monthly report for?"** and list them. Also offer "all workspaces" as an option.
3. If the user has only one workspace, confirm it and proceed.

### Step 1b: Choose Locations
1. Call `mcp__fly-agent__list_locations` (filtered to the selected workspace)
2. Ask: **"Which locations within [workspace name]? You can pick specific locations or say 'all'."** Default to all locations within the chosen workspace if the user confirms.
3. If the user picks specific locations, note them for the remaining steps.

### Step 1c: Choose Period
If not specified in arguments, ask: **"Which month/year would you like the report for? (default: previous calendar month)"**

Do NOT proceed until workspace, locations, and period are all confirmed.

## Step 2: Executive KPI Summary

Call `mcp__fly-agent__get_executive_kpi_summary` with:
- `period`: "30d" (or "mtd" for month-to-date if mid-month)
- `compare_with`: "previous"

Present the high-level business health in outcome terms:
- **Visibility**: Total impressions + growth % — "Your business was seen X times this month, Y% [more/less] than last month"
- **Lead Generation**: Total actions + growth % — "X potential customers took action (called, visited website, requested directions)"
- **Conversion Efficiency**: Action-to-impression ratio — "Y% of people who saw you took action"
- **Brand Trust**: Average rating + review response rate — "Your Z-star rating with W% response rate builds customer confidence"
- **Top/Bottom Performers**: Best and worst locations by lead generation — focus optimization on underperformers

## Step 3: Full Monthly Reports

### Per-Location Reports
For each location in scope:
1. Call `mcp__fly-agent__generate_monthly_report` with month and year
2. Call `mcp__fly-agent__get_monthly_summary` for quick metrics

### Workspace Reports (if scope includes a full workspace)
For each workspace in scope:
1. Call `mcp__fly-agent__generate_workspace_report` with month and year

### Month-Over-Month Comparison
Call `mcp__fly-agent__compare_months` comparing current month to previous month.

## Step 4: SEO Re-Audit

**Use aggregate tool** to audit all locations at once:
1. Call `mcp__fly-agent__get_workspace_seo_audit_summary` — returns SEO scores, score distribution (excellent/good/fair/poor), and per-location audit details sorted by lowest score first, all in one call
2. Compare to last month's scores and flag improvements or regressions
3. Focus optimization recommendations on locations scoring "fair" or "poor"

**Fallback**: For a single location, use `get_profile_audit` → `get_seo_score_breakdown` individually.

## Step 5: Traffic Insights Refresh

**Use aggregate tools** to refresh and analyze traffic across all locations:
1. Call `mcp__fly-agent__bulk_refresh_traffic_insights` to pull latest Google data for all workspace locations at once (batched 10 at a time)
2. Call `mcp__fly-agent__get_workspace_traffic_overview` with months=1 — returns search traffic, maps traffic, and top keywords per location in one call
3. For locations with notable traffic changes, drill into `mcp__fly-agent__get_monthly_trends` and `mcp__fly-agent__get_keyword_performance` for detailed analysis

**Fallback**: For a single location, use `refresh_traffic_insights` → `get_traffic_insights` → `get_monthly_trends` → `get_keyword_performance` individually.

## Step 6: Multi-Location Comparison (if scope includes multiple locations)

1. Call `mcp__fly-agent__get_location_performance_table` with workspace_id and period "30d"
2. Call `mcp__fly-agent__get_regional_performance` with group_by "zone" or "city"
3. Identify top and bottom performing locations

## Step 7: Content Review

**Use aggregate tool** to review content health across all locations:
1. Call `mcp__fly-agent__get_workspace_content_health` with days=90 — returns posts published, content gaps, last-post dates, and post-type breakdowns per location in one call
2. Identify locations with no recent posts or content gaps
3. Recommend content focus areas for next month, prioritizing locations with the least recent activity

**Fallback**: For a single location, use `get_best_performing_content` → `get_content_gaps` individually.

## Step 8: Citation Health

1. Per-location in scope: call `mcp__fly-agent__get_citation_health_report`
2. Workspace-wide (if applicable): call `mcp__fly-agent__get_workspace_citations_overview`
3. Flag any NAP consistency issues

## Step 9: Report Delivery

1. Ask user which reports to generate as PDF
2. Call `mcp__fly-agent__generate_report_pdf` for each selected report
3. Optionally call `mcp__fly-agent__send_report_email` to deliver to stakeholders

## Step 10: Load Branding & Monthly Summary

Before presenting the summary, load the white-label branding config:
1. Read `${CLAUDE_PLUGIN_ROOT}/config/branding.json` (or workspace-specific variant `config/branding-{workspace-name}.json`)
2. If branding is configured, apply brand_name as the report header, logo reference, brand_color for accents, and footer_text as the sign-off
3. If no branding is configured, proceed without it but mention `/setup-branding` is available

Present a comprehensive monthly summary branded with the user's identity. Structure as an ROI-focused business review:

**Monthly Business Impact Summary:**
- **Visibility Growth**: Impression change % — "Your search visibility [grew/declined] by X% this month"
- **Lead Generation**: Total customer actions + change — "X leads generated (calls, direction requests, website clicks), Y% change from last month"
- **Ranking Progress**: Keywords in top 3, positions gained/lost — "You now rank in the top 3 for X keywords, capturing the majority of local clicks"
- **Brand Health**: Rating trend + review volume + reply rate — "X.X star rating with Y new reviews and Z% reply rate"
- **Traffic Insights**: Top traffic keywords + new opportunities — "Transactional traffic [grew/declined] by X%, indicating [stronger/weaker] purchase intent"
- **Profile Strength**: SEO score change — "Profile SEO score: X/100 (change from last month)"
- **Citation Authority**: NAP consistency + new citations — "X consistent citations across Y directories"
- **Content Activity**: Posts published + engagement — "X posts published, generating Y views and Z actions"

**Month-Over-Month ROI Narrative**: One paragraph summarizing the cumulative impact of all optimizations: "This month's efforts resulted in X% more visibility and Y% more customer actions. Key wins: [specific improvements]. Areas to focus next month: [specific opportunities]."

**Priority Action Plan for Next Month** (top 5 actions ranked by expected impact):
1. [Highest impact action with expected outcome]
2. [Second action with expected outcome]
3. [Third action]
4. [Fourth action]
5. [Fifth action]

Include report links and delivery confirmation.

## Step 11: Client Delivery (for agencies/freelancers)

Ask the user: **"Would you like to email the monthly report to your client?"**

If yes:
1. Ensure PDFs have been generated in Step 9 (if not, generate them now)
2. Ask for the client's email address (or use a previously provided one)
3. Call `mcp__fly-agent__send_report_email` with report_type "monthly", the month/year, and client email
4. Confirm delivery and provide a copy of what was sent
