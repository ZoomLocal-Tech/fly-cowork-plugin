---
description: Run a citation scan to find business listings
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__run_citation_scan", "mcp__fly-agent__save_discovered_citation", "mcp__fly-agent__complete_citation_scan", "mcp__fly-agent__get_citation_health_report", "mcp__fly-agent__get_all_citations", "mcp__fly-agent__get_priority_citation_actions", "WebSearch"]
argument-hint: [workspace-name, location-name]
---

Run a comprehensive citation scan for selected locations. Consistent citations across directories strengthen local authority signals and directly improve local search rankings.

## Step 1: Establish Scope

**IMPORTANT — always ask the user to choose scope. Never assume or default without user confirmation.**

Check $ARGUMENTS first. If the user explicitly specified a workspace or location, use that. Otherwise:

### Step 1a: Choose Workspace
1. Call `mcp__fly-agent__list_workspaces` to get all workspaces
2. If multiple workspaces, ask which one.
3. If only one workspace, confirm and proceed.

### Step 1b: Choose Locations
1. Call `mcp__fly-agent__list_locations` (filtered to selected workspace)
2. Ask: **"Which locations would you like to scan? Pick specific ones or say 'all'."** Default to all within the chosen workspace if user confirms.

Do NOT proceed until scope is confirmed.

## Step 2: Run Scan (per location in scope)

1. Set default location
2. Call `mcp__fly-agent__run_citation_scan` to get search queries
3. Execute ALL returned search queries in parallel using web search
4. For each listing discovered, call `mcp__fly-agent__save_discovered_citation` with the found details
5. Call `mcp__fly-agent__complete_citation_scan` to finalize
6. Call `mcp__fly-agent__get_citation_health_report` to show updated health
7. Call `mcp__fly-agent__get_priority_citation_actions` for recommended next steps

## Step 3: Outcome Summary

Present per location with business impact:
- **Total citations**: X listings found across Y directories — "More consistent citations = stronger local authority"
- **NAP consistency**: X% — "Inconsistent NAP data directly confuses Google and hurts your local rankings"
- **New discoveries**: X new listings found this scan
- **Citations needing fixes**: X listings with incorrect info — "Each one is actively sending conflicting signals to Google"
- **Unclaimed listings**: X — "Claiming these gives you control over your brand presence"
- **Priority actions**: Top 3 fixes ranked by impact on local ranking signals
- **Recommended Next Action**: Based on scan results:
  - Low consistency → "Fix the top 3 NAP inconsistencies first — this is the fastest citation-related win for rankings"
  - Good consistency, few citations → "Expand to new directories to build authority. Target directories your competitors use."
  - Strong citation profile → "Citations are solid. Focus on other ranking factors — run `/rank-check` to see the impact."
