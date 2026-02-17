---
name: performance-analytics
description: >
  This skill should be used when the user asks about "performance metrics",
  "how am I doing", "show my analytics", "KPI dashboard", "views and clicks",
  "compare performance", "regional breakdown", "mobile vs desktop",
  "executive summary", "business health", or needs any Google Business Profile
  performance data, trends, or analysis.
version: 0.1.0
---

# Performance & Analytics

Comprehensive GBP performance tracking, analysis, and reporting across single locations, multiple locations, and full workspaces.

## Multi-Location Awareness

1. Establish context with `mcp__fly-agent__list_workspaces` and `mcp__fly-agent__list_locations`
2. For workspace-wide metrics, use workspace-level tools (pass workspace_id)
3. For location comparison, use multi-location tools (pass location_ids list)
4. For single location, set context with `mcp__fly-agent__set_default_location`

**Important**: Google performance data has approximately a 7-day reporting delay. Always inform users that "current" period data actually ends ~7 days ago.

## Workflow: Performance Dashboard (Single Location)

1. **Quick summary** — call `mcp__fly-agent__get_performance_summary` for an executive overview with insights
2. **Detailed stats** — call `mcp__fly-agent__get_performance_stats` with days parameter (default 30) for views, searches, calls, directions, website clicks
3. **Device breakdown** — call `mcp__fly-agent__get_performance_breakdown` with metric "all" for mobile/desktop split across all fields
4. **Deep analytics** — call `mcp__fly-agent__get_performance_analytics` for device breakdown percentages, source analysis, action breakdown, best/worst days, day-of-week patterns

## Workflow: Performance Comparison

1. **Period comparison** — call `mcp__fly-agent__get_performance_comparison` with period "week", "month", or "quarter"
2. **Custom date range** — call `mcp__fly-agent__get_performance_breakdown` with start_date and end_date (YYYY-MM-DD format)
3. **Trend analysis** — call `mcp__fly-agent__get_performance_trends` with cadence "weekly" or "monthly" and periods count (default 4, max 12)

## Workflow: Chart Data

Call `mcp__fly-agent__get_performance_charts` with chart_type parameter:
- `mobile` — Mobile Search + Mobile Maps impressions
- `desktop` — Desktop Search + Desktop Maps impressions
- `actions` — Website Clicks, Phone Calls, Directions, Bookings
- `all` — All three chart types

Supports period: 7d, 30d, or 90d.

## Workflow: Multi-Location Performance

1. **Location comparison table** — call `mcp__fly-agent__get_location_performance_table` with workspace_id or location_ids list. Shows per-location: impressions, views, actions, conversion rate
2. **Workspace aggregate** — call `mcp__fly-agent__get_workspace_performance` with workspace_id
3. **Search by name** — use `location_search` parameter to find locations by name across any performance tool

## Workflow: Executive KPI Summary

Call `mcp__fly-agent__get_executive_kpi_summary` with:
- `period`: 7d, 30d, 90d, mtd, qtd, ytd
- `compare_with`: "previous" or "yoy" (year-over-year)

Returns: total visibility, customer engagement, conversion rate, review health, top/bottom performers.

## Workflow: Regional Performance

Call `mcp__fly-agent__get_regional_performance` with:
- `group_by`: "zone" (North/South/East/West/Central), "state", or "city"
- `period`: 7d, 30d, 90d

## Workflow: Specific Metric Focus

Use `mcp__fly-agent__get_performance_breakdown` with metric parameter:
- `impressions` — all impression data
- `actions` — all action data
- `search` — search impressions only
- `maps` — maps impressions only
- `calls` — phone calls only
- `website` — website clicks only
- `directions` — direction requests only

## Data Freshness & Refresh Cadence

- **Performance Stats** refresh **daily** for the window T to T-14 (today minus 14 days). The most recent ~7 days may have incomplete data due to Google's reporting delay.
- **Monthly Performance Reports** are generated on the **7th of each month** by Fly's backend.
- Always inform users: "Performance data has a ~7 day Google reporting delay. The most recent complete data is from approximately [date]."
- **Follow-up triggers**:
  - After a performance drop is detected → suggest auditing the profile (`/seo-audit`) and checking for unauthorized edits (`get_profile_protection_status`)
  - After a performance spike → identify what changed (new reviews? posts? rank improvement?) and recommend repeating that action
  - Weekly: compare week-over-week to catch trends early before they become monthly problems

## Quantifiable Outcomes & KPIs

Every performance view should translate metrics into business language:

| KPI | What to Show | Business Impact |
|-----|-------------|-----------------|
| Total Impressions | Views across search + maps | Raw visibility — how many people see your business |
| Impression Trend | Week/month change % | Shows whether visibility is growing or declining |
| Total Actions | Calls + website + directions + bookings | Direct lead indicators — people taking action |
| Conversion Rate | Actions / Impressions × 100 | Efficiency of turning views into leads |
| Calls | Phone call count + trend | Most direct lead type for service businesses |
| Direction Requests | Count + trend | Foot traffic indicator for retail/restaurant |
| Website Clicks | Count + trend | Digital lead funnel entry point |
| Mobile vs Desktop | Percentage split | Tells you where to focus UX optimization |
| Top/Bottom Performers | Best and worst locations | Where to allocate optimization effort |

## Action-to-Outcome Funnel

After presenting performance data, always recommend the next highest-impact action:

1. **Impressions declining** → "Visibility is dropping. Check your SEO score (`/seo-audit`) and rankings (`/rank-check`) — you may need profile optimization or fresh content."
2. **High impressions, low actions** → "People see you but don't engage. Improve your profile (photos, description, reviews) and add a call-to-action post (`/quick-post`)."
3. **Actions declining but impressions stable** → "Your profile may need refreshing — update photos, respond to recent reviews (`/respond-reviews`), and publish a new post."
4. **Strong growth across metrics** → "Great momentum. Document this in a client report (`/monthly-ops`) and double down on what's working."
5. **Specific location underperforming** → "This location needs attention. Start with an audit (`/seo-audit`) then check review sentiment and citations."
6. **Mobile impressions dominating** → "X% of your traffic is mobile. Ensure your website is mobile-optimized and your Google profile has a click-to-call button."
7. **Calls declining** → "Phone leads are dropping. Verify your phone number is correct, add a call CTA to your latest post, and check competitor activity."

**Always end with a "Performance Health Verdict"**: one sentence summarizing whether the business is growing, stable, or needs attention, plus the single most impactful next step.

## Output Formatting

Present performance data with:
- Clear metric labels and values with business-impact context
- Trend indicators (up/down arrows with percentages)
- Period context (e.g., "Last 30 days ending Feb 9 — note: data has ~7 day lag")
- Comparison to previous period with "better/worse/stable" verdict
- For multi-location: rank locations by performance, highlight top performers to replicate and underperformers to fix
- **Recommended Next Action** at the bottom of every dashboard
