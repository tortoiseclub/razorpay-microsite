# Design Spec: Razorpay Employee Benefit Microsite — Device Leasing (Powered by Tortoise)

> Note: Brand guidelines and the visual system (colors, typography, tokens) are provided separately in Claude Design. This spec covers structure, content, behavior, and logic only. Where this spec says "primary", "accent green", "muted", etc., map those to the provided brand system.

## 1. Overview

Razorpay runs an internal employee benefits portal. Each month one benefit is featured via a dedicated microsite. This month's featured benefit is **Tortoise's Device Leasing Program**.

Build a **single-page, fully responsive microsite** that explains the benefit to Razorpay employees. This is an **internal education page, not a marketing landing page** — the audience is already eligible. The goals, in order:

1. Explain the benefit simply (what it is, how it works, what's included).
2. Let employees **play with an interactive savings calculator** and see what a device would really cost them.
3. Build trust (insurance clarity, honest math, FAQs).
4. Drive them to the two live events and the "Browse Devices" action.

Tone: warm, plainspoken, employee-first — "here's a perk you already have" — never salesy.

No stock photos and no real brand logos. Use abstract device-mockup shapes, simple line icons, or tasteful illustration.

---

## 2. Page Structure (in order)

### 2.1 Header (sticky)
- Left: Razorpay wordmark + "Powered by **TORTOISE**" lockup.
- Nav links (anchor-scroll): Browse Devices · Savings Calculator · How It Works · Insurance · FAQs · Events.
- Right: primary button **"Apply Now"**.
- Mobile: logo + hamburger; nav collapses into a sheet.

### 2.2 Hero
- Headline: **"Upgrade today."** / **"Pay over time."**, stacked, with the second line in the primary brand color.
- Subhead: "Get your next smartphone, laptop or tablet through Razorpay's Device Leasing Program, powered by Tortoise."
- Three proof chips with line icons: `12 easy salary deductions` · `Insurance included` · `Tax savings of up to 30%*`.
- Circular badge, top-right: "SAVE UP TO **30%*** ON YOUR DEVICE".
- Two event callouts (compact, icon + label + date): **Live Webinar — 24 July** · **Experience Booth — 28 July**.
- CTAs: **"Browse Devices"** (primary) and **"Calculate Your Savings"** (secondary, smooth-scrolls to the calculator, §2.4).
- Right side: abstract device cluster illustration (laptop, phone, tablet, watch silhouettes).

### 2.3 Four benefit cards (equal-width row; 2×2 on tablet; stacked on mobile)
1. **Save up to 30%** — "Enjoy tax savings based on your income tax slab with salary deductions."
2. **12-Month Plan** — "No large upfront payment. Simply spread the cost over 12 monthly deductions."
3. **Insurance Included** — "Comprehensive protection against accidental damage, liquid damage and theft."
4. **Delivered to You** — "Choose your device. Complete your application. We'll handle the rest."

### 2.4 Interactive Savings Calculator — THE CENTERPIECE
Full spec in §3. Anchored `#calculator`. Sits on a subtly tinted panel that sets it apart from the page background, with heading **"How much can you save?"** and sub "Your savings depend on your income tax slab."

### 2.5 How it works
Heading: **"How it works"**. Horizontal 6-step timeline (numbered circles with icons, connecting line). Vertical timeline on mobile.
1. **Choose** — "Browse from a curated range of premium devices."
2. **Apply** — "Complete a quick and fully digital application."
3. **Approval** — "Your application goes through the approval workflow."
4. **Delivery** — "Your device is delivered to your preferred address."
5. **Salary Deductions** — "12 monthly salary deductions. Hassle-free and convenient."
6. **End of Lease** — "Own your device with a token ₹1 buyback."

### 2.6 Everything is included
Heading: **"Everything is included"**. 3×2 icon grid (2×3 on mobile): Accidental Damage · Liquid Damage · Theft Protection · Manufacturer Warranty · Doorstep Claim Assistance · Cashless Repair Process.

### 2.7 Why lease instead of buying?
Comparison table, two columns: **Buying** vs **Device Leasing** (leasing column visually emphasized — highlighted header and tinted background).

| Row | Buying | Device Leasing |
|---|---|---|
| Payment | Pay full amount today | Pay monthly over 12 months |
| Upfront Cost | Large upfront expense | No large upfront payment |
| Insurance | Buy insurance separately | Insurance included |
| Pricing | Retail pricing | Corporate pricing (wherever applicable) |
| Ownership | Yours on day one | Yours at lease end for just ₹1 |
| Cash Flow | One-time cash outflow | Better cash flow management |

Interaction: on row hover, the leasing cell brightens slightly (see §5).

### 2.8 Top brands
Heading: **"Top brands. Premium devices."** Text-placeholder logo strip: Apple · Samsung · Google Pixel · Dell · HP · Lenovo · Asus · OnePlus · Mi. Render as neutral text/wordmark placeholders — **do not draw real logos**. CTA below: **"Browse Catalogue →"**.

### 2.9 Insurance
Heading: **"Insurance that has you covered"**, sub "Comprehensive protection for complete peace of mind."
Two lists side by side:
- **Covered** (positive ✓): Accidental damage · Liquid damage · Theft · Mechanical breakdown (manufacturer warranty)
- **Not covered** (muted ✕): Normal wear & tear · Intentional damage · Unauthorised repairs · Loss due to negligence

CTA: **"Read Insurance Guide"** (secondary). Right side: shield illustration.

### 2.10 Events (two cards)
- **Live Webinar — 24 July.** Agenda list: How device leasing works · Tax savings · Insurance coverage · Application process · Live Q&A. CTA: **"Register Now"** (primary).
- **Experience Booth — 28 July.** "Visit the Tortoise Experience Desk to:" Explore devices · Compare models · Understand pricing · Get your questions answered · Apply on the spot. CTA: **"Visit Us"** (accent).

### 2.11 FAQs
Heading: **"Frequently Asked Questions"**. Accordion (one open at a time), 8 items in 2 columns desktop / 1 column mobile:
1. Is there any upfront payment?
2. How long is the lease?
3. Can I choose any device?
4. Is insurance included?
5. Is this available under the New Tax Regime?
6. How much can I save?
7. Can I repay early?
8. What happens if I leave Razorpay?

Write short, honest 2–3 sentence placeholder answers consistent with the rest of the page (e.g., for #1: no upfront payment, only ₹1 buyback at the end). CTA below: **"View All FAQs"** (ghost).

### 2.12 Final CTA banner
Full-width rounded banner in a strong brand treatment, light text.
Headline: **"Your next device is closer than you think."**
Sub: "Premium devices. Monthly payments. Insurance included. Tax savings up to 30%*."
Button: **"Browse Devices →"** (inverted: light background, brand-colored text).

### 2.13 Footer
"Powered by Tortoise — your trusted partner in device leasing." Links: Device Leasing Policy · Insurance Guide · Terms & Conditions · Privacy Policy · Contact Us.

---

## 3. Calculator Specification (do not simplify this math)

### 3.1 Configurable constants
Define once at the top of the code, clearly commented as configuration:

```js
const CONFIG = {
  TENURE_MONTHS: 12,       // lease tenure
  CESS: 0.04,              // 4% health & education cess applied on tax savings
  BUYBACK_AMOUNT: 1,       // flat ₹ amount to own the device at lease end (configurable)
  PRICE_MIN: 40000,
  PRICE_MAX: 250000,
  PRICE_DEFAULT: 100000,
  TAX_SLABS: [5, 10, 20, 30],
  TAX_SLAB_DEFAULT: 20,
};
```

### 3.2 Inputs
- **Device Price**: slider from `PRICE_MIN` to `PRICE_MAX`, step ₹5,000, default `PRICE_DEFAULT`, plus a synced editable number field above it. Slider endpoints labelled ₹40,000 and ₹2,50,000.
- **Your Tax Slab**: segmented control — 5% / 10% / 20% / 30% — default 20%. Active segment filled with the primary brand color.

### 3.3 Calculation (exact formulas)
```
salary_sacrifice  = device_price
monthly_deduction = salary_sacrifice / TENURE_MONTHS
tax_savings       = salary_sacrifice × (tax_slab / 100) × (1 + CESS)
buyback_amount    = BUYBACK_AMOUNT
effective_cost    = salary_sacrifice − tax_savings + buyback_amount
```
Round all displayed values to the nearest rupee. Effective cost must never render below ₹0.

Worked example (defaults): ₹1,00,000 device, 20% slab → monthly ₹8,333 · tax savings ₹20,800 · effective cost ₹79,201.

### 3.4 Outputs (three stat cards, live-updating)
1. **Monthly Deduction** — large stat number. Caption: "For 12 months".
2. **Estimated Tax Savings** — large stat number in the accent/savings color. Caption: "Incl. 4% cess".
3. **Effective Cost** — the hero number, largest of the three, on a subtly highlighted card. Caption: "What the device really costs you".

Below the cards, one transparent breakdown line in muted secondary text, small:
> ₹{salary_sacrifice} salary sacrifice − ₹{tax_savings} tax savings + ₹{buyback} buyback to own it

Disclaimer beneath: *"Illustrative calculation. Actual figures depend on your salary structure, applicable tax slab, and lease terms."*

CTA under panel: **"Calculate My Savings"** (accent) — on the microsite this scrolls-to/deep-links to the full calculator or application flow (placeholder link).

### 3.5 Number formatting
Indian digit grouping everywhere: ₹1,00,000, ₹8,333, ₹2,50,000. Tabular numerals so digits don't jump during animation.

### 3.6 Calculator states
| State | Behavior |
|---|---|
| Default | Defaults loaded, outputs pre-computed (never empty) |
| Dragging slider | Outputs update live on every frame; numbers animate (count-up ~250ms) |
| Manual price entry | Clamp to min/max on blur; sync slider position |
| Invalid/empty number field | Revert to last valid value on blur; never show NaN or ₹0 flash |
| Slab change | Animate savings + effective cost; brief positive pulse on the savings card |

---

## 4. Responsive Behavior

| Breakpoint | Changes |
|---|---|
| Desktop >1024px | Layout as specced; calculator = inputs left, outputs right |
| Tablet 768–1024px | Benefit cards 2×2; calculator stacks inputs above outputs; events cards remain side-by-side |
| Mobile <768px | Everything single-column; sticky header slims down; timeline goes vertical; comparison table becomes stacked cards or horizontally scrollable with sticky first column; outputs become a vertical stack with Effective Cost first |

Assume **many employees open this on mobile from an internal portal link** — mobile is a first-class experience, not a squeeze-down.

---

## 5. Motion

| Element | Trigger | Animation | Duration / Easing |
|---|---|---|---|
| Sections | Scroll into view | Fade + 16px rise, once | 400ms, ease-out |
| Calculator numbers | Input change | Count-up/down to new value | 250ms, ease-out |
| Savings card | Slab increase | Soft positive pulse | 300ms |
| Comparison table row | Hover | Leasing cell background brightens | 150ms |
| FAQ accordion | Toggle | Height + chevron rotate | 200ms, ease-in-out |
| Nav links / hero CTAs | Click | Smooth anchor scroll | native smooth |

Keep motion subtle and respectful of `prefers-reduced-motion` (disable count-ups and reveals; snap to final values).

---

## 6. Edge Cases

- **Price at min/max**: slider thumb stops cleanly; typed values clamp with no error toast needed.
- **Long copy**: FAQ answers and card copy should wrap gracefully; no truncation on this page.
- **JS disabled / slow load**: calculator panel shows default computed values as static text rather than an empty shell.
- **Effective cost floor**: never below ₹0 (mathematically can't happen at these slabs, but guard anyway).

---

## 7. Accessibility

- Full keyboard operation: slider (arrow keys, ±₹5,000 per press), segmented control (arrow keys within group), accordion (Enter/Space), logical focus order top-to-bottom.
- Slider: `role="slider"` with `aria-valuemin/max/now` and `aria-valuetext` announcing "₹1,00,000".
- Live outputs wrapped in `aria-live="polite"` region announcing the effective cost after input settles (debounced — not per animation frame).
- Segmented control: `role="radiogroup"` with labelled radios.
- Contrast: all text ≥ 4.5:1, including accent-colored stat numbers on light backgrounds.
- Touch targets ≥ 44×44px.

---

## 8. Copy Rules & Guardrails

- Keep hero claim at "up to 30%*" even though 30% slab + cess computes to 31.2% — do not "correct" the marketing copy to match the math.
- Always footnote savings claims with the asterisk → disclaimer.
- ₹1 buyback is a **feature** — mention it in step 6 of How It Works, in the comparison table, and in the calculator breakdown. Phrase as "own your device for just ₹1 at lease end."
- Indian English, INR only, Indian digit grouping.
- Never imply guaranteed savings; savings language always tied to "your income tax slab."

---

## 9. Out of Scope

- Real brand logos, stock photography, real employee data.
- Actual application flow, login, or backend integration — all CTAs are placeholder links/anchors.
- Per-device-type buyback variations, sponsorship, or input-tax-credit scenarios (the config constant exists so these can be changed later; do not build UI for them).
