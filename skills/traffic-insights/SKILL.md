---
name: traffic-insights
description: >
  This skill should be used when the user asks about "search traffic",
  "keyword traffic", "what keywords drive traffic", "traffic trends",
  "branded vs transactional", "traffic distribution", "keyword performance",
  "traffic report", "search insights", or needs to analyze how customers
  find their business through Google Search.
metadata:
  version: 0.1.0
---

# Traffic Insights

Analyze search traffic data from Google Business Profile to understand how customers discover the business, which keywords drive traffic, and how search behavior trends over time.

## Multi-Location Awareness

1. Establish context with workspaces/locations
2. Traffic insights are per-location; loop through locations for multi-location analysis

## Workflow: Traffic Dashboard

1. **Summary** — call `mcp__fly-agent__get_traffic_insights` with months parameter (1, 3, 6, or 12) for total traffic, category breakdown, top 10 keywords, and basic trends
2. **Top keywords** — call `mcp__fly-agent__get_top_keywords` with limit (default 25, max 50) for highest-traffic keywords across all categories
3. **Distribution** — call `mcp__fly-agent__get_traffic_distribution` for volume bucket analysis (high/medium/low) and category percentages

Present as a dashboard showing total traffic, category pie chart, and top keywords table.

## Workflow: Category Analysis

Traffic is categorized into four types:

| Category | Description | Example |
|----------|-------------|---------|
| Branded | Searches including business name | "joe's pizza dallas" |
| Transactional | Searches with purchase intent | "pizza delivery near me" |
| Navigational | Searches for directions/location | "pizza shop on main street" |
| Informational | General research queries | "best pizza toppings" |

### View category detail
Call `mcp__fly-agent__get_traffic_by_category` with category ("branded", "transactional", "navigational", or "informational") for detailed keyword list within that category.

### Deep dive
Call `mcp__fly-agent__get_category_deep_dive` with category for:
- Total traffic and share of voice
- Monthly trend with growth rates
- Top keywords in category
- Category-specific recommendations

## Workflow: Trend Analysis

1. **Monthly trends** — call `mcp__fly-agent__get_monthly_trends` with months (1-12, default 6) for month-over-month traffic totals, growth rates, and category trends
2. **Keyword performance** — call `mcp__fly-agent__get_keyword_performance` to identify trending up, trending down, stable, and new keywords
3. **Period comparison** — call `mcp__fly-agent__compare_traffic_periods` with period1_months and period2_months to compare recent vs prior periods

## Workflow: Refresh Data

Call `mcp__fly-agent__refresh_traffic_insights` to fetch latest data from Google's Performance API. This takes 10-30 seconds. Only use when user explicitly asks to refresh — do not call automatically.

## Workflow: Export & Report

Call `mcp__fly-agent__export_traffic_report` with:
- `months`: time range to include
- `email_to`: optional email address for delivery

Generates comprehensive report with top 50 keywords.

## Data Freshness & Refresh Cadence

- **Search Insights** refresh **weekly every Monday** via Fly's backend.
- Calling `refresh_traffic_insights` triggers an on-demand fetch from Google's Performance API (takes 10-30 seconds). Only use when user explicitly asks to refresh.
- Traffic data typically has a 3-5 day reporting delay from Google.
- **Follow-up triggers**:
  - After Monday's weekly refresh → review for any new keyword opportunities or declining traffic signals
  - After significant traffic changes → cross-reference with ranking changes (`/rank-check`) and profile changes (`/seo-audit`)
  - Monthly → deep-dive into traffic trends as part of `/monthly-ops` and update content strategy based on shifting keyword patterns
  - New transactional keywords appearing → consider tracking them for rankings and creating targeted content

## Quantifiable Outcomes & KPIs

Every traffic view should connect search data to business growth:

| KPI | What to Show | Business Impact |
|-----|-------------|-----------------|
| Total Search Traffic | Impressions from all keyword categories | Overall measure of search visibility |
| Traffic Trend | Month-over-month growth rate | Shows whether visibility is expanding or contracting |
| Branded Traffic % | Share of branded vs. non-branded | High branded = strong awareness; low branded = opportunity to build brand |
| Transactional Traffic % | Share of high-intent keywords | These visitors are most likely to convert to leads |
| Top Keywords | Highest-traffic terms | Focus optimization and content on what drives real traffic |
| Trending Up Keywords | Growing search terms | Opportunities to capitalize on rising demand |
| Trending Down Keywords | Declining search terms | May need defensive action or indicate seasonal shift |
| New Keywords | Terms appearing for the first time | Emerging opportunities or new customer segments |

## Action-to-Outcome Funnel

After presenting traffic insights, always recommend actions that grow visibility and leads:

1. **Branded traffic declining** → "Brand awareness is weakening. Increase posting frequency (`/quick-post`), encourage more reviews, and ensure your business name is consistent across citations."
2. **Transactional traffic low** → "High-intent searchers aren't finding you. Optimize for transactional keywords in your profile description and posts. Consider tracking these keywords (`/rank-check`)."
3. **Transactional traffic high** → "Great buying intent. Make sure your conversion funnel is tight — phone number visible, website linked, direction button working. Check conversion rate via `/performance`."
4. **New keywords discovered** → "New search terms are leading people to your profile. Consider: Are these worth tracking? Should you create content targeting them?"
5. **Traffic declining overall** → "Search visibility is dropping. This could indicate: ranking drops, increased competition, or profile issues. Cross-check with `/rank-check` and `/seo-audit`."
6. **Traffic growing** → "Your optimization efforts are paying off. Document this growth in a client report (`/monthly-ops`) and continue the strategies that are working."
7. **Informational traffic high** → "People are researching in your space. Create educational content to capture these researchers early in their journey — they become customers later."

**Always end with a "Traffic Health Verdict"**: total traffic trend, category balance, top opportunity keyword, and the best action to grow qualified leads.

## Interpreting Traffic Data

- **High branded traffic**: strong brand awareness; focus on defending brand terms and converting brand searches to actions
- **High transactional traffic**: strong commercial intent; optimize conversion (phone, directions, website) — these are your best leads
- **Low informational traffic**: opportunity to create content targeting research-phase customers and build top-of-funnel awareness
- **Declining keywords**: may indicate seasonal changes, increased competition, or profile degradation — investigate promptly
- **New keywords appearing**: potential new market opportunities or shifting customer needs — evaluate and track the valuable ones
