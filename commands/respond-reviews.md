---
description: Batch-respond to all unreplied reviews
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__get_reviews_needing_reply", "mcp__fly-agent__generate_review_response", "mcp__fly-agent__post_selected_reply", "mcp__fly-agent__respond_to_review", "mcp__fly-agent__get_workspace_review_summary", "mcp__fly-agent__setup_review_responder", "mcp__fly-agent__get_auto_responder_status", "mcp__fly-agent__generate_shareable_link"]
argument-hint: [workspace-name, location-name, or "all"]
---

Batch-respond to unreplied reviews for selected locations. A high reply rate builds customer trust, improves local ranking signals, and protects your brand reputation.

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

## Step 2: Generate Responses

For each location in scope:
1. Call `mcp__fly-agent__get_reviews_needing_reply` with limit 20
2. For each unreplied review, generate a response with `mcp__fly-agent__generate_review_response` using appropriate tone:
   - 4-5 stars: friendly
   - 3 stars: professional
   - 1-2 stars: apologetic
3. Present all generated responses in a numbered list grouped by location

## Step 3: Approve & Post

1. Ask user to approve all, select specific ones, or edit individual responses
2. Post approved responses using `mcp__fly-agent__post_selected_reply`

## Step 4: Outcome Summary

Present an outcome-focused report:
- **Responded**: X of Y reviews handled — reply rate now Z%
- **Rating context**: Current average rating and how these responses help maintain/improve it
- **Negative reviews addressed**: X negative reviews responded to — "Timely responses to negative reviews can prevent customer churn and show potential customers you care"
- **Reply rate impact**: "Your reply rate is now X%. Businesses with 90%+ reply rates see higher trust and better conversion."
- **Remaining**: Y reviews still pending (if any)
- **Auto-responder check**: Call `mcp__fly-agent__get_auto_responder_status` — if OFF, offer to enable it with `mcp__fly-agent__setup_review_responder` to maintain 100% reply rate automatically
- **Recommended Next Action**: Based on results — e.g., "Enable the auto-responder to maintain 100% reply rate" or "Your review volume is low — share your review link to collect more social proof" or "Great job! All reviews handled. Next: check your rankings to see the impact."
