---
description: Run a quick SEO audit on a location
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__get_gbp_profile", "mcp__fly-agent__get_profile_audit", "mcp__fly-agent__get_seo_score_breakdown", "mcp__fly-agent__get_profile_protection_status", "mcp__fly-agent__enable_profile_protection", "mcp__fly-agent__run_gmb_audit"]
argument-hint: [workspace-name, location-name, or "all"]
---

Run an SEO audit on selected locations. Produces a quantified profile health score with prioritized actions tied to visibility, rank, and lead generation impact.

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

## Step 2: Run Audit

For each location in scope:
1. Set default location with `mcp__fly-agent__set_default_location`
2. Call `mcp__fly-agent__get_gbp_profile` for current profile data
3. Call `mcp__fly-agent__get_profile_audit` for completeness score and recommendations
4. Call `mcp__fly-agent__get_seo_score_breakdown` for detailed scoring
5. Call `mcp__fly-agent__get_profile_protection_status` to check monitoring
6. If protection is NOT enabled, call `mcp__fly-agent__enable_profile_protection` to turn it on immediately

## Step 3: Present Results with Business Impact

**Single location:** Present as an outcome-focused scorecard:
- Overall SEO Score (X/100) with estimated visibility impact
- Category scores with what each gap costs in visibility
- Top 3 priority actions ranked by expected impact on leads and rank
- Profile protection status with risk assessment
- **"What This Means"**: Plain-language summary (e.g., "Your profile is missing 15 points worth of optimization that could increase your discovery searches significantly")
- **Recommended Next Action**: The single most impactful thing to do right now (e.g., "Optimize your description with target keywords — this is the fastest win for visibility")

**Multiple locations:** Present a summary table with: location name, SEO score, biggest gap, estimated visibility opportunity — sorted by lowest score (biggest opportunity). Then offer:
- "Want to optimize the weakest location first? That's where the biggest gains are."
- "Want to see a full breakdown for any specific location?"
