---
description: Run daily Local SEO operational checks
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__get_reviews_needing_reply", "mcp__fly-agent__generate_review_response", "mcp__fly-agent__post_selected_reply", "mcp__fly-agent__get_profile_protection_status", "mcp__fly-agent__enable_profile_protection", "mcp__fly-agent__get_auto_responder_status", "mcp__fly-agent__setup_review_responder", "mcp__fly-agent__get_failed_posts", "mcp__fly-agent__retry_failed_post", "mcp__fly-agent__get_workspace_review_summary", "mcp__fly-agent__get_workspace_summary", "mcp__fly-agent__refresh_reviews_from_google", "mcp__fly-agent__send_report_email", "mcp__fly-agent__get_workspace_reviews_needing_reply", "mcp__fly-agent__get_workspace_protection_status", "mcp__fly-agent__get_workspace_failed_posts", "mcp__fly-agent__bulk_enable_protection", "mcp__fly-agent__bulk_setup_review_responder", "mcp__fly-agent__bulk_retry_failed_posts", "mcp__fly-agent__generate_shareable_link", "mcp__fly-agent__get_post_history"]
argument-hint: [workspace-name, location-name, or "all"]
---

Execute the daily Local SEO operations routine. Essential daily checks that keep profiles healthy, responsive, and generating leads.

**Data freshness**: Daily ops leverage the freshest data — GBP profiles, reviews, and posts all refresh daily from Fly's backend. Always working with the latest data available.

**Outcome focus**: Every check must surface quantifiable metrics and connect to business impact. Don't just report status — highlight what changed, what it means for visibility/leads, and what to do next.

## Step 1: Establish Scope

**IMPORTANT — always ask the user to choose scope. Never assume or default without user confirmation.**

Check $ARGUMENTS first. If the user explicitly specified a workspace, location, or "all", use that. Otherwise follow this two-step selection:

### Step 1a: Choose Workspace
1. Call `mcp__fly-agent__list_workspaces` to get all workspaces
2. If the user has multiple workspaces, ask: **"Which workspace would you like to run daily ops on?"** and list them. Also offer "all workspaces" as an option.
3. If the user has only one workspace, confirm it and proceed.

### Step 1b: Choose Locations
1. Call `mcp__fly-agent__list_locations` (filtered to the selected workspace)
2. Ask: **"Which locations within [workspace name]? You can pick specific locations or say 'all'."** Default to all locations within the chosen workspace if the user confirms.
3. If the user picks specific locations, note them for the remaining steps.

Do NOT proceed until both workspace and location scope are confirmed.

## Step 2: Workspace-Level Summary

For each workspace in scope:
1. Call `mcp__fly-agent__get_workspace_summary` to get aggregate pending reviews, average rating, and highlights
2. Call `mcp__fly-agent__get_workspace_review_summary` for review metrics across locations

Present a quick overview with quantifiable metrics: total unreplied reviews (with urgency — negative reviews first), current average rating and trend, and any protection alerts. Frame as: "X reviews need responses — Y are negative and should be addressed urgently to protect your rating."

## Step 3: Review Response

**Use aggregate tool first** to get all unreplied reviews across the workspace in a single call:
1. Call `mcp__fly-agent__get_workspace_reviews_needing_reply` with `limit_per_location=10`
2. This returns all unreplied reviews grouped by location — no need to loop through locations individually
3. For each unreplied review, call `mcp__fly-agent__generate_review_response` with appropriate tone based on star rating (friendly for 4-5, professional for 3, apologetic for 1-2)
4. Present generated responses to the user for approval
5. On approval, post using `mcp__fly-agent__post_selected_reply`

**Fallback**: If running for a single specific location, use `mcp__fly-agent__get_reviews_needing_reply` directly.

## Step 4: Profile Protection Check

**Use aggregate tool** to check all locations at once:
1. Call `mcp__fly-agent__get_workspace_protection_status` — returns protection and auto-responder status for all locations in one call
2. If any locations have protection disabled, call `mcp__fly-agent__bulk_enable_protection` to enable for all unprotected locations at once
3. If any locations have auto-responder disabled, call `mcp__fly-agent__bulk_setup_review_responder` to enable for all at once
4. Report any recent unauthorized change alerts

**Fallback**: For a single location, use the individual `get_profile_protection_status` → `enable_profile_protection` → `get_auto_responder_status` → `setup_review_responder` flow.

## Step 5: Failed Post Recovery

**Use aggregate tool** to check all locations at once:
1. Call `mcp__fly-agent__get_workspace_failed_posts` — returns all failed posts grouped by location
2. If any failed posts have retry attempts remaining, ask user if they want to retry
3. Call `mcp__fly-agent__bulk_retry_failed_posts` to retry all eligible failed posts across the workspace at once

**Fallback**: For a single location, use `get_failed_posts` → `retry_failed_post` individually.

## Step 6: Load Branding & Daily Summary

Before presenting the summary, load the white-label branding config:
1. Read `${CLAUDE_PLUGIN_ROOT}/config/branding.json` (or workspace-specific variant `config/branding-{workspace-name}.json`)
2. If branding is configured, apply brand_name as the report header and footer_text as the sign-off
3. If no branding is configured, proceed without it but mention `/setup-branding` is available

Present a consolidated daily ops report branded with the user's identity. Lead with outcomes:

**Daily Scorecard:**
- **Reviews handled**: X of Y responded (reply rate now Z%) — "Maintaining a 90%+ reply rate builds trust and improves local ranking signals"
- **Rating watch**: Current average X.X (trend: up/down/stable) — "Each 0.1 star improvement can increase click-through by ~2%"
- **Profile protection**: X locations protected / Y need attention — "Unprotected profiles risk ranking loss from unauthorized edits"
- **Content recovery**: X failed posts retried — "Active posting keeps your profile visible in local search"
- **Urgent items**: List anything needing immediate manual attention

**Recommended Next Action**: Based on today's data, suggest the single most impactful thing the user should do next (e.g., "Your reply rate is below 80% — respond to remaining reviews to build customer trust" or "All clear today — consider publishing a post to maintain engagement").

**IMPORTANT — posting recommendations**: Before suggesting that the user publish a post, check `mcp__fly-agent__get_post_history` (add it to the daily ops flow or reference the failed-posts data). If a post was published in the last 24 hours, do NOT suggest posting again. Instead say: "You posted recently — your next post should be in [X] days to maintain optimal spacing (2-3 days between posts)." Only recommend posting if the last post was 3+ days ago.

Keep the tone operational and outcome-focused. Flag urgent items at the top.

## Step 7: Client Update (for agencies/freelancers)

Ask the user: **"Would you like to send a daily update to your client?"**

If yes:
1. Compile the daily summary into a concise update
2. Ask for the client's email address (or use a previously provided one)
3. Call `mcp__fly-agent__send_report_email` with report_type "custom" and the client email
4. Alternatively, present the summary in a copy-friendly format the user can paste into their own email/chat
