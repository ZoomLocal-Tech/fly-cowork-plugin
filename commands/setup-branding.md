---
description: Configure white-label branding for reports and emails
allowed-tools: Read, Write, Edit
argument-hint: [brand-name]
---

Configure white-label branding that will be applied to all reports, emails, and generated content. This branding ensures all client-facing output carries the agency's, freelancer's, or brand's identity — not Fly's.

## Step 1: Collect Branding Details

Ask the user for the following information. Present as a checklist and collect each item:

1. **Brand / Agency / Company Name** — the name to display on all reports and emails (e.g., "Digital Growth Agency")
2. **Logo URL** — a publicly accessible URL to the logo image (PNG or SVG preferred, minimum 200x200px). This will appear on PDF reports and email headers.
3. **Website URL** — the agency/brand website (e.g., "https://www.digitalgrowth.com")
4. **Contact Email** — the reply-to email address for client communications (e.g., "hello@digitalgrowth.com")
5. **Brand Color** (optional) — primary brand hex color for report accents (e.g., "#2563eb")
6. **Tagline** (optional) — a short tagline or descriptor shown under the logo (e.g., "Your Local SEO Partner")
7. **Footer Text** (optional) — custom text for report and email footers (e.g., "Powered by Digital Growth Agency | www.digitalgrowth.com")

If $ARGUMENTS contains a brand name, use it as the Brand Name and ask for the remaining details.

## Step 2: Confirm Configuration

Present all collected details back to the user in a clear summary:

```
White-Label Branding Configuration
===================================
Brand Name:    Digital Growth Agency
Logo URL:      https://example.com/logo.png
Website:       https://www.digitalgrowth.com
Contact Email: hello@digitalgrowth.com
Brand Color:   #2563eb
Tagline:       Your Local SEO Partner
Footer:        Powered by Digital Growth Agency | www.digitalgrowth.com
```

Ask: **"Does this look correct? Any changes?"**

## Step 3: Save Configuration

Save the branding configuration to the plugin's config file:

Write a JSON file at `${CLAUDE_PLUGIN_ROOT}/config/branding.json` with the structure:

```json
{
  "brand_name": "Digital Growth Agency",
  "logo_url": "https://example.com/logo.png",
  "website_url": "https://www.digitalgrowth.com",
  "contact_email": "hello@digitalgrowth.com",
  "brand_color": "#2563eb",
  "tagline": "Your Local SEO Partner",
  "footer_text": "Powered by Digital Growth Agency | www.digitalgrowth.com"
}
```

## Step 4: Per-Workspace Branding (Optional)

If the user manages multiple brands/clients across different workspaces, ask:

**"Do you want different branding per workspace (e.g., different logo for each client), or one brand across everything?"**

- **Single brand for everything** → save as `config/branding.json` (done in Step 3)
- **Per-workspace branding** → save as `config/branding-{workspace-name}.json` for each workspace, collecting details per workspace. Also save a default `config/branding.json` as the fallback.

## Step 5: Confirm & Next Steps

Confirm the configuration is saved and explain:

- All reports generated via `/monthly-ops`, `/weekly-ops`, and `/daily-ops` will use this branding
- PDF reports will include the logo, brand name, and footer
- Emails sent to clients will use the contact email as reply-to and include branding
- The branding can be updated anytime by running `/setup-branding` again

## How Other Commands Use This Config

When any command or skill needs to generate a report or send an email:
1. Read `${CLAUDE_PLUGIN_ROOT}/config/branding.json` (or the workspace-specific variant)
2. Include the brand_name in report headers instead of "Fly Agent"
3. Include the logo_url in PDF report headers and email templates
4. Use brand_color for accent elements
5. Apply footer_text to all report footers and email signatures
6. Use contact_email as the reply-to for client emails
7. Include website_url in report footers
