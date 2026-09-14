# Cosy Home Club — website content plan

Status: draft v1. Items marked **TBC** are placeholders pending confirmation
(capacity numbers, skip-a-month policy) — do not treat these as final copy
or launch content. Price and cancellation terms are confirmed (see §3).

## 1. Overview

- **Brand**: Cosy Home Club — a UK monthly home-styling membership.
- **Commerce**: Shopify, headless — Storefront API only, no Shopify theme.
  Subscriptions run via Shopify selling plans.
- **Frontend**: Custom build on Hydrogen (Remix-based).
- **Voice**: warm, plain sentences, sentence case (not Title Case), no
  urgency or scarcity language, no exclamation-mark stacking.

## 2. Brand system (reference — apply exactly)

**Fonts** (Google Fonts)
- Fraunces — display / headlines (serif)
- Jost — body / UI (sans-serif)
- Cormorant Garamond italic — small accents only, used sparingly

**Colours**
| Token | Hex | Use |
|---|---|---|
| Cream | `#FAF6F0` | Page background |
| Stone | `#DCC9B6` | Secondary surfaces, cards |
| Latte | `#B98D75` | Accent, links, secondary buttons |
| Latte Deep | `#8C6A54` | Primary buttons, emphasis |
| Espresso | `#3A342E` | Body text, headings (never pure black) |
| Line | `#E4D9CB` | Borders, dividers |

## 3. The monthly cycle (core business logic)

Every edition follows a fixed monthly cycle:

1. **Opens** on the 1st of the month.
2. **Orders close** on the 15th.
3. **Renewal / demand-lock** on the 16th — renewals lock in for the
   *following* month's edition, and Cosy Home Club finalises stock and
   production against confirmed orders.
4. **Ships** in the first week of the following month.

**Price**: £34.99/month.

**Cancellation**: members can cancel at any time. To avoid receiving (and
being charged for) the following month's edition, cancellation must
happen before the 16th — after that, renewal has already locked in and
the next box will still ship. This is not "cancel anytime" in the sense
of stopping the next shipment on demand; copy must reflect the 16th
cutoff exactly, and must never say "cancel anytime" unqualified.

This cycle drives three distinct product states across the Shop and
product pages — never a simple "buy / sold out" binary:

### State 1 — Open (1st–15th, capacity remaining)
Normal purchase flow. Show the edition theme, mystery description, price,
capacity remaining (if surfaced), and the "join this edition" CTA.

### State 2 — Sold out (capacity reached before the 15th)
The current edition is no longer purchasable, even though the order
window hasn't technically closed. No purchase CTA. Copy should
acknowledge the edition is full and point to email capture for the next
one, without scarcity/urgency framing (state the fact plainly).

### State 3 — Closed between editions (16th – end of month)
The edition that just closed is unavailable, **and the copy must not
reference it** — no "sorry, the March edition is closed" framing. Instead
point forward to the next genuinely reachable edition (the 1st of the
next calendar month), with copy in this shape:

> This edition is now closed. The next edition opens on the 1st of
> [Month]. Pop your email below and we'll let you know the moment it's
> live.

Plus an email capture field.

**Implementation note**: state and "next reachable edition" month must be
computed from the current date server-side (or via Shopify
inventory/selling-plan data), not hardcoded.

## 4. Product contents — mystery rule

Never list specific product names or contents anywhere on the site,
including the product page. Describe only:
- The seasonal **theme** and **mood** (e.g. "a quiet, slow-mornings
  theme")
- The **category count** (e.g. "five considered pieces, one seasonal
  theme")

Actual contents are a surprise until delivery. This is deliberate, not an
omission — copy review should flag any accidental specificity.

## 5. Sitemap

1. Home (`/`)
2. Shop / current edition product page (`/products/[handle]`)
3. How membership works (`/how-it-works`)
4. About (`/about`)
5. FAQ (`/faq`)
6. Contact (`/contact`)
7. Legal (placeholder pages, real copy TBC):
   - Terms of service (`/legal/terms`)
   - Privacy policy (`/legal/privacy`)
   - Shipping & returns (`/legal/shipping-returns`)
   - Subscription/cancellation terms (`/legal/subscription-terms`)

## 6. Page-by-page requirements

### 6.1 Home

**Purpose**: introduce the membership, set the tone, funnel to the Shop
page (or to email capture if the edition is closed).

Sections:
- Hero — Fraunces headline, one-line description, primary CTA ("see this
  month's edition" or, in closed state, "join the waitlist")
- How it works, condensed (3-step summary, links to full page)
- Current edition teaser — theme name/mood only, respects state logic
  above, links to product page
- Brand story snippet — short, warm, 2–3 sentences, links to About
- Trust / reassurance row — no long tie-in, UK-based, links to the
  cancelling detail on How membership works rather than stating the
  16th cutoff inline
- Email capture (always available, not just in closed state)
- Footer nav to all pages + legal

### 6.2 Shop / product page

**Purpose**: the commerce page. Must fully implement the three-state
logic in §3. See `product-page-mockup.html` for layout reference.

Content per state:
- **Open**: theme name/mood, "five considered pieces, one seasonal
  theme"-style category count, price (£34.99/month), cadence note ("a
  brand new edition ships every month" — no cancellation detail inline;
  that lives in the cancelling subsection), capacity remaining if shown,
  primary CTA to subscribe via Shopify selling plan.
- **Sold out**: same theme framing, no CTA, plain "this edition is full"
  statement, email capture for next edition.
- **Closed between editions**: forward-looking copy per §3 exactly, email
  capture, no reference to the just-closed edition.

Supporting sections (all states): how the cycle works (short, links to
full page), what "five considered pieces" means without specifics,
shipping note, FAQ snippet (2–3 most relevant questions, links to full
FAQ).

### 6.3 How membership works

**Purpose**: explain the mechanics in full — the cycle, pricing logic,
skip-a-month policy, cancellation.

Sections:
- The monthly cycle, step by step (opens/closes/locks/ships, matching §3)
- Pricing — £34.99/month
- Skip-a-month policy — **TBC**, placeholder only, do not invent terms
- Cancellation — cancel any time; cancel before the 16th to stop the
  following month's edition (see §3)
- Shipping — UK-only assumed, confirm; delivery window in the first week
  of the month
- What you get each month — theme/mood/category-count framing only, no
  content specifics

### 6.4 About

**Purpose**: brand story, warm and plain, no corporate tone.

Sections:
- Origin story / why Cosy Home Club exists
- Values (considered, seasonal, no clutter — tone-match brand voice)
- Small team/founder note if applicable (**content TBC** — no bios
  drafted without input)

### 6.5 FAQ

**Purpose**: answer practical questions, reduce support load.

Suggested categories (content **TBC** pending skip-a-month policy
confirmation; pricing and cancellation are confirmed, see §3):
- Ordering & the monthly cycle
- Pricing & billing
- Skipping / pausing / cancelling
- Shipping & delivery
- Returns
- What's actually inside (mystery-rule-compliant answer — confirms the
  surprise, states category count only)

### 6.6 Contact

**Purpose**: simple contact path.

Sections:
- Contact form (name, email, message) or mailto — **method TBC**
- Response-time expectation (plain, no urgency language)
- Link back to FAQ for common questions

### 6.7 Legal (placeholders)

Stub pages with headings and "coming soon" or lorem-structure content
until real legal copy is supplied. Do not draft binding legal terms.

## 7. Open questions — confirm before finalising copy

- **Multi-month discount**: any discount for paying/committing across
  multiple months (price itself is confirmed at £34.99/month).
- **Capacity numbers**: units per edition that trigger "sold out" state.
- **Skip-a-month policy**: mechanics, deadline relative to the 15th
  cutoff, any limits per year.
- **Refunds on a locked order**: whether a member who cancels after the
  16th (once that month's renewal is locked) is entitled to a refund on
  the box that still ships, or only stops future renewals.
- **Shipping scope**: UK-only confirmed? Any excluded regions
  (Highlands/Islands, NI)?
- **Contact method**: form vs. mailto vs. both.
