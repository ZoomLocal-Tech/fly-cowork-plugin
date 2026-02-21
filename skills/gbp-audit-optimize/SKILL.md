---
name: gbp-audit-optimize
description: >
  This skill should be used when the user asks to "audit my profile",
  "optimize my GBP", "check my SEO score", "improve my Google Business Profile",
  "run a profile audit", "generate a better description", "optimize profile",
  or needs guidance on GBP profile completeness, SEO scoring, or profile protection.
version: 0.1.0
allowed-tools: ["mcp__fly-agent__list_workspaces", "mcp__fly-agent__list_locations", "mcp__fly-agent__set_default_location", "mcp__fly-agent__get_gbp_profile", "mcp__fly-agent__get_profile_audit", "mcp__fly-agent__get_seo_score_breakdown", "mcp__fly-agent__get_profile_protection_status", "mcp__fly-agent__enable_profile_protection", "mcp__fly-agent__run_gmb_audit", "mcp__fly-agent__get_category_suggestions", "mcp__fly-agent__update_profile_categories", "mcp__fly-agent__get_available_services", "mcp__fly-agent__update_services", "mcp__fly-agent__start_profile_optimization", "mcp__fly-agent__apply_profile_optimizations", "mcp__fly-agent__analyze_website_for_optimization", "mcp__fly-agent__generate_seo_description", "mcp__fly-agent__update_profile_field", "mcp__fly-agent__sync_or_refresh_profile_from_google", "mcp__fly-agent__compare_audit_scores", "mcp__fly-agent__generate_shareable_link", "mcp__fly-agent__get_setup_progress", "mcp__fly-agent__get_next_setup_step", "mcp__fly-agent__get_full_setup_status", "mcp__fly-agent__redo_setup_step", "mcp__fly-agent__create_onboarding_link"]
---

# GBP Audit & Optimize

Full Google Business Profile audit and optimization workflow. Supports single-location and multi-location operations across workspaces.

## Agentic First, Link Fallback

**Always prefer direct tool actions over shareable links.** Only offer a shareable link when:
- The direct tool approach fails or doesn't fully cover the need
- The user explicitly asks to "do it manually" or "review it myself"
- The action requires UI interaction (e.g., photo uploads, OAuth connect)

| Action | Primary (Agentic) | Fallback (Link) |
|--------|-------------------|-----------------|
| Update categories | `get_category_suggestions` → `update_profile_categories` | `generate_shareable_link` type=optimize |
| Update services | `get_available_services` → `update_services` | `generate_shareable_link` type=gbp_services |
| Update attributes | `update_profile_field` | `generate_shareable_link` type=gbp_attributes |
| Upload photos | _(no agentic tool — link required)_ | `generate_shareable_link` type=photos |
| Full optimization | `apply_profile_optimizations` | `generate_shareable_link` type=optimize |
| Microsite setup | Microsite tools (set_theme, update_hero, etc.) | `generate_shareable_link` type=microsite |

When the agentic approach completes successfully, skip the link. When it fails or partially succeeds, offer: _"I've done what I can directly. Want a link to review and finish the rest in the UI?"_

## Multi-Location Awareness

Before running any audit or optimization:

1. Call `mcp__fly-agent__list_workspaces` to show all available workspaces
2. Call `mcp__fly-agent__list_locations` to show locations in the selected workspace
3. Ask the user which location(s) to operate on, or confirm "all locations"
4. Use `mcp__fly-agent__set_default_location` to set context for single-location ops

For bulk operations, loop through each location_id and run the workflow per location.

## Workflow: Full SEO Audit

1. **Pull current profile** — call `mcp__fly-agent__get_gbp_profile` to retrieve business name, description, categories, hours, contact info, rating, and review count
2. **Run SEO audit** — call `mcp__fly-agent__get_profile_audit` to get completeness score and recommendations
3. **Get SEO score breakdown** — call `mcp__fly-agent__get_seo_score_breakdown` for detailed scoring across business name, description, primary category, and additional categories
4. **Check profile protection** — call `mcp__fly-agent__get_profile_protection_status` to verify monitoring is active
5. **Enable protection if off** — if protection is NOT enabled, call `mcp__fly-agent__enable_profile_protection` to turn it on immediately
6. **Present findings** — summarize the audit with a clear score, category-by-category breakdown, and prioritized action items

## Workflow: Profile Optimization

1. **Start optimization flow** — call `mcp__fly-agent__start_profile_optimization` to get the current assessment and optimization link
2. **Analyze website** (if available) — call `mcp__fly-agent__analyze_website_for_optimization` with the business website URL to extract products, services, USPs, and keywords
3. **Generate SEO description** — call `mcp__fly-agent__generate_seo_description` with style preference (professional, friendly, or compelling)
4. **Present optimization suggestions** — show the user what changes are recommended, numbered for selection
5. **Apply selected changes** — call `mcp__fly-agent__apply_profile_optimizations` with the user's selection (e.g., "1, 2, 3" or "all")
6. **Update specific fields** if needed — use `mcp__fly-agent__update_profile_field` for targeted changes to description, phone, website, hours, attributes, or service areas

## Workflow: Category & Service Optimization

Use these dedicated tools for category and service updates — they validate against Google's official taxonomy to ensure only valid values are submitted.

1. **Get category suggestions** — call `mcp__fly-agent__get_category_suggestions` to get AI-powered category recommendations. Each suggestion includes a `display_name` and `category_id` (gcid format), all pre-validated against Google's official category list.
2. **Update categories** — call `mcp__fly-agent__update_profile_categories` passing the exact `display_name` or `category_id` values from the suggestions. Do NOT invent category names — only use values returned by the suggestion tool.
3. **Get available services** — call `mcp__fly-agent__get_available_services` to see the valid service types for the location's categories (pulled from Google's official taxonomy)
4. **Update services** — call `mcp__fly-agent__update_services` with validated serviceTypeId values to add or update service items on the profile

> **Important**: Do NOT use `update_profile_field` for categories or service items — use the dedicated tools above which validate against Google's official values and prevent rejected updates.

**Link fallback**: If the agentic tools fail or the user wants manual control:
- Categories & services: `mcp__fly-agent__generate_shareable_link` with `link_type="optimize"` — full optimization wizard
- Services only: `mcp__fly-agent__generate_shareable_link` with `link_type="gbp_services"`
- Attributes only: `mcp__fly-agent__generate_shareable_link` with `link_type="gbp_attributes"`

## Workflow: Competitor Audit

1. Call `mcp__fly-agent__run_gmb_audit` with a competitor's business_name (and optional lat/lng for location bias) or place_id
2. Present the competitor's profile completeness, metrics, and comparison insights
3. Identify gaps between the user's profile and the competitor

## Workflow: Profile Sync & Refresh

1. Call `mcp__fly-agent__sync_or_refresh_profile_from_google` to pull latest data from Google
2. Re-run audit after sync to show updated scores

## Workflow: Before/After Score Comparison

After optimization, call `mcp__fly-agent__compare_audit_scores` with the initial_score from the first audit to show improvement.

## Workflow: Onboarding & Setup

1. Call `mcp__fly-agent__get_setup_progress` to see completed and remaining setup steps
2. Call `mcp__fly-agent__get_next_setup_step` to guide through the next action
3. Use `mcp__fly-agent__redo_setup_step` with step_number (1=SEO Audit, 2=Profile Optimization, 3=Profile Protection, 4=Auto-Responder, 5=Review Generator, 6=Microsite) to re-run any step
4. Call `mcp__fly-agent__get_full_setup_status` for a comprehensive status view
5. Use `mcp__fly-agent__create_onboarding_link` to generate a shareable link for the business owner (simple variant for essential optimization, advanced for full flow)

## Data Freshness & Refresh Cadence

- **GBP Profile data** refreshes **daily** from Google. Always check the sync status before auditing.
- If the user reports recent changes that aren't reflected, call `mcp__fly-agent__sync_or_refresh_profile_from_google` first.
- After applying optimizations, note: "Changes typically reflect in Google within 24-48 hours. Run another audit tomorrow to verify your score improvement."

## Quantifiable Outcomes & KPIs

Every audit must connect findings to business impact. Track and present:

| KPI | What to Show | Business Impact |
|-----|-------------|-----------------|
| SEO Score (X/100) | Current vs. previous | Higher score = better local search visibility |
| Score Delta | Points gained since last audit | Proves optimization ROI to clients |
| Category Gaps | Missing categories count | Each relevant category added can unlock new keyword visibility |
| Description Keywords | Keyword count and relevance | Keyword-rich descriptions improve discoverability for transactional searches |
| Profile Completeness % | Fields filled vs. total | Complete profiles get significantly more views and actions |
| Competitor Gap | Score difference vs. top local competitor | Quantifies the opportunity to overtake competitors |
| Protection Status | On/Off | Unprotected profiles risk losing ranking overnight from unauthorized edits |

## Action-to-Outcome Funnel

After every audit, guide the user to the highest-impact next action. Never leave the user without a clear next step:

1. **Score below 50** → "Your profile is losing significant visibility. Optimizing to 80+ can dramatically increase discovery searches." → Run profile optimization immediately.
2. **Score 50-79** → "Good foundation — closing these gaps could increase impressions by 20-40%." → Prioritize description + category optimization.
3. **Score 80+** → "Strong profile. Now convert visibility into leads — focus on reviews, content, and conversion actions." → Suggest `/respond-reviews` and `/quick-post`.
4. **Protection OFF** → "Your profile is unprotected. Unauthorized edits could tank your rankings overnight." → Call `mcp__fly-agent__enable_profile_protection` to enable it immediately.
5. **Competitor scores higher** → "Your competitor has X points on you — here's exactly what they have that you don't." → Present gap as actionable checklist with estimated impact.
6. **Post-optimization** → "Re-audit in 24-48h to verify score improvement. Then track impact on impressions via `/performance`."

**Always end every audit with a "What This Means For Your Business" summary** that translates scores into plain language: estimated visibility impact, lead generation potential, and the single most impactful action to take right now.

## Output Format

Present audit results as an outcome-focused scorecard:
- Overall SEO Score (X/100) with trend vs. last audit
- Estimated visibility impact: "Fixing the top 3 items could increase profile views by ~X%"
- Category scores with status indicators
- Top 3 priority actions ranked by impact on visibility and leads
- Link to optimization page if applicable
- **Recommended Next Action**: specific command to run next (e.g., "Run `/quick-post` to start converting visibility into engagement" or "Run `/rank-check` to see how these changes affect your local rankings")

For multi-location audits, present a summary table: location name, SEO score, score trend, biggest gap, estimated visibility opportunity, and recommended action — sorted by lowest score first (biggest opportunity).

## Available Shareable Links

When a user wants to do something manually in the web UI, or when a direct tool action isn't available, use `mcp__fly-agent__generate_shareable_link` with the appropriate `link_type`:

| link_type | When to offer |
|-----------|---------------|
| `optimize` | Full profile optimization wizard (categories, services, hours, attributes) |
| `gbp_services` | User wants to manually browse and add/edit services |
| `gbp_attributes` | User wants to manually manage business attributes |
| `photos` | User wants to upload/manage GBP photos (always requires link — no agentic upload) |
| `dashboard` | User wants to see a visual performance dashboard |

Call `mcp__fly-agent__get_available_links` to show the user all available self-service options.

## Reference Files

- **`references/seo-scoring-guide.md`** — detailed explanation of how each SEO category is scored and what impacts rankings
