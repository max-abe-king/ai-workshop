
Skill — acme-retail-brand-guide

Page
1
/
1
100%
"Data Classification" label was auto-applied to this file and set to "Internal Use"
---
name: acme-retail-brand-guide
description: Use when writing, reviewing, or checking any marketing creative for Acme Retail. Loads the full Acme Retail brand system — voice, tone, color palette, typography, logo usage, button styles, offer conventions, and CTA rules. Triggers on: "write copy for Acme Retail", "brand guide", "is this on brand", "check this copy", "Acme Retail creative", "write an email for Acme", "acme brand voice", "acme colors", "acme logo", or any request to generate or review Acme Retail marketing assets.
---

# Acme Retail Brand Guide

Acme Retail is a US-based mid-market retailer. Apply this full brand system to all marketing creative. Load this guide before writing any asset.

> **For business context, customer data, and segment definitions, also load the `acme-retail-knowledge` skill.**

---

## Brand Overview

**Full name:** Acme Retail, Inc.
**Tagline:** America's Home Store
**Founded:** 1987
**Headquarters:** 450 Commerce Blvd, Suite 100, Austin, TX 78701
**Currency:** USD — always write as "$" (e.g. "$50", "$12.40 off")
**Language:** US English — "shipping" not "postage", "cart" not "basket", "zip code" not "postcode"

---

## Color System

Split-complementary palette. Navy anchors trust. Teal bridges to modern/fresh. Aqua is the CTA accent — high contrast, used sparingly at decision points only. Driftwood warm neutral prevents the cool triad from reading as cold.

| Name | Hex | Role | Usage |
|---|---|---|---|
| Midnight Navy | #0F2742 | Primary | Headers, nav, footer, hero backgrounds — 60% of visual weight |
| Pacific Teal | #0A7C82 | Secondary | Section headers, loyalty, links, supporting UI — 30% of visual weight |
| Aqua | #13B8C4 | CTA Accent | Buttons, active states, highlights — 10% only, at decision points |
| Driftwood | #F2EDE4 | Warm Canvas | Email background, card surface, page canvas |
| Graphite | #2D3748 | Body Text | All paragraph copy, secondary UI |
| Mist | #D6EEF0 | Cool Surface | Dividers, secondary panels, loyalty strips, hover states |

**60/30/10 rule:** Navy dominates, Teal supports, Aqua appears only at decision points. Overusing Aqua dilutes its urgency signal.

**Never:** place Aqua on Teal, use more than three palette colors in a single asset, or introduce off-palette colors.

---

## Logo & Wordmark

**Construction:**
- Square Navy icon (#0F2742) with white serif "A" inside
- Small Aqua dot (#13B8C4) at bottom-right corner of the icon
- Wordmark: "ACME" in Midnight Navy, "RETAIL" in Pacific Teal
- Tagline beneath: "America's Home Store" in Aqua, uppercase, tracked

**Light usage:** Navy wordmark + Teal "RETAIL" on Driftwood or white backgrounds

**Dark usage:** White "ACME" + Aqua "RETAIL" on Navy backgrounds. Icon block shifts to Pacific Teal.

**Never:** stretch, recolor, separate the icon from the wordmark, or place on a background with insufficient contrast.

---

## Typography

| Role | Typeface | Weight | Notes |
|---|---|---|---|
| Display / H1 | Georgia | Bold 700 | Serif — emotive, established, trustworthy. Headlines and hero copy only. |
| Body | Inter | Regular 400 | Geometric sans — clean, readable at all sizes. All paragraph copy. |
| CTA / Label | Inter | SemiBold 600 | Uppercase, 0.08–0.10em letter-spacing. Buttons, tags, labels. |

---

## Button Styles

- **Border radius:** 8px
- **Height:** minimum 44px (tap target)
- **Font:** Inter SemiBold, uppercase, 0.08em tracking
- **Padding:** 24px horizontal, 12px vertical

| Style | Background | Text | Use |
|---|---|---|---|
| Primary | Aqua #13B8C4 | White | Main CTA — one per email/screen |
| Secondary | Pacific Teal #0A7C82 | White | Supporting actions |
| Deep | Midnight Navy #0F2742 | White | Navigation-level actions |
| Ghost | Transparent + Navy border | Navy | Secondary links, soft CTAs |

---

## Brand Voice

Warm, direct, and unpretentious. Write like a knowledgeable friend — not a salesperson. Enthusiastic about products without being pushy. Honest about value without being discount-obsessed.

### Tone by Situation

| Situation | Tone |
|---|---|
| Re-engagement | Warm and light. Acknowledge the gap without guilt-tripping. |
| Promotional | Energetic but grounded. Lead with the value, not the mechanics. |
| Loyalty | Appreciative and personal. Make the customer feel recognized, not marketed to. |
| Urgency | Honest scarcity only. Never manufacture urgency that isn't real. |

### Voice Do's

- Use the customer's first name once — in the subject line or opening line, not both
- Lead with the benefit, not the product
- Use active verbs: discover, grab, claim, explore
- Keep sentences short. One idea per sentence.
- Be specific — "20% off your next order" beats "great savings await"
- Express points value in dollars — "1,240 points — $12.40 toward your next order"

### Voice Don'ts

- Never use: "Don't miss out", "Act now", "Limited time only" as standalone CTAs
- No exclamation marks in subject lines
- No passive voice in CTAs
- Don't stack more than two offers in one message
- Never guilt-trip or pressure the customer
- Never use British English (no "colour", "favourite", "whilst", "postage")

---

## Offer Conventions

| What | Write this | Not this |
|---|---|---|
| Discounts | 20% off | Save 20% / 20% discount |
| Free shipping | Free shipping | Free delivery / Free P&P |
| Points balance | 1,240 points | 1200pts / 1.2K points |
| Points as value | $12.40 toward your next order | 1240 points redeemable |
| Cashback | $10 cashback | $10 back |
| Minimum spend | Orders over $50 | Spend $50 or more |

---

## CTA Patterns

**Primary CTA** — action + object, 4 words maximum, uppercase:
- "CLAIM YOUR OFFER"
- "SHOP ELECTRONICS"
- "SEE WHAT'S BACK"
- "EXPLORE THE RANGE"

**Secondary CTA** — softer, mixed case, optional:
- "Browse the range"
- "Find out more"

**Never use:** "Click here", "Buy now", "Shop now" as standalone CTAs, or any CTA over 4 words.

---

## Compliance Check

After writing any asset, check each element against this guide and present a pass/flag table before delivering the final output:

| Asset | Element | Status | Note |
|---|---|---|---|
| Email | Subject line | Pass/Flag | reason if flagged |
| Email | CTA text | Pass/Flag | reason if flagged |
| Email | Offer language | Pass/Flag | reason if flagged |
| SMS | Character count | Pass/Flag | reason if flagged |
| SMS | Opt-out present | Pass/Flag | reason if flagged |
| Push | Title standalone | Pass/Flag | reason if flagged |

Fix all flagged items before presenting the final output.
Displaying Skill — acme-retail-brand-guide.
