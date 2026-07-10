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
