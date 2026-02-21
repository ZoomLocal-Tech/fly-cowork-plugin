---
name: workspace-account-ops
description: >
  This skill should be used when the user asks to "switch workspace",
  "list my locations", "manage my account", "subscription status",
  "add a location", "manage billing", "usage limits", "switch location",
  "show all workspaces", "onboarding link", "upload photos",
  or needs help navigating multi-workspace and multi-location setups.
version: 0.1.0
---

# Workspace & Account Operations

Navigate and manage multi-workspace, multi-location setups. Handle account details, subscriptions, usage tracking, and onboarding for agencies, freelancers, and multi-location brands.

## Workflow: Workspace Navigation

1. **List workspaces** — call `mcp__fly-agent__list_workspaces` to see all accessible workspaces (each represents a client or business unit)
2. **Workspace summary** — call `mcp__fly-agent__get_workspace_summary` with workspace_id for aggregate metrics (reviews pending, avg rating, highlights)
3. **List locations in workspace** — call `mcp__fly-agent__list_locations` with optional workspace_id filter
4. **Location details** — call `mcp__fly-agent__get_locations_summary` with workspace_id for all locations with addresses and subscription info
5. **Set active location** — call `mcp__fly-agent__set_default_location` with location_id to set context for subsequent operations

## Workflow: Account Management

1. **Account details** — call `mcp__fly-agent__get_account_details` with user_id to see name, email, phone, connected Google Account, total locations, workspace info
2. **Account page link** — call `mcp__fly-agent__get_account_details_link` with user_id and link_type "account"
3. **Manage locations link** — call `mcp__fly-agent__get_manage_locations_link` with user_id and link_type "manage_locations"

## Workflow: Subscription & Billing

1. **Status** — call `mcp__fly-agent__get_subscription_status` for plan details, usage, and trial info
2. **Benefits** — call `mcp__fly-agent__explain_subscription_benefits` for feature breakdown and value prop
3. **Manage subscription** — call `mcp__fly-agent__get_subscription_link` with user_id and link_type "manage_subscription"
4. **Checkout** — call `mcp__fly-agent__get_checkout_link` with user_id and link_type "checkout"

## Workflow: Usage Tracking

Call `mcp__fly-agent__get_usage_summary` to see monthly usage of chat messages and AI images against limits.

## Workflow: Onboarding & Setup

1. **Setup progress** — call `mcp__fly-agent__get_setup_progress` to see completed/remaining steps
2. **Next step** — call `mcp__fly-agent__get_next_setup_step` for guided next action
3. **Full status** — call `mcp__fly-agent__get_full_setup_status` for comprehensive feature status
4. **Redo a step** — call `mcp__fly-agent__redo_setup_step` with step_number
5. **Onboarding link** — call `mcp__fly-agent__create_onboarding_link` with variant ("simple" or "advanced")
6. **SEO next steps** — call `mcp__fly-agent__get_next_steps_for_seo` for actionable improvement path

## Workflow: Media Uploads

1. **Reference images** — call `mcp__fly-agent__get_reference_images_upload_link` for content personalization images
2. **GBP photos** — call `mcp__fly-agent__get_photos_upload_link` for photos published to the Google Business Profile
3. **Alternative** — call `mcp__fly-agent__generate_shareable_link` with `link_type="photos"` or `link_type="references"` for the mobile-friendly upload interface

## Workflow: Profile Links

Call `mcp__fly-agent__get_all_profile_links` with optional link_filter:
- `"microsite"` — microsite/landing page link
- `"google_review"` — Google review link
- `"review_generator"` — Fly review generator link
- `"maps"` — Google Maps profile link
- `"website"` — website link
- No filter — all links

## Agency/Freelancer Navigation Pattern

When managing multiple clients:
1. Start with `list_workspaces` to see all clients
2. Select a workspace (client)
3. List locations within that workspace
4. Set default location for operations
5. Run desired workflows (audit, reviews, performance, etc.)
6. Switch to next workspace/location and repeat

For workspace-wide operations, pass workspace_id directly to workspace-level tools without setting a default location.

## Workflow: White-Label Branding Setup

For agencies, freelancers, and brands that want their own identity on all reports and emails:

1. Run `/setup-branding` to configure brand name, logo, website, contact email, colors, tagline, and footer text
2. Branding is saved to `${CLAUDE_PLUGIN_ROOT}/config/branding.json`
3. For multi-client agencies, per-workspace branding can be saved as `config/branding-{workspace-name}.json`
4. All reports (PDF, email, and summaries) will automatically use this branding
5. Re-run `/setup-branding` anytime to update

This ensures all client-facing output — reports, emails, summaries — carries the agency/brand identity, not Fly's.

## Data Freshness & Refresh Cadence (Global Reference)

Fly's backend continuously refreshes data at these cadences. All skills and commands have access to the latest data via Fly's data injection — temporal trends, historical comparisons, and contextual recommendations are always available.

| Data Type | Refresh Cadence | Notes |
|-----------|----------------|-------|
| Google Business Profile | Daily | Profile fields, categories, hours, contact info |
| Reviews | Daily | New reviews + insights (weekly + monthly aggregates) |
| Posts | Daily | Published post status and engagement |
| Performance Stats | Daily (T to T-14) | ~7 day reporting delay from Google |
| Local Rankings | Weekly (every Monday) | Automated grid scans across all tracked keywords |
| Search Insights | Weekly (every Monday) | Keyword traffic data from Google Performance API |
| Review Insights | Daily / Weekly / Monthly | Tiered: new reviews daily, weekly rollups, monthly summaries |
| Content Strategy | Monthly (7th of month) | Fresh recommendations based on trends and seasonality |
| Monthly Performance Report | Monthly (7th of month) | Full month data compiled by backend |

**Operational implications**: Daily operations leverage the freshest profile/review/post data. Weekly operations are best timed after Monday's ranking and search insight refreshes. Monthly operations should be run after the 7th when backend reports are fully compiled.

## Quantifiable Outcomes & KPIs

Workspace management itself supports measurable outcomes:

| KPI | What to Track | Business Impact |
|-----|--------------|-----------------|
| Locations Active | Connected + optimized locations | More active locations = broader market coverage |
| Setup Completion % | Onboarding steps completed per location | Fully set-up locations perform significantly better |
| Subscription Utilization | Usage vs. plan limits | Ensures you're getting full value from the platform |
| Multi-Location Coverage | % of locations with all features enabled | Gaps in coverage = missed optimization opportunities |

## Action-to-Outcome Funnel

After any account/workspace operation, guide toward value realization:

1. **Locations not fully set up** → "X locations haven't completed onboarding. Fully onboarded locations see significantly better performance. Complete setup now with `/seo-audit` and profile optimization."
2. **Usage near limits** → "You've used X% of your monthly quota. Consider upgrading to ensure uninterrupted optimization."
3. **New workspace/location added** → "Let's get this location optimized from day one. Start with `/seo-audit` → `/setup-branding` → `/respond-reviews`."
4. **Multiple workspaces** → "As an agency, ensure every client workspace has: branding configured, keywords tracked, and a monthly reporting cadence established."
5. **After switching context** → Always suggest the most relevant next action for the selected workspace/location based on what needs attention most.

## All Shareable Link Types

Use `mcp__fly-agent__generate_shareable_link` with `link_type` to generate mobile-friendly self-service links. Call `mcp__fly-agent__get_available_links` to show the user all options.

**Always prefer agentic tools first. Only offer links when the user wants manual control or the action requires UI interaction (file uploads, OAuth, etc.).**

| link_type | Purpose |
|-----------|---------|
| `optimize` | Full profile optimization wizard (categories, services, hours, attributes) |
| `gbp_services` | Add/edit services on the Google Business Profile |
| `gbp_attributes` | Add/edit business attributes (amenities, accessibility) |
| `photos` | Upload/manage GBP photos |
| `templates` | Select frame/post templates |
| `references` | Upload reference images (logos, products, team) |
| `new_post` | Create and publish a GBP post |
| `ideas` | View and approve content ideas |
| `review_generator` | Configure review QR code and collection page |
| `review_responder` | Configure auto-responder settings |
| `microsite` | Configure microsite/landing page |
| `dashboard` | View location performance dashboard |
| `subscriptions` | View plan, usage, and billing |
| `credits_purchase` | Purchase additional credits |
| `connect` | Connect a new Google location (requires phone) |
| `reconnect` | Refresh expired Google connection |
