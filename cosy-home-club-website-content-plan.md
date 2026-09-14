# Cosy Home Club — website content plan

Status: draft v1. Items marked **TBC** are placeholders pending
confirmation (capacity numbers, the About page team/founder note, and
real legal copy) — do not treat these as final copy or launch content.
Price, billing, cancellation, discount, skip-a-month, shipping, returns
and contact method are all confirmed (see §3 and §6).

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

**Billing**: the first edition is charged at sign-up. Every edition after
that is charged automatically on the 16th of each month, for the
following month's edition, until cancelled — the 16th is both the
renewal-lock date and the charge date.

**Cancellation**: members can cancel at any time. To avoid being charged
for (and receiving) the following month's edition, cancellation must
happen before the 16th — after that, renewal has already locked in, the
charge has gone through, and the next box will still ship. This is not
"cancel anytime" in the sense of stopping the next shipment on demand;
copy must reflect the 16th cutoff exactly, and must never say "cancel
anytime" unqualified. Cancelling after the 16th does not refund the
edition that's already locked in and charged — that box still ships —
but it does stop billing for the edition after that.

**Shipping**: the UK and Ireland only.

**Returns**: no returns offered. Members are encouraged to share
feedback instead — if unhappy with a piece, contact
`hello@cosyhomeclub.co.uk`.

**Contact**: email only (`hello@cosyhomeclub.co.uk`), no contact form.

**Discount**: no multi-month or subscription-length discount. New
members get 10% off their first box with the code `WELCOME10`.

**Skipping a month**: not currently offered. The workaround is to cancel
before the 16th and resubscribe whenever ready to start again — this is
not a formal "skip" feature and shouldn't be described as one.

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

**Purpose**: introduce the membership, and let people subscribe directly
from the page — not just funnel to the Shop page. See
`home-page-mockup.html` for layout reference.

Sections:
- Hero — Fraunces headline, one-line description, primary CTA anchoring
  down to the subscribe section
- Subscribe section — a condensed version of the product page: single
  teaser image, theme name/mood, category count, price, cadence line
  ("a brand new edition ships every month"), and the *same three-state
  logic* as the full product page (open/sold out/closed, including the
  no-reference-to-the-closed-edition rule). No accordion — a "see full
  details & how it works" link goes to the product page for that.
- How the cycle moves, condensed — the same 4-step strip as the product
  page (opens/closes/locks/ships), links to How membership works for
  the full breakdown
- Brand story snippet — short, warm, 2–3 sentences, links to About
- Trust / reassurance row — no long tie-in, delivered across the UK &amp;
  Ireland, links to the cancelling detail on How membership works rather
  than stating the 16th cutoff inline
- General newsletter signup ("stay in the loop") — always available,
  distinct in purpose from the state-driven "notify me" capture inside
  the subscribe section (sold out / closed states only)
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
- Pricing & billing — £34.99/month; first edition charged at sign-up,
  then automatically on the 16th of each month for the following
  month's edition, until cancelled; no multi-month discount, but
  `WELCOME10` gives 10% off a first box (see §3)
- Skip-a-month policy — not offered; cancel before the 16th and
  resubscribe when ready is the only way to miss an edition (see §3)
- Cancellation — cancel any time; cancel before the 16th to stop the
  following month's charge and edition; cancelling after the 16th does
  not refund the box already locked in, but stops billing after that
  (see §3)
- Shipping — UK and Ireland only; delivery window in the first week of
  the month
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

**Purpose**: answer practical questions, reduce support load. See
`faq-page-mockup.html` for layout reference — category jump nav, an
accordion per question, and a contact CTA at the bottom.

All six categories are now fully confirmed (methodology for any future
unanswered question: mark it with a visible "answer pending" flag rather
than inventing copy, as this page did while pricing/shipping/returns
were still open):
- Ordering & the monthly cycle — cycle mechanics, sell-out behaviour
- Pricing & billing — £34.99/month, charged at sign-up then on the 16th
  of each month, no multi-month discount, `WELCOME10` for 10% off a
  first box
- Skipping / pausing / cancelling — no skip (cancel and resubscribe
  instead); cancel before the 16th to avoid the next charge; cancelling
  after the 16th bills and ships that locked-in box but not the one
  after
- Shipping & delivery — UK and Ireland only, ships first week of the
  month
- Returns — none offered; direct unhappy members to
  `hello@cosyhomeclub.co.uk` for feedback instead
- What's actually inside (mystery-rule-compliant answer — confirms the
  surprise, states category count only)

### 6.6 Contact

**Purpose**: simple contact path.

Sections:
- Email only, via `mailto:hello@cosyhomeclub.co.uk` — no contact form
- Response-time expectation (plain, no urgency language)
- Link back to FAQ for common questions

### 6.7 Legal (placeholders)

Stub pages with headings and "coming soon" or lorem-structure content
until real legal copy is supplied. Do not draft binding legal terms.

## 7. Open questions — confirm before finalising copy

- **Capacity numbers**: units per edition that trigger "sold out" state.
- **About page team/founder note**: any bio or "who's behind this"
  content, or leave it out entirely.
- **Legal pages**: real copy for terms, privacy, shipping & returns, and
  subscription terms (placeholders only for now, not blocking).
