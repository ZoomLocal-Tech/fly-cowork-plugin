# Release Notes

## v0.8.0 (2026-02-20)

### Shareable Links Integration & Agentic-First Pattern

**New MCP Tools Available:**
- `generate_shareable_link` — generate mobile-friendly self-service links for 16 different actions
- `get_available_links` — show all available self-service link options to users

**New Link Types (6 added to existing 10):**
- `optimize` — Full profile optimization wizard (categories, services, hours, attributes)
- `photos` — Upload/manage GBP photos
- `gbp_services` — Add/edit services on Google Business Profile
- `gbp_attributes` — Add/edit business attributes (amenities, accessibility)
- `credits_purchase` — Purchase additional credits
- `dashboard` — View location performance dashboard

**Agentic-First, Link-Fallback Pattern:**
- All skills now follow the principle: prefer direct tool actions first, offer shareable links only as fallback
- `gbp-audit-optimize` skill adds decision table mapping each action to its primary (tool) and fallback (link) approach
- Link fallback sections added to: review-command-center, content-engine, microsite-manager, workspace-account-ops

**Commands Updated:**
- `/seo-audit` — added `generate_shareable_link` to allowed-tools, added manual optimization link option in results
- `/daily-ops` — added `generate_shareable_link` to allowed-tools
- `/respond-reviews` — added `generate_shareable_link` to allowed-tools
- `/quick-post` — added `generate_shareable_link` to allowed-tools

**Skills Updated:**
- `workspace-account-ops` — added complete 16-type shareable link reference table

---

## v0.7.0 (2026-02-20)

### Validated Category & Service Tools

**New MCP Tools Referenced:**
- `get_category_suggestions` — get validated category recommendations from Google's official taxonomy
- `update_profile_categories` — update primary and additional categories with validated gcid values
- `get_available_services` — list valid service types for a location's categories
- `update_services` — add/update service items with validated serviceTypeId values

**Skills Updated:**
- `gbp-audit-optimize` — new "Category & Service Optimization" workflow with validated tools
- `gbp-audit-optimize` — `update_profile_field` no longer recommended for categories/services

**Commands Updated:**
- `/seo-audit` — added `get_category_suggestions` and `get_available_services` to allowed-tools
- `/seo-audit` — added "Step 2b: Category & Service Gap Analysis" workflow

**Reference Files:**
- `seo-scoring-guide.md` — updated optimization priority order with tool recommendations

---

## v0.6.1 (2026-02-19)

### Workspace-Level Aggregate Tools

- Added workspace-level bulk/aggregate tools to `/daily-ops`, `/weekly-ops`, `/monthly-ops` commands
- Added `workspace-orchestrator` and `review-responder` agent types
- Workspace-wide review, protection, content, and SEO operations now use single aggregate API calls instead of per-location loops

---

## v0.6.0 (2026-02-18)

### Initial Release

- 10 specialized skills: gbp-audit-optimize, review-command-center, performance-analytics, rank-tracker, citation-scanner, content-engine, microsite-manager, traffic-insights, reporting-hub, workspace-account-ops
- 11 slash commands: /setup-mcp, /setup-branding, /daily-ops, /weekly-ops, /monthly-ops, /seo-audit, /respond-reviews, /rank-check, /citation-scan, /quick-post, /performance
- 2 autonomous agents: workspace-orchestrator, review-responder
- Multi-workspace, multi-location support with scope confirmation
- White-label branding configuration
- Quantifiable outcomes and KPIs for every workflow
- Action-to-outcome funnels guiding users to highest-impact next steps
