---
name: review-command-center
description: >
  This skill should be used when the user asks to "manage reviews",
  "respond to reviews", "check review sentiment", "set up auto responder",
  "get a review QR code", "review generator link", "bulk reply to reviews",
  "analyze review trends", or needs help with any Google Business Profile
  review management tasks.
version: 0.1.0
---

# Review Command Center

Complete review management workflow — fetch, analyze, respond, and automate review operations across single or multiple locations.

## Multi-Location Awareness

Before any review operation:

1. Call `mcp__fly-agent__list_workspaces` and `mcp__fly-agent__list_locations` to establish context
2. For workspace-wide review summaries, use `mcp__fly-agent__get_workspace_review_summary`
3. Set default location with `mcp__fly-agent__set_default_location` for single-location work

## Workflow: Review Dashboard

1. **Get stats** — call `mcp__fly-agent__get_review_stats` for total reviews, average rating, rating distribution, and trends
2. **Check pending replies** — call `mcp__fly-agent__get_reviews_needing_reply` to see unreplied reviews
3. **Review trends** — call `mcp__fly-agent__get_review_stats` for rating distribution, trends, and reply rate metrics
4. Present a dashboard summary: total reviews, average rating, reply rate, rating distribution, and count of reviews needing attention

## Workflow: Respond to Reviews

### Single Review Response
1. Call `mcp__fly-agent__get_reviews_needing_reply` to list unreplied reviews
2. User selects a review (by position number, reviewer name, or review ID)
3. Call `mcp__fly-agent__generate_review_response` with the selected review — use `position` for numbered selection, `reviewer_name` for name-based selection, or `review_id` for direct ID
4. Set `tone` based on review rating: "friendly" for 4-5 stars, "professional" for 3 stars, "apologetic" for 1-2 stars (or let user choose)
5. Present the generated response options to the user
6. On user approval, call `mcp__fly-agent__post_selected_reply` with the chosen option_number (1, 2, or 3)

### Bulk Review Response
1. Fetch all unreplied reviews with `mcp__fly-agent__get_reviews_needing_reply` (set higher limit)
2. For each review, generate a response with appropriate tone
3. Present all generated responses in a numbered list
4. Ask user to approve all, select specific ones, or edit individual responses
5. Post approved responses using `mcp__fly-agent__post_selected_reply` or `mcp__fly-agent__respond_to_review` for custom text

### Update or Delete Existing Reply
- Use `mcp__fly-agent__respond_to_review` with action "update" to modify an existing reply
- Use `mcp__fly-agent__respond_to_review` with action "delete" to remove a reply

## Workflow: Review Search & Analysis

1. **Search by keyword** — call `mcp__fly-agent__search_reviews` with a query (e.g., "parking", "service", "wait time")
2. **Recent reviews** — call `mcp__fly-agent__get_recent_reviews` with a limit
3. **Refresh from Google** — call `mcp__fly-agent__refresh_reviews_from_google` to sync latest reviews
4. **Workspace overview** — call `mcp__fly-agent__get_workspace_review_summary` for cross-location review health

## Workflow: Auto-Responder Setup

### Quick Setup (recommended for first-time enablement)
1. Call `mcp__fly-agent__setup_review_responder` with `location_id` — enables auto-responder with sensible defaults
   - Optional: `salutation` (standard, dear, ji, sir_maam, none) — defaults to "standard"
   - Optional: `word_limits` (short, medium, long) — defaults to "medium"
   - Only `location_id` is required — workspace is resolved automatically

### Advanced Configuration
1. Check current status with `mcp__fly-agent__get_auto_responder_status`
2. Configure settings with `mcp__fly-agent__update_auto_responder_settings`:
   - `enabled`: true/false
   - `salutation`: standard, dear, ji, sir_maam, none
   - `word_limits`: short (8-12 words), medium (12-16), long (16-24)
   - `business_name`: custom name for responses
3. Both `location_id` and `workspace_id` are required for advanced configuration

## Workflow: Review Collection Tools

1. **Review generator link** — call `mcp__fly-agent__get_review_generator_info` to get/create the shareable review collection link
2. **QR code** — call `mcp__fly-agent__get_review_qr_code` with location_id to generate a printable QR code for in-store display
3. **All profile links** — call `mcp__fly-agent__get_all_profile_links` with link_filter "google_review" or "review_generator"

## Workflow: Multi-Location Review Summary

1. Call `mcp__fly-agent__get_workspace_review_summary` for aggregate metrics across all locations
2. Identify locations with lowest ratings or highest unreplied counts
3. Prioritize response effort on locations needing the most attention

## Tone Selection Guide

| Star Rating | Recommended Tone | Approach |
|-------------|-----------------|----------|
| 5 stars | friendly | Thank warmly, highlight what they enjoyed, invite return |
| 4 stars | friendly | Thank, acknowledge the positive, gently address any concerns |
| 3 stars | professional | Acknowledge feedback, address specific points, offer resolution |
| 2 stars | apologetic | Apologize sincerely, address concerns directly, offer to make it right |
| 1 star | apologetic | Empathize, take responsibility, provide contact for resolution |

## Data Freshness & Refresh Cadence

- **Reviews** refresh **daily** from Google — new reviews appear within 24 hours.
- **Review Insights** refresh daily for new reviews, weekly for weekly aggregates, and monthly for monthly summaries.
- Always call `mcp__fly-agent__refresh_reviews_from_google` at the start of any review session to ensure the latest reviews are loaded.
- After posting responses, note: "Response will appear on Google within a few hours. Monitor for any follow-up replies from reviewers."
- **Follow-up trigger**: After responding to negative reviews, schedule a check in 7 days to see if the reviewer updated their rating.

## Quantifiable Outcomes & KPIs

Every review operation should surface measurable business impact:

| KPI | What to Show | Business Impact |
|-----|-------------|-----------------|
| Reply Rate % | Replied / Total reviews | Businesses that reply to 90%+ of reviews see higher trust and conversion |
| Average Rating | Current rating + trend | Each 0.1 star increase can increase click-through by ~2% |
| Rating Delta | Change over 30/90 days | Shows whether customer satisfaction is improving |
| Rating Distribution | 5/4/3/2/1 star breakdown | Shows customer satisfaction patterns and identifies problem areas |
| Time to Reply | Average response time | Faster replies show engagement — Google rewards responsive businesses |
| Review Volume | New reviews per month | More reviews = stronger social proof = more leads |
| Negative Review % | 1-2 star share of total | Declining negative % indicates service improvements |

## Action-to-Outcome Funnel

After every review operation, guide the user toward lead-generating actions:

1. **Low reply rate (<70%)** → "Unreplied reviews hurt trust. Responding to all reviews can increase customer engagement by up to 12%." → Clear the backlog now with `/respond-reviews`.
2. **Rating below 4.0** → "A 4.0+ rating is the threshold most customers use to filter businesses. Focus on addressing negative feedback and encouraging new positive reviews." → Set up review generator + QR code.
3. **Rating 4.0-4.4** → "Getting to 4.5+ puts you in the top tier for local searches. Encourage happy customers to leave reviews." → Share review generator link.
4. **Rating 4.5+** → "Excellent rating. Maintain it by responding promptly and use this social proof in your content." → Suggest `/quick-post` highlighting customer love.
5. **Negative reviews spike** → "Multiple low-rated reviews this week. Address these urgently — unresolved complaints deter new customers." → Prioritize 1-2 star responses.
6. **Auto-responder OFF** → "Enable auto-responder to ensure 100% reply rate even when you're busy. Consistent responses build trust." → Call `mcp__fly-agent__setup_review_responder` to enable it immediately.
7. **Low review volume** → "More reviews = more visibility. Share your review link and QR code to boost collection." → Generate QR code and review link.

**Always end with a "Review Health Summary"** showing: total reviews, rating, reply rate, rating trend, and the single most impactful action to boost brand trust and leads.

## Shareable Link Fallbacks

When the user wants to do things manually in the web UI, use `mcp__fly-agent__generate_shareable_link`:

| link_type | When to offer |
|-----------|---------------|
| `review_generator` | User wants to visually configure review QR code and collection page settings |
| `review_responder` | User wants to visually configure auto-responder rules and tone settings |
| `dashboard` | User wants to see review stats in a visual dashboard |

**Always try the agentic approach first** (e.g., `setup_review_responder`, `get_review_qr_code`). Only offer links if the user prefers manual control or the tool action fails.

## Reference Files

- **`references/review-response-best-practices.md`** — guidelines for crafting effective review responses
