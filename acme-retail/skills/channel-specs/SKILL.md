---
name: acme-retail-channel-specs
description: Use when writing or adapting Acme Retail marketing assets for specific channels — email, SMS, push notification, or in-app message. Loads character limits, structure rules, and cross-channel consistency guidelines. Triggers on: "write an email", "adapt for SMS", "push notification", "in-app message", "channel specs", "adapt this for all channels", "what are the character limits", or any request to produce or check a channel-specific Acme Retail asset.
---

# Acme Retail Channel Specs

Apply these limits and structure rules when writing or adapting any Acme Retail channel asset. Always load this alongside the acme-retail-brand-guide skill.

## Email

| Element | Limit | Notes |
|---|---|---|
| Subject line | 40 characters | Shorter performs better on mobile. Name or key benefit first. |
| Preheader | 85 characters | Adds context to subject — never repeats it. |
| Hero copy | 15 words max | One idea only. First thing read after the image. |
| Body copy | 3 paragraphs max | Max 2 sentences per paragraph. White space is your friend. |
| Primary CTA | 4 words max | Action + object format. |
| Secondary CTA | 4 words max | Optional. Only if there is a genuinely different second action. |

**Email structure:**
1. Subject line + preheader
2. Hero image
3. Hero copy (one-line payoff)
4. Body copy
5. Primary CTA
6. Optional secondary block + CTA

## HTML Email — Engage Compatibility Rules

Engage and most email clients strip everything inside `<head>` — including `<style>` blocks and CSS classes. A browser preview will look correct because browsers support `<style>` blocks, but the email will break in Engage and in Gmail, Outlook, and Apple Mail.

**The rule: every style must be written as an inline `style=""` attribute. No exceptions.**

### What to never do
```html
<!-- WRONG — <style> block will be stripped by Engage -->
<head>
  <style>
    .header { background-color: #0F2742; }
    .cta-button { background-color: #13B8C4; color: white; }
  </style>
</head>
<div class="header">...</div>
<a class="cta-button">CLAIM YOUR OFFER</a>
```

### What to always do
```html
<!-- CORRECT — inline style survives every email client -->
<div style="background-color: #0F2742; padding: 20px;">...</div>
<a style="background-color: #13B8C4; color: #ffffff; padding: 12px 24px; text-decoration: none; font-family: Inter, Arial, sans-serif; font-weight: 600; font-size: 14px; letter-spacing: 0.08em; border-radius: 8px; display: inline-block;">CLAIM YOUR OFFER</a>
```

### Required inline style rules

**Wrapper / canvas:**
```html
<table width="100%" cellpadding="0" cellspacing="0" border="0" style="background-color: #F2EDE4;">
  <tr><td align="center">
    <table width="600" cellpadding="0" cellspacing="0" border="0">
```
Always use `<table>` layout — `<div>` layout breaks in Outlook.

**Header block:**
```html
<td style="background-color: #0F2742; padding: 20px 24px;">
```

**Headline (Georgia serif):**
```html
<h1 style="font-family: Georgia, 'Times New Roman', serif; font-size: 28px; font-weight: 700; color: #0F2742; margin: 0 0 12px 0; line-height: 1.2;">
```

**Body copy (Inter/Arial):**
```html
<p style="font-family: Inter, Arial, sans-serif; font-size: 15px; font-weight: 400; color: #2D3748; line-height: 1.6; margin: 0 0 16px 0;">
```

**Primary CTA button:**
```html
<a href="#" style="display: inline-block; background-color: #13B8C4; color: #ffffff; font-family: Inter, Arial, sans-serif; font-size: 14px; font-weight: 600; letter-spacing: 0.08em; text-decoration: none; padding: 14px 28px; border-radius: 8px;">CLAIM YOUR OFFER</a>
```

**Loyalty / info strip:**
```html
<td style="background-color: #D6EEF0; padding: 12px 24px; font-family: Inter, Arial, sans-serif; font-size: 13px; color: #0F2742;">
```

**Footer:**
```html
<td style="background-color: #0F2742; padding: 20px 24px; text-align: center; font-family: Inter, Arial, sans-serif; font-size: 11px; color: #0A7C82;">
```

### Font stack rule
Always specify a web-safe fallback after Inter and Georgia — email clients may not load web fonts:
- Headlines: `Georgia, 'Times New Roman', serif`
- Body and CTAs: `Inter, Arial, Helvetica, sans-serif`

### Safe CSS properties for email
These work reliably across all clients:
`background-color`, `color`, `font-family`, `font-size`, `font-weight`, `line-height`, `padding`, `margin`, `text-align`, `text-decoration`, `letter-spacing`, `border-radius`, `width`, `max-width`, `display: inline-block`

### Avoid in email HTML
- `display: flex` or `display: grid` — not supported in Outlook
- `<div>` as layout wrapper — use `<table>` instead
- CSS shorthand `font:` or `border:` — expand to individual properties
- `background` shorthand — use `background-color` only
- External stylesheets or `@import`
- `class=` attributes — they will be ignored after `<head>` is stripped

### Compliance check addition
When reviewing HTML email output, add these checks to the pass/flag table:
- No `<style>` block present
- No `class=` attributes on any element
- All layout uses `<table>` not `<div>`
- All fonts have web-safe fallbacks
- CTA is an `<a>` tag with full inline styles, not a `<button>`

## SMS

| Element | Limit | Notes |
|---|---|---|
| Full message | 160 characters | Hard limit including opt-out. |
| Opt-out text | Always required | "Reply STOP to unsubscribe" = 26 chars, always at the end. |
| Usable message | 134 characters | After opt-out is accounted for. |
| Offer placement | First 60 characters | Lead with value before brand name. |

**SMS structure:**
1. Offer or hook (first 60 chars)
2. One supporting line or CTA
3. "Reply STOP to unsubscribe"

## Push Notification

| Element | Limit | Notes |
|---|---|---|
| Title | 50 characters | Must work standalone — body may be truncated. |
| Body | 100 characters | One supporting sentence. |
| Action button | 20 characters | Optional. Matches primary CTA pattern. |

## In-App Message

| Element | Limit | Notes |
|---|---|---|
| Headline | 30 characters | Bold, short, benefit-led. |
| Body | 75 characters | One sentence. Context or incentive. |
| CTA button | 20 characters | Action + object. Tied to in-app action available. |

## Cross-Channel Consistency Rules

- Core concept must be recognisable across all channels
- Offer must be identical across all channels — never vary the discount by channel
- CTA action should be consistent across channels
- Tone may vary (SMS = immediate, in-app = contextual) but voice stays the same
- Customer name — use in email and SMS, not in push or in-app

## Quick Reference

| Channel | Max length | Personalisation |
|---|---|---|
| Email | Use spec above | Name, product, offer |
| SMS | 160 chars total | Name, offer |
| Push | 150 chars total | Product, behaviour |
| In-app | 125 chars total | Behaviour, context |

## Output Format

When producing multi-channel assets, present them in this order with character counts:

**Email**
- Subject line: [text] ([n] chars)
- Preheader: [text] ([n] chars)
- Hero copy: [text]
- Body: [text]
- CTA: [text]

**SMS**
- Message: [text] ([n] chars including opt-out)

**Push**
- Title: [text] ([n] chars)
- Body: [text] ([n] chars)
- Action: [text] ([n] chars)

**In-App**
- Headline: [text] ([n] chars)
- Body: [text] ([n] chars)
- CTA: [text] ([n] chars)
