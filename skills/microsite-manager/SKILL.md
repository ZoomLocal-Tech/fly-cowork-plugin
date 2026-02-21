---
name: microsite-manager
description: >
  This skill should be used when the user asks about "microsite",
  "landing page", "create a website", "store locator", "subdomain",
  "customize my site", "change theme", "site sections", "custom domain",
  "microsite analytics", "SEO settings for my site", or needs help
  managing Fly-powered microsites and landing pages.
version: 0.1.0
---

# Microsite Manager

Create, customize, and manage Fly-powered landing pages and store locators. Includes theming, section management, SEO optimization, custom domains, and analytics.

## Multi-Location Awareness

1. Establish context with workspaces/locations
2. For workspace-wide microsite overview, use `mcp__fly-agent__list_all_microsites`
3. For workspace-wide analytics, use `mcp__fly-agent__get_workspace_analytics`
4. Store locators are workspace-level (showing all locations on a map)

## Workflow: Create a Microsite

### Landing Page (Single Location)
1. **Check subdomain** — call `mcp__fly-agent__check_subdomain` with desired subdomain name
2. **Create subdomain** — call `mcp__fly-agent__create_microsite_subdomain` with subdomain and subdomain_type "landing"
3. **Generate content** — call `mcp__fly-agent__generate_microsite` with optional template to create the SEO-optimized landing page
4. Present the microsite URL and offer customization options

### Store Locator (Multi-Location)
1. **Check subdomain** — call `mcp__fly-agent__check_subdomain`
2. **Create store locator** — call `mcp__fly-agent__create_store_locator` with subdomain
3. **Configure map** — call `mcp__fly-agent__configure_map` with map_style (roadmap, satellite, terrain, hybrid), default_zoom, enable_search, enable_filters
4. **Set card template** — call `mcp__fly-agent__set_card_template` with template (default, compact, detailed)

### Auto-Create for All Locations
Call `mcp__fly-agent__auto_create_all_subdomains` to automatically create microsites for all locations that don't have one yet.

## Workflow: Theme & Styling

### Set Base Theme
Call `mcp__fly-agent__set_theme` with theme: light, dark, green, blue, purple, high-contrast, night-mode, or inverted.

### Customize Theme
Call `mcp__fly-agent__customize_microsite_theme` with:
- `primary_color`: hex color (e.g., "#3b82f6")
- `secondary_color`: hex color
- `font_family`: "Inter", "Roboto", "Open Sans", etc.
- `template_name`: Modern, Classic, Minimal, Bold, Elegant, Restaurant, Healthcare, Retail, Service

### Apply Style Modifiers
Call `mcp__fly-agent__apply_styles` with:
- `borders`: sharp, rounded, minimal, bold, chunky
- `density`: ultra-compact, comfortable, spacious
- `animation`: reduced-motion, fast-motion, bouncy, smooth
- `elevation`: flat, material, neumorphism
- `size`: compact, large, xlarge

### Apply Theme Across All Locations
Call `mcp__fly-agent__apply_theme_everywhere` with theme name for brand consistency.

### Reset Theme
Call `mcp__fly-agent__reset_microsite_theme` to return to default light theme.

### View Templates
Call `mcp__fly-agent__list_landing_page_templates` with optional category ("general" or "industry") to see available templates.

## Workflow: Section Management

### View Current Sections
Call `mcp__fly-agent__get_section_status` to see which sections are enabled/disabled.

### Toggle Individual Section
Call `mcp__fly-agent__toggle_section` with section name and visible (true/false).
Available sections: hero, services, gallery, reviews, posts, blogs, products_services, contact, appointment, social.

### Configure Multiple Sections
Call `mcp__fly-agent__configure_sections` with comma-separated list of sections to SHOW (all others hidden). E.g., "hero,reviews,contact,services".

### Update Section Content
- **Hero section** — call `mcp__fly-agent__update_hero` with title, description, background_image
- **Other sections** — call `mcp__fly-agent__update_section` with section name, heading, description

## Workflow: SEO Settings

1. **Basic SEO** — call `mcp__fly-agent__update_seo` with title (50-60 chars), description (150-160 chars), keywords (comma-separated)
2. **Geographic SEO** — call `mcp__fly-agent__update_geo_seo` with placename, region code (e.g., "IN", "US"), coordinates
3. **Business SEO** — call `mcp__fly-agent__update_business_seo` with business_name, business_type, phone, email

## Workflow: Custom Domain

1. **Setup** — call `mcp__fly-agent__setup_custom_domain` with domain (e.g., "www.mybusiness.com"). Returns DNS configuration instructions
2. **Check status** — call `mcp__fly-agent__get_custom_domain_status` to see verification state and DNS records needed
3. **Verify** — call `mcp__fly-agent__verify_custom_domain` after user configures DNS to check if records are correct
4. **Remove** — call `mcp__fly-agent__remove_custom_domain` with domain name or domain_id to disconnect

## Workflow: Microsite Management

- **View info** — `mcp__fly-agent__get_microsite_info` for URL, status, theme, config
- **Enable/disable** — `mcp__fly-agent__toggle_microsite` with is_active true/false
- **Change subdomain** — `mcp__fly-agent__change_subdomain` with new_subdomain
- **Editor link** — `mcp__fly-agent__get_microsite_editor_link` for web-based editing
- **List all** — `mcp__fly-agent__list_all_microsites` for workspace-wide view

## Workflow: Microsite Analytics

- **Single location** — call `mcp__fly-agent__get_microsite_analytics` with days (7, 30, or 90)
- **All locations** — call `mcp__fly-agent__get_workspace_analytics` for aggregate metrics

## Data Freshness & Refresh Cadence

- Microsite analytics are tracked in real-time — visitor data, page views, and conversion metrics update continuously.
- **GBP Profile data** (which populates microsite content) refreshes **daily**.
- After updating microsite content, sections, or theme → the changes take effect immediately on the live site.
- After setting up a custom domain → DNS propagation takes 24-48 hours; verify after that window.
- **Follow-up triggers**:
  - After creating a microsite → check analytics after 7 days to establish a baseline for traffic and conversions
  - After theme/content changes → compare analytics week-over-week to measure impact
  - Monthly → review microsite analytics as part of `/monthly-ops` to identify optimization opportunities

## Quantifiable Outcomes & KPIs

Every microsite action should connect to lead generation and brand presence:

| KPI | What to Show | Business Impact |
|-----|-------------|-----------------|
| Page Views | Total visits to the microsite | Measures additional web presence beyond GBP |
| Unique Visitors | Distinct visitors | Actual reach of your landing page |
| Conversion Actions | Calls, directions, form fills from microsite | Direct leads generated by the microsite |
| Conversion Rate | Actions / Visitors × 100 | How well the microsite converts visitors to leads |
| Bounce Rate | Single-page exits | High bounce = content or UX needs improvement |
| SEO Score (Microsite) | On-page SEO completeness | Better SEO = more organic traffic over time |
| Custom Domain Status | Active and verified | Custom domains build brand credibility and trust |
| Store Locator Usage | Map interactions + location clicks | For multi-location: shows which locations draw interest |

## Action-to-Outcome Funnel

After every microsite operation, guide toward measurable improvements:

1. **No microsite yet** → "You're missing an owned web presence. A microsite creates an additional lead-generation channel beyond your GBP listing." → Create one now.
2. **Low page views** → "Your microsite isn't getting traffic. Improve SEO settings, share the link in your GBP profile, and add it to your review generator page."
3. **High views but low conversions** → "Visitors aren't converting. Add prominent CTAs (call button, direction link), enable the contact section, and ensure your phone number is clickable."
4. **No custom domain** → "A custom domain builds brand credibility. Set one up to make your microsite look professional."
5. **Sections disabled** → "You have valuable sections turned off (reviews, services, gallery). Enabling them provides more reasons for visitors to engage."
6. **Store locator not set up** → "For multi-location brands, a store locator helps customers find their nearest location — reducing friction and driving foot traffic."
7. **Post-setup** → "Check back in 7 days via microsite analytics to see your traffic baseline. Then optimize based on what sections get the most engagement."

**Always end with a "Microsite Health Summary"**: live status, visitor trend, conversion rate, and the best action to drive more leads from the site.

## Shareable Link Fallbacks

When the user wants to configure their microsite manually in the web UI, use `mcp__fly-agent__generate_shareable_link`:

| link_type | When to offer |
|-----------|---------------|
| `microsite` | User wants to visually configure microsite settings, design, and sections |

**Always try the agentic approach first** (e.g., `set_theme`, `update_hero`, `toggle_section`, `update_seo`). Only offer the microsite link if the user prefers the visual editor or wants to preview changes live.
