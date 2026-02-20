# Release Notes

## v0.8.0 (2026-02-20)

### Self-Service Links & Smarter Automation

**Do it yourself or let the AI handle it — your choice.**

This release adds 16 shareable self-service links across the plugin. Every workflow now follows an "automation first" approach: the AI tries to get the job done directly using tools, and only offers you a self-service link if you'd prefer to review and do it yourself in the UI.

**New self-service link types you can request:**

- **Optimize** — Opens a guided wizard to update your categories, services, hours, and attributes step by step
- **Photos** — Upload and manage your Google Business Profile photos directly from your phone or browser
- **Services** — Add or edit the services listed on your profile so customers know exactly what you offer
- **Attributes** — Set business attributes like Wi-Fi, wheelchair access, outdoor seating, etc.
- **Buy Credits** — Purchase additional credits when you need more AI-generated content, scans, or reports
- **Dashboard** — View your location's performance dashboard with key metrics at a glance

These join the 10 existing link types (review generator, review responder, microsite editor, post creator, templates, content ideas, reference images, onboarding, account settings, and custom domain setup).

**How it works in practice:**

When you ask to optimize your profile, the AI will:
1. Try to make the changes directly (update categories, services, description, etc.)
2. If something needs your manual review — like uploading photos — it generates a mobile-friendly link you can tap to finish in the UI
3. You're always in control: say "give me a link" anytime to switch to the self-service UI

**Updated commands:** `/seo-audit`, `/daily-ops`, `/respond-reviews`, and `/quick-post` all now support generating self-service links when needed.

---

## v0.7.0 (2026-02-20)

### Validated Category & Service Updates

**No more guesswork when updating your business categories and services.**

Previously, updating categories and services could fail silently if the values didn't match Google's official taxonomy. Now, every category and service update is validated against Google's database before being applied.

**What you can now do:**

- **Get category recommendations** — Ask "what categories should I use?" and get suggestions pulled from Google's official taxonomy, matched to your business type
- **Update categories with confidence** — When the AI updates your primary or additional categories, it uses verified Google category IDs so changes actually stick
- **See available services** — Ask "what services can I add?" to see the exact service types Google supports for your business categories
- **Add services that work** — Service updates now use validated service type IDs, eliminating failed or ignored updates

**Where you'll see this:**

- `/seo-audit` now includes a Category & Service Gap Analysis step that checks if you're using the best categories and identifies missing services
- The GBP Audit & Optimize skill walks you through category and service optimization using the validated tools
- The SEO scoring guide now prioritizes category and service optimization in its recommendations

---

## v0.6.1 (2026-02-19)

### Faster Multi-Location Operations

**Manage all your locations at once instead of one by one.**

If you manage multiple locations (or multiple clients with many locations each), bulk operations are now significantly faster.

**What changed:**

- **Workspace-level commands** — `/daily-ops`, `/weekly-ops`, and `/monthly-ops` now use workspace-wide API calls instead of looping through each location individually. This means checking reviews, protection status, and content health across 50 locations takes one call instead of 50.
- **Two new agent types** — The Workspace Orchestrator handles bulk cross-location operations (audits, reports, comparisons), and the Review Responder systematically works through unreplied reviews across all your locations with appropriate tone for each rating level.

---

## v0.6.0 (2026-02-18)

### Initial Release

**Everything you need to manage Google Business Profiles from Claude Code.**

The first release of the Local SEO Pro plugin brings a complete management suite for agencies, freelancers, and multi-location brands.

**10 skills** that activate when you ask naturally:
- Audit and optimize your Google Business Profile with SEO scoring
- Respond to customer reviews individually or in bulk with AI-generated, tone-appropriate replies
- Track keyword rankings and monitor your local search visibility
- Create, schedule, and publish posts to keep your profile active
- Build and customize landing pages and store locators
- Analyze search traffic to understand how customers find you
- Generate branded PDF reports and email them to clients
- Scan and manage business citations across online directories
- View performance analytics with regional and device breakdowns
- Navigate multi-workspace setups and manage accounts and subscriptions

**11 slash commands** for quick actions:
- `/setup-mcp` and `/setup-branding` to get started
- `/daily-ops`, `/weekly-ops`, `/monthly-ops` for operational routines
- `/seo-audit`, `/respond-reviews`, `/rank-check`, `/citation-scan`, `/quick-post`, `/performance` for on-demand tasks

**2 autonomous agents** that handle complex multi-location workflows:
- Workspace Orchestrator for cross-location bulk operations
- Review Responder for systematic review management

**Built for agencies:** Multi-workspace support, per-client branding, scope confirmation before every operation, and white-label PDF reports.
