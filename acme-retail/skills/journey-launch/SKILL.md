---
name: acme-journey-launch
description: Workshop skill for launching CDP journeys against the Acme Retail account. Covers the full pipeline — segment authoring, journey YAML, email template prep, activation wiring, and push — with known-good connector configs, syntax fixes for common validation errors, and placeholder values for all fields that require real IDs.
type: project
---

# Acme Retail — Journey Launch Skill

Use this skill whenever building or pushing a CDP journey in the Acme Retail workshop environment. It documents every gotcha encountered in production and provides copy-paste-ready patterns.

---

## Account Context

| Field | Value |
|---|---|
| Parent Segment | `Acme Retail` |
| Engage Workspace | `Acme Retail Test` |
| Engage Workspace ID | `019f22d3-ce5b-700c-8814-40e6b716ab7e` |
| TD Site | `us01` |

---

## Connector Catalog

There are **2 connections** in this account. Always use these exact names in `connection:` fields.

### `engage_studio` — Treasure Engage V1 (email)

Use for all email activations via Engage.

```yaml
connection: engage_studio
all_columns: true
run_after_journey_refresh: true
connector_config:
  campaign_type: email
  campaign_model: always_on
  workspace_id: "019f22d3-ce5b-700c-8814-40e6b716ab7e"
  always_on_campaign_id: "PLACEHOLDER_CAMPAIGN_ID"   # replace with real ID once campaign exists
```

> **Note:** `always_on_campaign_id` requires an existing Engage campaign. If no campaign has been created yet, use the placeholder string — the journey will validate and push in draft state, but won't send until a real ID is set.

### `sms_and_push_system` — Google Sheets (SMS / Push export)

Use for SMS and push notification activations. Writes audience rows to a Google Sheet, which the downstream SMS/push platform reads.

**For Push:**
```yaml
connection: sms_and_push_system
all_columns: true
run_after_journey_refresh: true
connector_config:
  spreadsheet_title: "PLACEHOLDER_CAMPAIGN_NAME Campaign"
  sheet_title: "Push Recipients"
  mode: append
```

**For SMS:**
```yaml
connection: sms_and_push_system
all_columns: true
run_after_journey_refresh: true
connector_config:
  spreadsheet_title: "PLACEHOLDER_CAMPAIGN_NAME Campaign"
  sheet_title: "SMS Recipients"
  mode: append
```

> Replace `PLACEHOLDER_CAMPAIGN_NAME` with your campaign name (e.g. `"Everything Is Free Campaign"`). Both push and SMS can share one spreadsheet with different `sheet_title` values.

---

## Placeholder Values — Workshop Use

When a real ID or value isn't available, use these strings. They allow the journey to validate and push to draft without errors:

| Field | Placeholder |
|---|---|
| `always_on_campaign_id` | `"PLACEHOLDER_CAMPAIGN_ID"` |
| `spreadsheet_title` | `"PLACEHOLDER_CAMPAIGN_NAME Campaign"` |
| `email_sender_id` | `"00000000-0000-0000-0000-000000000000"` |
| `segment` reference | use an existing embedded segment name |

---

## Segment Authoring — Known Syntax Fixes

### Behavior conditions — use `type: Value`, NOT `type: Behavior`

`type: Behavior` passes local validation but is **rejected by the journey API**. Always write behavior conditions as:

```yaml
# CORRECT
- type: Value
  attribute: ""          # empty string — required
  source: behavior_enriched_ecomm_orders
  operator:
    type: GreaterEqual
    value: 1
  aggregation:
    type: Count
  timeWindow:
    type: withinPast
    value: 7
    unit: day

# WRONG — will fail journey push
- type: Behavior
  source: behavior_enriched_ecomm_orders
  operator:
    type: GreaterEqual
    value: 1
```

### Behavior filter syntax — wrap in `And` group

When filtering a behavior by a column value (e.g. `is_unsubscribe = 1`), the filter must be wrapped in a `type: And` group with `type: Column` conditions inside:

```yaml
# CORRECT
filter:
  type: And
  conditions:
    - type: Column
      column: is_unsubscribe
      operator:
        type: Equal
        value: 1

# WRONG — will fail with JOURNEY_SCHEMA_ERROR
filter:
  type: Column
  column: is_unsubscribe
  operator:
    type: Equal
    value: 1
```

### Available behavior sources

| Source key | Display name |
|---|---|
| `behavior_enriched_ecomm_orders` | Online Orders |
| `behavior_enriched_pos_transactions` | In-Store Transactions |
| `behavior_enriched_mobile_app_events` | Mobile App Events |
| `behavior_enriched_email_clicks` | Email Engagements |
| `behavior_enriched_pageviews_summary` | Web Pageviews |

---

## Journey Flow Rules — Common Mistakes

### Condition waits: only use when branches do DIFFERENT things

If both the matched path and the timeout path lead to the same next step, use a **duration wait** instead. A condition wait where both paths converge on the same step produces `BRANCH_DIRECTLY_TO_MERGE` warnings and is semantically a duration wait anyway.

```yaml
# Use this when both outcomes (purchased / timed out) just move on
- type: wait
  name: Wait 5 Days
  next: Next Step
  with:
    duration: 5
    unit: day

# Only use condition wait when each path does something different
- type: wait
  name: Wait for Purchase
  with:
    condition:
      segment: campaign_purchase
      next: Thank You Email      # different action
      timeout:
        duration: 5
        unit: day
        next: Discount Offer     # different action
```

### Condition wait convergence requires a Merge

When a condition wait's paths converge (each does something different, then rejoin), they must meet at a **Merge** step before End:

```yaml
- type: wait
  name: Wait for Purchase
  with:
    condition:
      segment: campaign_purchase
      next: Thank You Email
      timeout:
        duration: 5
        unit: day
        next: Discount Offer

- type: activation
  name: Thank You Email
  next: Merge Post-Wait
  with:
    activation: thank-you-email

- type: activation
  name: Discount Offer
  next: Merge Post-Wait
  with:
    activation: discount-email

- type: merge
  name: Merge Post-Wait
  next: End Stage
```

---

## Email Templates — CSS Must Be Inlined

Engage strips `<style>` blocks from the `<head>`. All CSS must be **inline** on each element before pushing.

Use `juice` to inline automatically:

```bash
npx juice your-email.html your-email-inlined.html
```

Then reference the inlined file in your template YAML:

```yaml
html_file: "your-email-inlined.html"
```

> The Google Fonts `@import` warning from juice is expected and harmless — email clients don't load web fonts. Arial fallback applies.

---

## Full Pipeline Checklist

Run these steps in order for every journey launch:

```bash
# 1. Pull parent segment (sets context for all commands)
tdx sg pull "Acme Retail" --yes

# 2. Inline CSS on any email HTML files
npx juice email.html email-inlined.html

# 3. Validate and push Engage templates
tdx engage template validate templates/acme-retail-test/template.yaml
tdx engage template push templates/acme-retail-test/template.yaml --yes

# 4. Validate journey locally
tdx journey validate segments/acme-retail/journey.yml

# 5. Dry-run against API
tdx journey push segments/acme-retail/journey.yml --dry-run

# 6. Push
tdx journey push segments/acme-retail/journey.yml --yes
```

---

## Permission Requirements

Pushing journey activations requires the **`ACTIVATION_FULL`** permission on your TD account.

If you see:
```
HTTP 403: Activation Full Permission Required
ACTIVATION_FULL_REQUIRED
```

Ask your account admin to grant `ACTIVATION_FULL` in:
**TD Console → Account Settings → Users → [your user] → Permissions**

Permission changes take 1–2 minutes to propagate. Re-run the push after waiting.

---

## File Layout Convention

```
segments/acme-retail/
  my-journey.yml              # Journey YAML

templates/acme-retail-test/
  tdx.json                    # {"engage_workspace": "Acme Retail Test"}
  my-template.yaml            # Template YAML
  my-template.html            # Raw HTML (for local preview)
  my-template-inlined.html    # Juice-inlined HTML (reference in YAML)
```
