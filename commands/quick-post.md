---
description: Generate and publish a GBP post quickly
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__generate_post_content", "mcp__fly-agent__create_post_draft", "mcp__fly-agent__publish_post", "mcp__fly-agent__get_content_suggestions"]
argument-hint: [topic or "suggest"]
---

Quickly generate and publish a Google Business Profile post. Regular posting keeps your profile active in local search, signals freshness to Google, and drives customer engagement.

## Step 1: Establish Scope

**IMPORTANT — always ask the user to choose scope. Never assume or default without user confirmation.**

Check $ARGUMENTS for a topic (use it if present). For the target location:

### Step 1a: Choose Workspace
1. Call `mcp__fly-agent__list_workspaces` to get all workspaces
2. If multiple workspaces, ask which one.
3. If only one workspace, confirm and proceed.

### Step 1b: Choose Locations
1. Call `mcp__fly-agent__list_locations` (filtered to selected workspace)
2. Ask: **"Which locations should this post be published to? Pick specific ones or say 'all'."** Default to all within the chosen workspace if user confirms.

Do NOT proceed until scope is confirmed.

## Step 2: Generate Content

1. If no topic in $ARGUMENTS, call `mcp__fly-agent__get_content_suggestions` and let user pick
2. Generate content with `mcp__fly-agent__generate_post_content` using the topic, post_type "UPDATE", and style "engaging"
3. Present the generated post to the user for review

## Step 3: Publish

For each location in scope:
1. Save as draft with `mcp__fly-agent__create_post_draft`
2. On user approval, publish with `mcp__fly-agent__publish_post`
3. Confirm publication with post URL

## Step 4: Outcome Summary

After publishing, present the impact context:
- **Published to**: X locations
- **Post type**: Update/Offer/Event — "Offer posts typically drive the most direct conversions"
- **Expected impact**: "This post will be visible to customers finding you in Google Search and Maps. Posts with CTAs generate measurable clicks, calls, and visits."
- **Track impact**: "Check `/performance` in 48-72 hours to see how this post affected your views and customer actions."
- **Content cadence**: "You've published X posts this month. Target: 4-8 posts/month for optimal engagement."
- **Recommended Next Action**: Based on current content cadence:
  - Below target → "Schedule another post for later this week to maintain momentum"
  - On target → "Great posting cadence. Focus on varying content types (offers, events, updates) to reach different customer segments"
  - Content with CTA → "Posts with clear CTAs (Call Now, Visit Us, Book Online) convert better — make sure every post has one"
