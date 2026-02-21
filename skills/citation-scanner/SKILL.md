---
name: citation-scanner
description: >
  This skill should be used when the user asks to "scan citations",
  "check my listings", "find my business on directories", "NAP consistency",
  "citation health", "add a citation", "citation opportunities",
  "directory listings", or needs help managing business citations
  across online directories.
metadata:
  version: 0.1.0
---

# Citation Scanner & Builder

Discover, audit, and manage business listings across online directories. Ensure NAP (Name, Address, Phone) consistency for local SEO.

## Multi-Location Awareness

1. Establish context with workspaces/locations
2. For workspace-wide citation health, use `mcp__fly-agent__get_workspace_citations_overview`
3. Run scans per location

## Workflow: Citation Health Check

1. **Health report** — call `mcp__fly-agent__get_citation_health_report` for total citations found, NAP consistency score, citations needing attention, and opportunities
2. **All citations** — call `mcp__fly-agent__get_all_citations` for full list with directory name, status, NAP accuracy, claimed/verified status
3. **Needing updates** — call `mcp__fly-agent__get_citations_needing_updates` for listings with NAP inconsistencies
4. **Priority actions** — call `mcp__fly-agent__get_priority_citation_actions` for ordered action items by impact

Present as a health scorecard with consistency score, total listings, and top priorities.

## Workflow: Full Citation Scan

This is a multi-step process:

1. **Start scan** — call `mcp__fly-agent__run_citation_scan` to get business details and search queries
2. **Execute searches** — run ALL returned search queries in parallel using web search to find the business on major directories
3. **Save discoveries** — for EACH listing found, call `mcp__fly-agent__save_discovered_citation` with:
   - `directory_name` and `directory_domain`
   - `found_name`, `found_address`, `found_phone`, `found_website` (as shown on the directory)
   - `listing_url` (direct link to the listing)
   - `is_claimed` (whether it appears claimed)
   - `notes` (any observations)
   The tool automatically calculates NAP match scores
4. **Complete scan** — call `mcp__fly-agent__complete_citation_scan` to record in history and generate summary
5. **Show results** — call `mcp__fly-agent__get_citation_health_report` to display updated health

## Workflow: Add/Update Citations Manually

### Add a citation
Call `mcp__fly-agent__add_citation` with:
- `directory_name`: "Yelp", "Justdial", etc.
- `directory_domain`: "yelp.com", "justdial.com", etc.
- `listing_url`: direct URL to the listing
- `status`: "found", "claimed", "verified", or "needs_update"

### Update a citation
Call `mcp__fly-agent__update_citation` with:
- `citation_id`: UUID of the citation
- `status`: new status
- `is_claimed`, `is_verified`: boolean flags
- `notes`: additional context

## Workflow: Find Citation Opportunities

1. Call `mcp__fly-agent__get_business_context_for_citations` to get business details and existing citations
2. Use web search to find relevant directories for the business category and location:
   - Search "best business directories for [category] in [city/country]"
   - Search "[business name] [city]" to find existing unlisted citations
   - Check industry-specific directories
3. Present opportunities as a prioritized list with directory name, estimated impact, and action to take

## Workflow: Multi-Location Citation Overview

Call `mcp__fly-agent__get_workspace_citations_overview` for aggregate citation health across all locations. Identify locations with lowest consistency scores for priority attention.

## Data Freshness & Refresh Cadence

- Citations are **not auto-refreshed** by Fly's backend — they require on-demand scanning.
- NAP consistency data is captured at scan time and remains static until the next scan.
- **Recommended cadence**: Run a full citation scan monthly (align with `/monthly-ops`) to catch new listings, removed listings, and NAP drift.
- After fixing a citation on an external directory, update its status in Fly using `update_citation` and re-scan in 2-4 weeks to verify the correction propagated.
- **Follow-up triggers**:
  - NAP consistency below 80% → prioritize fixing inconsistent listings before any other SEO work (inconsistent NAP confuses Google and hurts rankings)
  - New citations discovered → claim and verify them to strengthen the citation profile
  - Competitor has more citations → find which directories they're on that you're not and submit listings

## Quantifiable Outcomes & KPIs

Every citation operation should connect to measurable SEO impact:

| KPI | What to Show | Business Impact |
|-----|-------------|-----------------|
| Total Citations | Number of directory listings found | More consistent citations = stronger local authority signals |
| NAP Consistency Score | % of listings with matching name, address, phone | Inconsistent NAP directly hurts local rankings |
| Citations Claimed/Verified | Count of owned listings | Claimed listings give you control over your brand presence |
| Citations Needing Updates | Count with incorrect info | Each incorrect listing is actively confusing Google |
| New Opportunities | Directories where you're not listed | Each new quality citation can incrementally boost rank |
| Competitor Citation Gap | Directories they have, you don't | Closing this gap helps you compete in local pack |

## Action-to-Outcome Funnel

After every citation check or scan, guide toward impact:

1. **NAP consistency below 70%** → "Critical: Inconsistent citations are actively hurting your rankings. Fix the top inconsistencies immediately — this is the single biggest citation-related improvement you can make."
2. **NAP consistency 70-89%** → "Good but leaky. Each inconsistent listing weakens your local authority. Fix the remaining mismatches to solidify your ranking signals."
3. **NAP consistency 90%+** → "Excellent consistency. Now focus on expanding — add listings to directories where competitors are present but you're not."
4. **Unclaimed citations found** → "You have X unclaimed listings. Claiming them gives you control over your brand information and prevents third-party edits."
5. **Few total citations (<10)** → "Your citation count is low compared to competitors. Building citations on high-authority directories can significantly boost local authority."
6. **Post-scan** → "Next: Fix the top 3 inconsistent citations, then run `/rank-check` in 2-3 weeks to measure ranking impact."

**Always end with a "Citation Health Verdict"**: consistency score, total listings, biggest gap, and the single most impactful fix.

## Key Directories by Region

### India
Justdial, Sulekha, IndiaMART, Zomato (restaurants), Practo (healthcare), Google Maps, Bing Places

### United States
Yelp, Yellow Pages, BBB, TripAdvisor (hospitality), Healthgrades (medical), Avvo (legal), Google Maps, Bing Places, Apple Maps

### Universal
Google Maps, Bing Places, Facebook Business, Apple Maps, Foursquare, TripAdvisor
