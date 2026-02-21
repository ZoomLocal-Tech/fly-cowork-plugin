---
name: rank-tracker
description: >
  This skill should be used when the user asks about "keyword rankings",
  "how do I rank", "track keywords", "visibility score", "competitor rankings",
  "ranking trends", "add keyword", "remove keyword", "keyword suggestions",
  "run a rank scan", "refresh rankings", or needs local search ranking data.
version: 0.1.0
---

# Rank Tracker & Visibility

Keyword ranking management, on-demand scanning, competitor analysis, and visibility scoring for local search.

## Multi-Location Awareness

1. Establish context with workspaces/locations
2. For workspace-wide rankings, use `mcp__fly-agent__get_workspace_rankings`
3. Each location can track up to 5 keywords

## Workflow: Rankings Dashboard

1. **Current rankings** — call `mcp__fly-agent__get_local_rankings` to see where the business ranks for each tracked keyword
2. **Tracked keywords** — call `mcp__fly-agent__get_tracked_keywords` to list all monitored keywords
3. **Visibility score** — call `mcp__fly-agent__get_visibility_score` for an overall local search presence score
4. **Ranking trends** — call `mcp__fly-agent__get_ranking_trends` for 30-day position change history

Present as a dashboard: keyword, current position, trend direction, and visibility score.

## Workflow: Keyword Management

### Add a Keyword
1. Call `mcp__fly-agent__get_tracked_keywords` first to check current count (max 5 per location)
2. If under limit, call `mcp__fly-agent__add_keyword_to_track` with the keyword string and optional category
3. If at limit, suggest removing a less relevant keyword first

### Remove a Keyword
Call `mcp__fly-agent__remove_keyword_from_tracking` with the keyword name (not UUID). The tool auto-resolves the ID.

### Get Keyword Suggestions
Call `mcp__fly-agent__suggest_keywords` to get recommendations based on the business category. Present as a list the user can choose from.

## Workflow: On-Demand Rank Scan

**For a NEW keyword not yet tracked:**
Call `mcp__fly-agent__run_on_demand_scan` with:
- `keyword`: the keyword to scan
- `grid_size`: 1-5 (3 = 3x3 grid with 9 points, 5 = 5x5 with 25 points)
- `spacing`: distance between grid points in km (default 0.5)

**For refreshing ALL tracked keywords:**
Call `mcp__fly-agent__refresh_all_rankings` with:
- `grid_size`: 0=1x1, 1=3x3, 2=5x5
- This takes 30-120 seconds per keyword

**Important**: Only use `run_on_demand_scan` for new/untracked keywords or when user explicitly asks to "run a fresh scan". For viewing existing rankings, always use `get_local_rankings`.

## Workflow: Competitor Analysis

Call `mcp__fly-agent__get_competitor_analysis` with a keyword to see:
- Who else ranks for that keyword
- Their positions relative to the user's business
- Competitive landscape overview

## Workflow: Multi-Location Rankings

Call `mcp__fly-agent__get_workspace_rankings` for aggregated keyword performance across all locations. Identify which locations rank well and which need attention.

## Data Freshness & Refresh Cadence

- **Local Rankings** refresh **weekly every Monday** via Fly's backend automated scans.
- On-demand scans (`run_on_demand_scan`, `refresh_all_rankings`) provide real-time data but should be used intentionally (not excessively).
- After running a ranking refresh, note: "These are live positions as of now. The next automated refresh will occur Monday."
- **Follow-up triggers**:
  - After Monday's automated refresh → check for any significant position drops → investigate (profile changes? competitor activity? Google update?)
  - Keyword drops 3+ positions → alert user and suggest corrective action (audit, content, citation fixes)
  - Keyword enters top 3 → celebrate and suggest maintaining with consistent content + reviews
  - New keyword tracked → schedule a re-check after 7 days to establish a baseline trend

## Quantifiable Outcomes & KPIs

Every ranking view should translate positions into business impact:

| KPI | What to Show | Business Impact |
|-----|-------------|-----------------|
| Average Position | Mean rank across tracked keywords | Lower = better visibility in local pack |
| Top 3 Keywords | Count of keywords ranking #1-3 | Top 3 positions get ~70% of local search clicks |
| Visibility Score | Overall local presence score | Composite metric showing search dominance |
| Position Changes | Keywords up / down / stable | Shows optimization momentum |
| Competitor Position | Your rank vs. top competitor for each keyword | Identifies who you're competing against |
| Keywords Not Ranking | Tracked keywords with no ranking | Opportunities where you're invisible |

## Action-to-Outcome Funnel

After every ranking check, guide toward actions that improve positions:

1. **No keywords in top 3** → "You're missing the most valuable local search real estate. The top 3 positions capture ~70% of clicks. Focus on: profile optimization (`/seo-audit`), review velocity, and consistent posting."
2. **Keywords dropping** → "Rank drops mean fewer customers finding you. Check: Has your profile changed? Are competitors posting more? Has review velocity slowed?" → Run `/seo-audit` + `/respond-reviews`.
3. **Keywords improving** → "Your optimization is working. Keep the momentum with regular content (`/quick-post`) and maintain review response rate."
4. **High visibility score (70+)** → "Strong local presence. Convert this visibility into leads — check your conversion rate via `/performance` and optimize CTAs."
5. **Low visibility score (<40)** → "Low visibility means customers can't find you. Start with profile optimization (`/seo-audit`), boost review volume, and post consistently (`/quick-post`)."
6. **Competitor outranking you** → "Your competitor ranks higher for [keyword]. Analyze what they do differently — review count, post frequency, citation coverage — and close the gap."
7. **Keywords at limit (5/5)** → "You're tracking the maximum 5 keywords. Review which ones matter most — replace low-value keywords with higher-impact terms."

**Always end with a "Ranking Health Verdict"**: how many keywords are in winning positions, the trend direction, and the single best action to improve rank.

## Keyword Strategy Tips

When suggesting keywords, prioritize by lead-generation potential:
- **High-intent transactional keywords** (e.g., "plumber near me", "pizza delivery") — these directly generate leads
- **Service + Location** keywords (e.g., "plumber in Dallas") — capture local intent
- **Category keywords** matching the GBP primary category — align with Google's categorization
- **Branded keywords** — monitor brand visibility and protect against competitors bidding on your name
- **Long-tail keywords** with lower competition — easier wins that compound over time
- Balance between aspirational high-volume terms and immediately achievable niche terms
