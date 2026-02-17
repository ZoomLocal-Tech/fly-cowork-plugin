---
description: Check keyword rankings for a location
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__get_local_rankings", "mcp__fly-agent__get_tracked_keywords", "mcp__fly-agent__get_visibility_score", "mcp__fly-agent__get_ranking_trends", "mcp__fly-agent__get_workspace_rankings", "mcp__fly-agent__run_on_demand_scan"]
argument-hint: [workspace-name, location-name, or keyword]
---

Check keyword rankings for selected locations, or scan a specific keyword. Rankings directly impact lead generation — top 3 positions capture ~70% of local search clicks.

**Data freshness**: Local rankings are auto-refreshed **weekly every Monday** by Fly's backend. On-demand scans provide real-time data.

## Step 1: Establish Scope

**IMPORTANT — always ask the user to choose scope. Never assume or default without user confirmation.**

Parse $ARGUMENTS:
- If it looks like a keyword phrase (not matching any workspace/location name), run an on-demand scan for that keyword on the user's chosen location
- If it matches a workspace or location name, use that as scope
- If "all" → show rankings across all locations
- If empty or unclear → follow the two-step selection below

### Step 1a: Choose Workspace
1. Call `mcp__fly-agent__list_workspaces` to get all workspaces
2. If multiple workspaces, ask which one. Also offer "all workspaces".
3. If only one workspace, confirm and proceed.

### Step 1b: Choose Locations
1. Call `mcp__fly-agent__list_locations` (filtered to selected workspace)
2. Ask: **"Which locations? Pick specific ones or say 'all'."** Default to all within the chosen workspace if user confirms.

Do NOT proceed until scope is confirmed.

## Step 2: Show Rankings

**For location rankings (per location in scope):**
1. Set default location
2. Call `mcp__fly-agent__get_tracked_keywords` to show monitored keywords
3. Call `mcp__fly-agent__get_local_rankings` for current positions
4. Call `mcp__fly-agent__get_visibility_score` for overall score
5. Call `mcp__fly-agent__get_ranking_trends` for movement

**For keyword scan:**
1. First confirm which location to scan from (if not already set)
2. Call `mcp__fly-agent__run_on_demand_scan` with the keyword
3. Present the grid results showing positions around the business location

## Step 3: Outcome Summary

Present rankings with business context:
- **Keywords in top 3**: X of Y — "These keywords are generating the majority of your local search leads"
- **Visibility score**: X/100 with trend — "Your overall local search presence is [strong/moderate/weak]"
- **Biggest win**: Keyword that improved the most — celebrate and reinforce
- **Biggest concern**: Keyword that dropped the most — explain potential impact on leads
- **Not ranking at all**: Keywords where the business doesn't appear — "You're invisible for these searches. Customers looking for [keyword] won't find you."
- **Recommended Next Action**: Based on ranking health:
  - Rankings strong → "Maintain with consistent posting and review responses. Check performance to verify these rankings are converting to leads."
  - Rankings dropping → "Investigate: check profile for recent changes (`/seo-audit`), ensure reviews are being responded to, and verify citation consistency."
  - Not ranking for key terms → "Consider: optimize your profile description for these terms, create content targeting them, and build relevant citations."
