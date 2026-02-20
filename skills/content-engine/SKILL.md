---
name: content-engine
description: >
  This skill should be used when the user asks to "create a post",
  "write content", "post ideas", "content calendar", "publish a post",
  "what should I post", "trending topics", "content gaps", "schedule posts",
  "manage drafts", "best performing content", "upcoming holidays",
  or needs help with Google Business Profile content creation and publishing.
version: 0.1.0
---

# Content Engine

Content ideation, creation, scheduling, and publishing for Google Business Profile posts. Includes strategic planning, trend analysis, and performance tracking.

## Multi-Location Awareness

1. Establish context with workspaces/locations
2. Content can be created per location or templated across locations
3. Each location has its own post history and drafts

## Workflow: Content Ideation

1. **Get ideas** — call `mcp__fly-agent__generate_post_ideas` with optional count (1-5) for AI-generated ideas based on business type and trends
2. **Strategic suggestions** — call `mcp__fly-agent__get_content_suggestions` for data-driven recommendations based on category, seasonality, and past performance
3. **Trending topics** — call `mcp__fly-agent__get_trending_topics` with optional category filter for current popular themes
4. **Upcoming holidays** — call `mcp__fly-agent__get_upcoming_holidays` with days_ahead (default 30) for timely content opportunities
5. **Content gaps** — call `mcp__fly-agent__get_content_gaps` to identify missing content types and opportunities
6. **Best performers** — call `mcp__fly-agent__get_best_performing_content` to see what content has worked well in the past 90 days

Present ideas as a numbered list with topic, suggested post type, and why it's relevant.

## Workflow: Content Creation

1. **Generate full post** — call `mcp__fly-agent__generate_post_content` with:
   - `topic`: the post topic or chosen idea
   - `post_type`: UPDATE (general), OFFER (promotions), or EVENT (events)
   - `style`: engaging, professional, or casual
2. Review the generated content with the user
3. Option A: **Save as draft** — call `mcp__fly-agent__create_post_draft` with title, content, post_type, and optional media_urls and call_to_action
4. Option B: **Publish immediately** — after saving as draft, call `mcp__fly-agent__publish_post` with the post_id
5. Option C: **Schedule for later** — after saving as draft, call `mcp__fly-agent__schedule_post` with the post_id and desired publish time

## Workflow: Draft Management

1. **View drafts** — call `mcp__fly-agent__get_post_drafts` to see all unpublished drafts
2. **Publish a draft** — call `mcp__fly-agent__publish_post` with post_id
3. **Delete a draft** — call `mcp__fly-agent__delete_post` with post_id

## Workflow: Post Scheduling

1. **Schedule a post** → after creating a draft with `mcp__fly-agent__create_post_draft`, call `mcp__fly-agent__schedule_post` with post_id and scheduled_at (ISO 8601, must be 10+ min in future)
2. **Publish vs. schedule** → always ask the user: "Publish now or schedule for later?"
3. **View scheduled** → scheduled posts appear in `mcp__fly-agent__get_post_history` with "scheduled" status

## Workflow: Post History & Recovery

1. **View history** — call `mcp__fly-agent__get_post_history` for recent posts with status and engagement
2. **Failed posts** — call `mcp__fly-agent__get_failed_posts` to see posts that failed to publish, with error details and retry attempts remaining
3. **Retry failed** — call `mcp__fly-agent__retry_failed_post` with post_id (max 3 retries per post)

## Workflow: Content Calendar

1. **View calendar** — call `mcp__fly-agent__get_content_calendar` with month and year to see planned and past posts
2. **Plan ahead** — combine holiday calendar, trending topics, and content gaps to build a monthly content plan
3. Create drafts for each planned post to build a ready-to-publish queue

## Workflow: Multi-Location Content

For multi-location brands:
1. Create a content template (topic + style + type)
2. Loop through locations, generating location-specific content using `generate_post_content` per location
3. Save as drafts across locations for review
4. Publish approved posts per location

## Data Freshness & Refresh Cadence

- **Posts** refresh **daily** from Google — published post status and engagement data are updated every day.
- **Content Strategy** is regenerated **monthly on the 7th** — fresh recommendations based on business trends and seasonal factors.
- **Best Performing Content** data reflects the last 90 days and updates daily.
- **Follow-up triggers**:
  - After publishing a post → check engagement metrics via `/performance` after 48-72 hours to see impact on views and actions
  - On the 7th of each month → review new content strategy recommendations and update the content calendar
  - After a failed post → retry within 24 hours (max 3 retries) before creating a new post
  - Weekly → check if the 1-2 posts/week cadence is being met; if not, suggest `/quick-post`

## Quantifiable Outcomes & KPIs

Every content action should connect to measurable business results:

| KPI | What to Show | Business Impact |
|-----|-------------|-----------------|
| Posts Published This Month | Count vs. target (4-8/month) | Consistent posting signals activity to Google |
| Post Engagement | Views, clicks, calls generated per post | Direct measure of content driving leads |
| Content Frequency | Posts per week average | 1-2/week is optimal for GBP engagement |
| Content Mix | Updates vs. Offers vs. Events ratio | Balanced mix reaches different customer intents |
| Best Performing Topic | Highest-engagement post type | Reveals what resonates with your audience |
| Content Gaps | Missing content types or topics | Unfilled gaps = missed audience segments |
| Drafts Pending | Ready-to-publish content count | A healthy queue prevents content gaps |

## Action-to-Outcome Funnel

After every content operation, guide toward lead-generating outcomes:

1. **Zero posts this month** → "Inactive profiles lose visibility. Google favors businesses that post regularly. Publish at least 1 post this week to re-signal activity." → Run `/quick-post` now.
2. **Posting consistently but low engagement** → "Your content isn't converting. Try: posts with offers/CTAs, customer testimonials, or holiday-themed content that drives action." → Check best performing content for patterns.
3. **High-engagement posts identified** → "This topic/format works well. Create similar content to maintain momentum and expand reach."
4. **Content gaps found** → "You're not posting about [topic/type]. Adding this to your mix could reach new customer segments looking for these services."
5. **Upcoming holiday/event** → "Timely content gets higher engagement. Create a holiday-specific post or offer to capitalize on seasonal search spikes."
6. **Offers underutilized** → "Offer posts drive the most direct conversions. Create a limited-time offer to generate immediate leads."
7. **Post published** → "Track impact: check `/performance` in 48-72 hours to see if views and actions increased. This tells you whether the content resonated."

**Always end with a "Content Health Summary"**: posts this month, posting frequency, engagement trend, and the single most impactful content action right now.

## Content Best Practices

- **Post frequency**: 1-2 posts per week for optimal engagement (profiles posting weekly see up to 2x more actions)
- **Post types**: Mix updates (awareness), offers (conversion), and events (engagement)
- **Timing**: Post during business hours for best visibility
- **Media**: Posts with images get significantly more engagement — always include a relevant image
- **CTAs**: Always include a clear call to action — "Call us", "Visit today", "Book now"
- **Length**: 150-300 words is the sweet spot
- **Consistency**: Regular posting compounds over time — set up a content calendar and stick to it

## Shareable Link Fallbacks

When the user wants to do things manually in the web UI, use `mcp__fly-agent__generate_shareable_link`:

| link_type | When to offer |
|-----------|---------------|
| `new_post` | User wants full control over post creation in the web wizard |
| `templates` | User wants to browse and select frame designs for posts |
| `references` | User wants to upload logo, product photos, or team images |
| `ideas` | User wants to browse and approve content ideas visually |
| `photos` | User wants to upload/manage GBP photos |

**Always try the agentic approach first** (e.g., `generate_post_content`, `create_post_draft`, `publish_post`). Only offer links if the user prefers manual control or wants to upload media files.
