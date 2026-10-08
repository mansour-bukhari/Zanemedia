# Shopify Store Blueprint — onlykw.com

### Premium desserts, confectionery & edible gifting · Kuwait-first, GCC-ready

_Version 1.0 · 2026-10-08 · Companion to `COMPETITOR_PLATFORM_AND_UX_ANALYSIS.md`_

---

## 0. Architecture Principles

| # | Principle | Why (competitor evidence) |
|---|---|---|
| P1 | **Mobile in-app browser first.** Design and test in the Instagram/Snapchat webviews on a mid-range Android over 4G. | GCC dessert demand is paid-social-led. Every top regional player is mobile/app-first (Floward, Bleems, Crumbl). |
| P2 | **The delivery promise is a product attribute, not a banner.** Every SKU carries its fulfilment mode and lead time; the UI only promises what the cart can actually deliver. | Fantastic Chocolate's "90 min" banner vs "order ice-cream cakes a day ahead" is a trust leak. |
| P3 | **Native Shopify first, apps second.** Use Search & Discovery, Markets, Translate & Adapt, Shopify Functions discounts and native metafields/metaobjects before adding apps. Cap at **≤ 8 storefront-loading apps**. | Speed. Shopify stacks win on theme + few apps (Milk Bar, Magnolia, Salt & Straw). |
| P4 | **Phone number is the customer ID.** WhatsApp is the GCC's SMS. Capture the phone at every step and use it for tracking, loyalty and winback. | Salt & Straw phone-based loyalty; Floward/Bleems app tracking. |
| P5 | **Arabic is a first-class language**, not a translation layer. Arabic RTL is the default for Kuwaiti traffic; English LTR is secondary. | Ad copy, search queries and gifting notes are predominantly Arabic. |

### 0.1 Shopify plan decision

| Plan | Fit | Notes |
|---|---|---|
| **Grow** (recommended for MVP) | ✅ | Enough staff seats and reports. Delivery date, slot and gift data are captured in the **cart** (cart attributes), which works on every plan. |
| Advanced | Upgrade trigger: ~15K KWD+/month GMV | Lower third-party transaction fee; custom reports. |
| **Plus** | Phase 3+ only if needed | Unlocks Checkout UI extensions on the information/shipping/payment steps, custom-app Shopify Functions, B2B (corporate gifting catalogs) and the lowest third-party fee. |

> ⚠️ **Shopify Payments is not available in Kuwait.** All card/KNET payments run through a third-party gateway, so **Shopify's third-party transaction fee applies** on top of gateway fees. It decreases by plan tier (Basic highest → Plus lowest; verify current rates in Shopify admin). Model this into the plan decision.

---

## 1. Theme Selection & Tech Stack Architecture

### 1.1 Theme recommendation

**Primary pick: Prestige (Maestrooo, OS 2.0)**
**Fallback: Impulse (Archetype)**
**Budget/dev-heavy alternative: Dawn (free) + custom sections**

| Criterion (weight) | Prestige | Impulse | Symmetry | Dawn |
|---|---|---|---|---|
| High-end visual storytelling (25%) | ★★★★★ editorial layouts, image-with-text overlays, video sections, luxury typography | ★★★★ | ★★★ | ★★★ |
| Mobile speed out of the box (20%) | ★★★★ | ★★★★ | ★★★ | ★★★★★ |
| Dense catalog & filtering (15%) | ★★★★ native Search & Discovery filters, mega menu | ★★★★★ promo tiles, mega menu, strong collection grids | ★★★★★ catalog-first | ★★★ |
| Cart drawer + upsell slots (15%) | ★★★★ drawer with recommendations | ★★★★ | ★★★★ | ★★★ |
| PDP flexibility (variant swatches, blocks, sticky ATC) (15%) | ★★★★ | ★★★★ | ★★★★ | ★★★ (needs dev) |
| Gifting/occasion merchandising (10%) | ★★★★ | ★★★★★ promotional, event-driven | ★★★ | ★★ |
| **Weighted fit** | **4.3** | 4.2 | 3.8 | 3.3 |

**Why Prestige:**
- **Look:** Only's competitive slot sits between *Mirzam/Bateel luxury* and *Fantastic Chocolate's catalog-and-promo* style. Prestige gives the luxury editorial look (Mirzam, Milk Bar-style hero storytelling) while handling a 30–80 SKU catalog with occasion collections.
- **Performance:** Maestrooo themes are well maintained and perform consistently.

**Non-negotiable acceptance tests before purchase** (run on the theme demo + a trial store):
1. **Arabic RTL:**
   - Switch the store language to Arabic.
   - Verify mirrored layout: drawer opens from the left, carousels reverse, icons flip.
   - Verify Arabic font rendering and that numbers stay LTR in prices ("7.750 د.ك").
2. **KWD 3-decimal pricing** renders correctly in product cards, cart and drawer.
3. **Lighthouse mobile ≥ 70** on the demo PDP with your own hero images.
4. **Cart drawer** exposes an app block/slot for a progress bar and upsells.
5. **Variant picker** supports custom labels (for "Large · serves 10–12").

> If Arabic RTL fails any test → choose the theme that passes. RTL quality outranks every other criterion for this market.

**Customisation layer** (sections/blocks to build on top of the theme; ~8–12 dev days):
- `delivery-mode-selector`
- `drop-showcase`
- `servings-variant-picker`
- `storage-badges`
- `attach-rail`
- `whatsapp-cta`
- `lead-time-resolver` (cart drawer)
- `gift-flow` steps

### 1.2 Tech stack overview

```
┌───────────────────────────── STOREFRONT (Prestige OS 2.0, AR-RTL / EN-LTR) ─────────────────────────────┐
│ Custom sections: delivery-mode · drop-showcase · servings picker · attach rail · lead-time resolver     │
│ Native: Search & Discovery (filters, complementary products) · Translate & Adapt · Markets (KWD)       │
│ Apps (storefront): Zapiet (date/slot) · UpCart→Rebuy (drawer/upsell) · Judge.me (reviews) · Loyalty     │
├───────────────────────────── CHECKOUT (Shopify, phone-first contact) ────────────────────────────────────┤
│ Gateways: Tap Payments (KNET, Apple Pay, cards) — backup MyFatoorah · BNPL: Tabby / Deema · COD (rules)│
│ Discounts: Shopify Functions (automatic GWP, tiered, bundles)                                          │
├───────────────────────────── MESSAGING & CRM ───────────────────────────────────────────────────────────┤
│ Klaviyo (email + WhatsApp + SMS fallback, reviews sync) · WhatsApp Business API (Meta-verified)        │
├───────────────────────────── DATA & ADS ────────────────────────────────────────────────────────────────┤
│ GA4 (Google & YouTube app) · Meta CAPI (Facebook & Instagram app) · Snapchat Ads app · TikTok app      │
│ Microsoft Clarity (session recording) · Shopify Analytics                                              │
├───────────────────────────── OPERATIONS ────────────────────────────────────────────────────────────────┤
│ Order printer / kitchen tickets · Zapiet dispatch calendar · driver ETA link → WhatsApp                │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### 1.3 Kuwait & GCC payments stack

| Layer | Primary | Backup / add-on | Integration route | Notes |
|---|---|---|---|---|
| **KNET** (debit, ~majority of KW online payments) | **Tap Payments** Shopify app | MyFatoorah or Hesabe or UPayments Shopify apps | Offsite payment app (Shopify Payments Apps API) | Set KNET as the **first** method in the checkout payment order. |
| **Apple Pay** | Tap (inside Tap's hosted step) | MyFatoorah | Same gateway | Shopify's native express Apple Pay button needs Shopify Payments (not in KW). So Apple Pay appears **after** "Pay with Tap", not as a top-of-checkout express button. Mention it in the PDP/cart trust row ("KNET · Apple Pay · Visa/MC"). |
| **Credit/debit cards** (Visa/MC/Amex) | Tap | MyFatoorah | Same gateway | Enable 3-D Secure. |
| **BNPL** | **Tabby** (Shopify app; confirm KWD merchant onboarding) | **Deema** (Kuwait-native BNPL), Tamara (confirm Kuwait availability for your entity), Taly | Offsite payment app | Show **only on carts ≥ 15 KWD**, using a checkout payment-customization Function where the plan/app allows; else accept on all orders. PDP widget: "Split into 4 payments of 3.875 KD". |
| **Cash on Delivery** | Shopify manual payment method | — | Native | Restrict: express/same-day only, max 30 KWD, not for gifts to third-party recipients (collection risk), first-order cap. Use a payment-customization app/Function to hide COD per rules. |
| **GCC expansion** | Tap (Mada/KSA, Benefit/Bahrain, NAPS/Qatar) | MyFatoorah | Same | Add with Markets expansion (Phase 3+). |

**Gateway selection checklist:**
- [ ] KWD settlement account + KNET merchant ID issued
- [ ] Settlement cycle (T+1 / T+2) and per-transaction fees (KNET is typically flat-fee; cards are a percentage) compared across Tap, MyFatoorah and Hesabe
- [ ] Refund API supported from Shopify admin (partial refunds for damaged items)
- [ ] Hosted page supports Arabic and mobile; test the in-app-browser redirect return (**the #1 checkout drop-off in Kuwait**)
- [ ] Webhook reliability: order is not marked paid if the customer closes the tab after KNET success. Test 20 transactions.

### 1.4 App ecosystem (lean & high-performance)

| Job | Recommended | Alternatives | Phase | Load budget / notes |
|---|---|---|---|---|
| **Delivery date, slot & cutoffs** | **Zapiet – Pickup + Delivery** | Bird: Delivery Date & Time, DingDoong, Stellar Delivery Date | 1 | Supports product-level lead times, blackout dates, per-slot capacity, same-day cutoffs, distance/zone rules, cart-page widget (works on non-Plus). Kuwait has no reliable postal codes: configure **distance-radius zones** from the kitchen, or area lists via custom address fields. |
| **Cart drawer + upsell + progress bar** | **UpCart** (lean, Phase 2) → **Rebuy** (Phase 3 if AI recs/post-purchase pay off) | Monster Upsell, theme-native drawer + custom section | 2 | One drawer app only. Never stack two drawer apps. |
| **Filters & recommendations** | **Shopify Search & Discovery** (free, native) | Boost Commerce (if catalog > 200 SKUs) | 1 | Metafield-driven filters; complementary products feed the attach rail. |
| **Reviews (photo/video)** | **Judge.me** (Awesome plan) | Loox (photo-led), Okendo (Plus-grade) | 1 | Lightweight. Supports Arabic review widgets, review requests and Klaviyo sync. |
| **Localization** | **Shopify Markets** + **Translate & Adapt** (free) | Weglot / Langify (only if machine translation workflow needed) | 1 | Arabic `/ar` subfolder, hreflang automatic. Human-translate all PDP and checkout copy. |
| **Email + WhatsApp + SMS** | **Klaviyo** (email, WhatsApp, SMS) | Zoko / WATI / Interakt (WhatsApp BSP) + Klaviyo email | 1 (transactional), 2 (flows) | Meta Business verification and template approval needed (see agency `klaviyo-whatsapp-architect` SOP). |
| **Loyalty & referral** | **Rivo** or **BON Loyalty** | Smile.io, Yotpo Loyalty | 3 | Must support phone-number identity, points-as-KWD display and Klaviyo sync. |
| **Discounts / GWP / bundles** | **Native Shopify Functions discounts** (automatic Buy X Get Y, amount-off with minimum, combinations) + Shopify **Bundles** app | Fast Bundle (if mix-and-match UI needed) | 2 | Native: zero storefront JS. |
| **Payments customization** (hide COD/BNPL by rule) | Payment-customization Function app (e.g. HidePay / Payfy) | — | 2 | Rules by cart value, delivery mode, gift flag. |
| **Analytics/pixels** | Google & YouTube, Facebook & Instagram (CAPI), Snapchat Ads, TikTok (native channel apps) + Microsoft Clarity | — | 1 | Use Shopify Customer Events (web pixels): sandboxed, no theme bloat. |
| **Order ops** | Shopify Order Printer (kitchen ticket) + Zapiet dispatch calendar | — | 1 | Ticket prints delivery date/slot, gift note and recipient. |

**App performance budget:**
- ≤ 8 apps injecting storefront JS.
- Total third-party JS ≤ 250 KB compressed.
- Re-test Lighthouse after every app install; uninstall residue code (old app snippets in `theme.liquid`).

---

## 2. Information Architecture & Navigation

### 2.1 URL & collection architecture

```
/ (AR default for KW visitors)  ·  /en (English)
/collections/cakes                 /collections/occasion-birthday
/collections/ice-cream             /collections/occasion-ramadan-eid
/collections/bites                 /collections/occasion-corporate
/collections/chocolates            /collections/occasion-gatherings   (ghabga / diwaniya / guests)
/collections/cookies-confections   /collections/same-day-delivery     (smart: fulfillment_mode ∈ express,same_day)
/collections/gift-boxes            /collections/drops                 (current monthly drop + archive)
/collections/best-sellers          /collections/under-10-kd           (smart: price < 10.000)
/pages/corporate-gifting · /pages/catering · /pages/delivery-areas · /pages/only-club · /blogs/journal
```

Smart collections run on **tags/metafields**, so merchandising never needs manual curation:
- Product tags `mode:express`, `mode:same_day`, `mode:preorder`
- `occasion:birthday`, …
- `diet:eggless`, …

### 2.2 Header & menu structure (mobile-first)

**Announcement bar** (rotating, max 2 messages) → **Header:** ☰ · Logo · 🔍 · 👤 · 🛍 (cart count) → **Delivery-mode pill** under the header: `🚚 Deliver today · until 9 PM` ⇄ `📅 Schedule for later`

**Mobile menu (drawer, opens from the right in AR / left in EN):**

| Level 1 | Level 2 | Notes |
|---|---|---|
| ⚡ **Same-Day Delivery** | All same-day · Express 90 min | Top item. Highest-intent journey (Bleems model). |
| **Shop by Category** | Cakes · Ice Cream & Bites · Chocolates · Cookies & Confections · Gift Boxes | Each with a thumbnail tile |
| **Shop by Occasion** | Birthday · Gatherings (Ghabga/Diwaniya) · Ramadan & Eid · National Day · Thank You · Corporate | Seasonal items auto-hide off-season via metaobject `active` flag |
| 🥭 **This Month's Drop** | Current drop · Coming next · Drop archive | Badge "NEW" |
| **Best Sellers** | — | |
| **Corporate & Catering** | Corporate gifting · Events & catering · Bulk order form | WhatsApp CTA |
| **Only Club** | Points & rewards · Refer a friend | Phase 3 |
| Footer links in drawer | Delivery areas & times · Track order (WhatsApp) · العربية / English toggle | |

**Desktop mega menu:** 4 columns: Category · Occasion · Delivery (Today / Schedule) · Featured tile (current drop image + CTA).

**Search:**
- Predictive search (native) with product, collection and page results.
- Synonyms configured in Search & Discovery: bilingual and dialect.

| Query | Maps to |
|---|---|
| منقا / مانجا / مانجو / mango | mango |
| كيكة / كيك / cake | cakes |
| بايتس / قضمات / bites | bites |
| حلى / حلويات / dessert | all |
| هدية / هدايا / gift | gift boxes |
| تيراميسو / tiramisu | tiramisu |

### 2.3 Faceted search & filter tree (Search & Discovery)

| Filter | Source | Values (EN / AR) | Type |
|---|---|---|---|
| **Delivery availability** | `custom.fulfillment_mode` (list) | Express 90 min / توصيل خلال ٩٠ دقيقة · Same day / نفس اليوم · Pre-order / طلب مسبق | Multi-select, **pinned first** |
| **Price** | Native price | Under 10 KD · 10–20 KD · 20+ KD | Price-range buckets (custom labelled via collection links if needed) |
| **Category** | Product type | Cakes · Ice Cream & Bites · Chocolates · Cookies · Gift Boxes | Multi-select |
| **Occasion** | `custom.occasions` (list of metaobject refs) | Birthday · Gatherings · Ramadan · Corporate · Thank you | Multi-select |
| **Serves** | `custom.servings_band` | 1–3 · 4–6 · 7–10 · 10+ | Multi-select |
| **Dietary** | `custom.dietary` (list) | Eggless · Gluten-free · Vegan · Nut-free · Sugar-reduced | Multi-select |
| **Flavor** | `custom.flavor_family` (list) | Mango · Chocolate · Coffee/Tiramisu · Nutella · Fruit · Saffron/Rose | Multi-select |
| **Storage** | `custom.storage_temperature` | Ambient · Chilled · Frozen | Multi-select (helps the gift buyer) |
| **Availability** | Native | In stock | Toggle |

Rules:
- Hide a filter value if fewer than 2 products use it.
- Sort default = "Best selling".
- Collection pages show **servings + price-per-person** on cards.

---

## 3. High-Converting Page Layout Specifications

### 3.1 Homepage wireframe logic (mobile)

| # | Section | Content & logic | Component |
|---|---|---|---|
| 1 | **Dynamic announcement bar** | Time-aware copy from the `settings.delivery_rules` metaobject. Examples below the table. | `announcement-countdown` (custom, timezone `Asia/Kuwait`) |
| 2 | **Header + delivery-mode pill** | Selecting a mode persists in `localStorage` + cart attribute `_delivery_mode` and pre-filters collections. | `delivery-mode-selector` |
| 3 | **Hero** (9:16-friendly video or image, ≤ 150 KB poster) | Headline + 2 CTAs: **"Deliver Today" / "توصيل اليوم"** → `/collections/same-day-delivery`, **"Schedule a Gift" / "جدول هدية"** → gift flow. | Theme slideshow/video + custom CTA block |
| 4 | **Shop by need** tiles (2×2) | Same-day · Birthday · Gatherings · Gift Boxes | Collection list |
| 5 | **Best-seller rail** | 6–8 products; cards show servings, price, "⚡ Today" badge if express-eligible, quick-add | Featured collection + card badges |
| 6 | **This Month's Drop showcase** | Driven by `drop` metaobject: name, hero, countdown to end date, "Get early access on WhatsApp" if `status = upcoming` | `drop-showcase` |
| 7 | **Gathering Boxes** (bundles) | 3 boxes: Diwaniya / Ghabga / Guests with "Serves X · from Y KD" | Native Bundles + collection |
| 8 | **Why Only** trust strip | Delivered cold · Fresh daily · KNET & Apple Pay · 4.8★ reviews | Icon row (`storage-badges` reused) |
| 9 | **Reviews / UGC** | Judge.me carousel with photo reviews | App block |
| 10 | **Corporate & catering** banner | "Ordering for 20+?" + WhatsApp CTA | `whatsapp-cta` |
| 11 | **Footer** | Delivery areas & hours, payment icons (KNET, Apple Pay, Visa, MC, Tabby), language toggle, WhatsApp, Instagram/Snap/TikTok | Theme footer |

**Announcement bar copy (section 1):**
- Before cutoff: `🚚 Order in 2h 14m for delivery today` / `اطلب خلال ٢:١٤ ساعة ويوصلك اليوم`
- After cutoff: `📅 Today's slots are full. Schedule for tomorrow from 12 PM`
- Second message: free-delivery threshold.

### 3.2 PDP anatomy (top → bottom, mobile)

| # | Block | Spec |
|---|---|---|
| 1 | **Media gallery** | First slide = **9:16 video** (autoplay muted, loop, poster image). Then 4–6 images (cross-section, serving shot, packaging, scale with hand). Pinch-zoom. |
| 2 | Title + rating | Judge.me stars (link to reviews) + "🔥 Sold 120 this week" (optional, only if true; from order data) |
| 3 | **Price** | `7.750 د.ك` + **price per person** (`≈ 0.86 KD / person`) computed from `variant.metafields.custom.servings_max` |
| 4 | **Servings-per-size variant switcher** | Pill buttons, each showing size, servings and price. Examples below the table. Data: variant metafields (schema §3.5). |
| 5 | **Delivery availability line** | Logic below the table. Rendered from `custom.fulfillment_mode` + `custom.lead_time_hours` + live cutoff. |
| 6 | **Add to cart** (sticky on scroll) + **qty** | Sticky bar shows variant + price + ATC |
| 7 | **Payment row** | `KNET · Apple Pay · Visa/MC` icons + Tabby widget (if cart ≥ 15 KD) |
| 8 | **Attach rail** ("Make it a gift") | Greeting card (custom message) · Candles · Gift bag · "Happy Birthday" topper · Add 6 cookies. Source: Search & Discovery complementary products. 1-tap add; card opens a message sheet (line-item properties). |
| 9 | **Storage & handling badges** | Badges below the table. From `custom.storage_temperature`, `custom.shelf_life_hours`, `custom.serving_instructions`. |
| 10 | Tabs/accordions | Description · Ingredients & allergens (`custom.allergens`) · Delivery & areas · Storage |
| 11 | **WhatsApp CTA** | "Custom size or catering? Chat with us" → `https://wa.me/965XXXXXXXX?text=<prefilled: product title + URL>` (localized) |
| 12 | Reviews | Judge.me photo/video reviews |
| 13 | "Complete the gathering" | Complementary rail (bites + cookies) |

**Variant pill examples (block 4):**
- `Small · serves 4–6 · 5.950 KD`
- `Large · serves 10–12 · 9.750 KD`
- `Party · serves 20+ · 17.500 KD`

**Delivery availability logic (block 5):**
- `⚡ Express: arrives in 90 min if ordered before 9 PM`
- `🚚 Same-day: order before 4 PM`
- `📅 Pre-order: earliest delivery Thu 10 Oct` (lead time applied)

**Storage badges (block 9):**
- `❄️ Delivered frozen. Keep in freezer`
- `🧊 Keep chilled 2–6°C`
- `⏱ Best within 48h`
- `✅ Arrives perfect or we replace it` (**Only Promise**, Salt & Straw "Melt-Free" model)

### 3.3 Slide-out cart drawer UX

```
┌───────────── Your order (3) ─────────── ✕ ┐
│ ▓▓▓▓▓▓▓▓▓▓░░░░  Add 2.250 KD for FREE      │  ← tier 1: free delivery @ 15 KD
│                 delivery 🚚                 │  ← tier 2: free chocolate box @ 25 KD
│ ─────────────────────────────────────────  │
│ ⚠ Mixed delivery windows                  │  ← lead-time resolver (only when conflict)
│ Mango Ice-Cream Cake is pre-order (24h).   │
│ [Deliver all on Thu 10 Oct] [Split: +1.5KD]│
│ ─────────────────────────────────────────  │
│ [img] Mango Cake · Large · serves 10–12    │
│       9.750 KD          [-] 1 [+]   🗑      │
│       🎁 Card: "Happy birthday Noura…" ✎    │
│ ─────────────────────────────────────────  │
│ Make it a gift:  [🕯 0.500] [💌 1.000] [🛍 0.750] │ ← attach rail (1-tap)
│ ─────────────────────────────────────────  │
│ 📅 Delivery: Today · 6–8 PM  (change)      │  ← Zapiet cart widget (date+slot)
│ 🎁 Sending to someone else?  [toggle]      │  ← opens gift flow §4.1
│ ─────────────────────────────────────────  │
│ Subtotal 12.750 KD · Delivery calc. next   │
│ [  Checkout  ·  KNET · Apple Pay  ]        │
└────────────────────────────────────────────┘
```

**Progress bar rules:**

| Tier | Threshold | Reward | Mechanism |
|---|---|---|---|
| 1 | **15.000 KD** | Free delivery | Shipping rate condition (free rate ≥ 15 KD) or a free-shipping discount Function |
| 2 | **25.000 KD** | Free chocolate box (or 6 cookies) | Automatic **Buy X Get Y** discount (min purchase amount → gift product at 100% off); gift auto-added by the drawer app |

Copy (AR/EN):
- `باقي 2.250 د.ك وتحصل توصيل مجاني`
- `Add 2.250 KD for free delivery`
- After tier 2: `🎉 Free chocolate box unlocked`

Thresholds are set by the margin model (see Phase 2). Start at ~1.35× current AOV.

**Lead-time conflict resolver (logic):**

```text
modes   = set(line.product.metafields.custom.fulfillment_mode for line in cart)   # express | same_day | preorder
temps   = set(line.product.metafields.custom.storage_temperature for line in cart) # ambient | chilled | frozen
maxLead = max(line.product.metafields.custom.lead_time_hours)

IF "preorder" in modes AND ("express" in modes OR "same_day" in modes):
    show warning: "{preorder item} needs {maxLead}h. Choose:"
      [A] Deliver everything together on {earliest date ≥ now + maxLead}   → sets cart attr _delivery_plan=consolidated
      [B] Split into two deliveries (+{split_fee} KD)                      → _delivery_plan=split (Phase 3; ops approval)
    lock Zapiet calendar min-date = now + maxLead when [A]

IF "frozen" in temps AND "ambient" in temps:
    info note: "Frozen items travel in an insulated box, all arrive together."

IF chosen slot is express AND any line not express-eligible:
    auto-downgrade to the next valid slot + toast explaining why
```

Server-side safety net (prevents bad orders if the JS is bypassed):
- A **Cart & Checkout Validation Function**, via a public app or custom app on Plus, rejects checkout when `_delivery_date < now + maxLead`.
- On non-Plus, Zapiet's own min-date enforcement plus an order-tag webhook alert to ops is the fallback.

### 3.4 Collection page

- 2-column mobile grid.
- Cards: image (hover/second image = cross-section), title, servings, price, ⚡ badge, quick-add.
- Sticky filter/sort bar.
- Pinned "Delivery availability" filter.
- Banner slot mid-grid for the drop or a bundle.

### 3.5 Data schema: metafields & metaobjects

**Product metafields** (namespace `custom`):

| Key | Type | Example | Used by |
|---|---|---|---|
| `fulfillment_mode` | `list.single_line_text_field` (choices: `express`, `same_day`, `preorder`) | `["same_day","preorder"]` | Filters, badges, resolver, smart collections |
| `lead_time_hours` | `number_integer` (min 0, max 168) | `24` | Resolver, Zapiet sync, PDP line |
| `storage_temperature` | `single_line_text_field` (choices: `ambient`, `chilled`, `frozen`) | `frozen` | Badges, resolver, filters |
| `storage_temp_range` | `single_line_text_field` | `-18°C` / `2–6°C` | Badges |
| `shelf_life_hours` | `number_integer` | `48` | Badges ("Best within 48h") |
| `serving_instructions` | `multi_line_text_field` (translatable) | `Take out 15 min before serving` | Storage tab |
| `allergens` | `list.single_line_text_field` (choices: `milk`,`egg`,`gluten`,`nuts`,`soy`,`sesame`) | `["milk","gluten"]` | Allergen tab, compliance |
| `dietary` | `list.single_line_text_field` (choices: `eggless`,`gluten_free`,`vegan`,`nut_free`,`reduced_sugar`) | `["eggless"]` | Filters |
| `flavor_family` | `list.single_line_text_field` | `["mango"]` | Filters, recs |
| `occasions` | `list.metaobject_reference` → `occasion` | `[gid://…/Metaobject/1]` | Occasion collections, filters |
| `servings_band` | `single_line_text_field` (choices: `1-3`,`4-6`,`7-10`,`10+`) | `7-10` | Filters (product-level summary) |
| `express_eligible` | `boolean` | `true` | ⚡ badge, express slot gating |
| `gift_wrappable` | `boolean` | `true` | Attach rail visibility |
| `video_9x16` | `file_reference` (video) | — | PDP first slide |
| `drop` | `metaobject_reference` → `drop` | — | Drop badge/countdown |

**Variant metafields** (namespace `custom`):

| Key | Type | Example |
|---|---|---|
| `servings_min` | `number_integer` | `10` |
| `servings_max` | `number_integer` | `12` |
| `size_label` | `single_line_text_field` (translatable) | `Large` / `كبير` |
| `weight_grams` | `number_integer` | `1800` |
| `diameter_cm` | `number_integer` | `24` |

**Metafield definition example** (Admin GraphQL, `metafieldDefinitionCreate`):

```graphql
mutation {
  metafieldDefinitionCreate(definition: {
    name: "Storage temperature"
    namespace: "custom"
    key: "storage_temperature"
    ownerType: PRODUCT
    type: "single_line_text_field"
    validations: [{ name: "choices", value: "[\"ambient\",\"chilled\",\"frozen\"]" }]
    access: { storefront: PUBLIC_READ }
    capabilities: { adminFilterable: { enabled: true } }
  }) { createdDefinition { id } userErrors { field message } }
}
```

```graphql
mutation {
  metafieldDefinitionCreate(definition: {
    name: "Servings (max)"
    namespace: "custom"
    key: "servings_max"
    ownerType: PRODUCTVARIANT
    type: "number_integer"
    validations: [{ name: "min", value: "1" }, { name: "max", value: "200" }]
    access: { storefront: PUBLIC_READ }
  }) { createdDefinition { id } userErrors { field message } }
}
```

**Liquid: servings-aware variant pill + price per person:**

```liquid
{%- for variant in product.variants -%}
  {%- assign smin = variant.metafields.custom.servings_min.value -%}
  {%- assign smax = variant.metafields.custom.servings_max.value -%}
  <label class="servings-pill" for="v-{{ variant.id }}">
    <input type="radio" id="v-{{ variant.id }}" name="id" value="{{ variant.id }}"
           {% if variant == product.selected_or_first_available_variant %}checked{% endif %}
           {% unless variant.available %}disabled{% endunless %}>
    <span class="servings-pill__size">{{ variant.metafields.custom.size_label.value | default: variant.title }}</span>
    <span class="servings-pill__serves">{{ 'products.serves' | t: min: smin, max: smax }}</span>
    <span class="servings-pill__price">{{ variant.price | money }}</span>
    {%- if smax > 0 -%}
      {%- assign pp = variant.price | divided_by: smax | money -%}
      <span class="servings-pill__pp">{{ 'products.per_person' | t: price: pp }}</span>
    {%- endif -%}
  </label>
{%- endfor -%}
```

Locale keys:
- `en.default.json`: `"serves": "serves {{ min }}–{{ max }}"`
- `ar.json`: `"serves": "يكفي {{ min }}–{{ max }} أشخاص"`

**Metaobject definitions:**

| Metaobject | Fields |
|---|---|
| `drop` | `name` (text, translatable) · `slug` · `status` (`upcoming`/`live`/`ended`) · `starts_at` (date_time) · `ends_at` (date_time) · `hero_image` (file) · `hero_video` (file) · `products` (list.product_reference) · `early_access_segment` (text: Klaviyo segment id) · `teaser_copy` (rich text) |
| `occasion` | `name` · `slug` · `icon` · `active_from` · `active_to` · `hero_image` · `collection` (collection_reference) |
| `delivery_rules` (single entry) | `express_cutoff` (`21:00`) · `same_day_cutoff` (`16:00`) · `opening` (`10:00`) · `closing` (`23:00`) · `friday_opening` · `ramadan_mode` (boolean) · `ramadan_hours` (json) · `free_delivery_threshold` (`15.000`) · `gwp_threshold` (`25.000`) · `blackout_dates` (list.date) |
| `delivery_zone` | `name` (Salmiya, Hawalli, …) · `governorate` · `fee` (money) · `express_available` (boolean) · `min_order` (money) |

**Cart attributes & line-item properties** (captured in the drawer/gift flow; underscore = hidden from customer-facing cart where the theme supports it):

```json
{
  "attributes": {
    "_delivery_mode": "same_day",
    "_delivery_date": "2026-10-10",
    "_delivery_slot": "18:00-20:00",
    "_delivery_plan": "consolidated",
    "_is_gift": "true",
    "_recipient_name": "Noura",
    "_recipient_phone": "+96550000000",
    "_sender_name_on_card": "Ahmad & family",
    "_hide_prices_on_slip": "true",
    "_surprise_no_call": "false"
  },
  "line_item_properties_example": {
    "Card message": "كل عام وانتي بخير 💛",
    "Candles": "Number 3 + 0",
    "_card_design": "birthday-gold"
  }
}
```

---

## 4. Gifting & Fulfillment Workflow Engine

### 4.1 Recipient journey (e-gifting flow)

Triggered by **"Schedule a Gift"** (hero), **"Sending to someone else?"** (drawer toggle), or any occasion collection.

| Step | Screen | Fields / UI | Validation & logic |
|---|---|---|---|
| 1 | **Who is it for?** | Toggle `For me` / `For someone else` | `For someone else` sets `_is_gift=true`; COD hidden for gift orders. |
| 2 | **Choose the treat** | Occasion-filtered products, servings pills | Express badge only if a valid slot exists for the chosen date |
| 3 | **When?** | Calendar (Zapiet) with **only valid dates/slots** given cart lead times; slots show capacity ("2 left") | Min date = now + max lead time; blackout/Ramadan rules from `delivery_rules` |
| 4 | **Make it personal** | Card design (3–5 options, 0.500–1.000 KD), **message** (max 200 chars, AR/EN keyboard, emoji allowed), **sign as** name, candles/topper/balloons | Character counter; profanity filter optional; preview card render |
| 5 | **Recipient details** | Recipient name · **recipient phone (+965, 8 digits)** · area (dropdown) · block · street · avenue (optional) · house/building · floor/apartment · **Google Maps pin** (optional) · delivery notes | Kuwait phone regex `^\+965[2569]\d{7}$`; area must be a valid `delivery_zone` |
| 6 | **Surprise settings** | ☐ Don't call the recipient before delivery (driver contacts sender) · ☐ Hide prices on the packing slip · ☐ Send recipient a WhatsApp "a gift is on its way" message at dispatch | Stored as cart attributes |
| 7 | **Checkout** | Sender phone (contact), KNET/Apple Pay/cards/Tabby | Shopify shipping address = recipient. Sender = customer. |
| 8 | **Post-purchase** | Thank-you page: "Share the delivery link with family" · loyalty sign-up · referral | Order status page extension (all plans) |

**Kuwait address form mapping** (Shopify address fields):

| Shopify field | Kuwait use |
|---|---|
| `city` | **Area** (dropdown from `delivery_zone`) |
| `address1` | Block + Street (`Block 4, Street 12`) |
| `address2` | Avenue / House / Building / Floor / Apt |
| `province` | Governorate (Capital, Hawalli, Farwaniya, Ahmadi, Jahra, Mubarak Al-Kabeer) |
| `zip` | Not required |
| `phone` | **Required**, recipient's phone |

Enable "Phone number required" for shipping addresses in checkout settings.

### 4.2 Cutoff & slot mechanics

Three fulfilment lanes, each with its own promise. **Never show a promise the lane can't keep.**

| Lane | Eligible SKUs | Order window | Promise shown | Slot model | Capacity control |
|---|---|---|---|---|---|
| ⚡ **Express 90 min** | `express_eligible = true` AND in stock at kitchen (ready-made, chilled/ambient, plus frozen items pre-stocked) | 10:00 → **21:00** (`express_cutoff`) | "Arrives within 90 min" | Rolling ASAP slot | Max N express orders per 30 min (driver count). Auto-disable when queue is full → falls back to the next same-day slot. |
| 🚚 **Same-day scheduled** | `fulfillment_mode ∋ same_day` | Order before **16:00** (`same_day_cutoff`) | "Today, choose a 2-hour slot" | 2-hour slots: 12–14, 14–16, 16–18, 18–20, 20–22 | Capacity per slot (e.g. 15 orders); slot closes 2h before start |
| 📅 **Pre-order / advance bake** | `fulfillment_mode ∋ preorder` (ice-cream cakes, custom/party sizes, corporate) | Any time | "Earliest delivery: {date}" | Date + 2-hour slot | Daily production cap per SKU (inventory per date via Zapiet limits or a daily inventory reset) |

**Rule set** (Zapiet configuration + theme logic):
1. `earliest_date = ceil(now + max(lead_time_hours of cart lines))`, rounded to the next open slot.
2. The cart lane is the **slowest** item's lane, unless the customer splits (Phase 3).
3. After `same_day_cutoff`, "Today" disappears from the calendar. The announcement bar switches to "Schedule for tomorrow".
4. **Friday & Ramadan profiles:**
   - Friday opens later.
   - Ramadan: kitchen hours shift. **Peak slot 19:00–21:00 (post-iftar)** gets extra capacity, and the **pre-iftar 17:00–18:30** "Iftar dessert" slot is a premium.
   - Switch via `delivery_rules.ramadan_mode`.
5. **Blackout dates** (Eid day 1, kitchen maintenance) are set from `delivery_rules.blackout_dates`.
6. **Peak days** (Valentine's, Mother's Day 21 Mar, National Day 25–26 Feb):
   - Pre-orders only, 48h ahead.
   - Express disabled.
   - Slot capacity raised to match extra drivers.
7. **Zone gating:** Express available only for zones with `express_available = true` (e.g. within ~15 km of the kitchen). Remote areas (e.g. Jahra, Ahmadi south) get same-day/pre-order only, with zone fee and minimum order.
8. **Trust contract:**
   - Every promise shown (bar, PDP, drawer, checkout, confirmation WhatsApp) is generated from the **same** rules object.
   - Late-delivery SLA breach → automatic apology + 1 KD credit via loyalty points (Phase 3).

**Ops flow:**

```
Order paid ──► Tag: lane:express|same_day|preorder, date:YYYY-MM-DD, slot:HH-HH, gift:yes
          ──► Kitchen ticket (Order Printer) with card message + candles + "hide prices"
          ──► Zapiet dispatch calendar (per slot) ──► driver assigned
          ──► Fulfillment marked with tracking URL ──► WhatsApp "Out for delivery + live ETA"
          ──► Delivered ──► WhatsApp "Rate your dessert ⭐" (Judge.me link) + loyalty points posted
```

---

## 5. Conversion & Retention Setup (GCC Focus)

### 5.1 WhatsApp & SMS-first configuration

**Checkout & identity:**

| Setting | Value |
|---|---|
| Checkout → Customer contact method | **Phone number or email** (phone shown first in AR/EN copy) |
| Shipping address phone | **Required** |
| Marketing consent at checkout | ☑ "Send me offers on WhatsApp/SMS" (Shopify SMS marketing consent field → synced to Klaviyo) + ☑ email |
| Customer accounts | New customer accounts (one-time code). Phone-based OTP login via the loyalty app widget if needed. Accounts optional, never forced. |
| Phone format | E.164 `+965XXXXXXXX`; normalise numbers starting with `00965`/`965`/8 digits before syncing to Klaviyo |

**WhatsApp Business API setup checklist** (Klaviyo WhatsApp or BSP):
- [ ] Meta Business Manager verified (trade licence, matching legal name)
- [ ] Dedicated WhatsApp number (not used on the WhatsApp app); display name "Only | اونلي" approved
- [ ] Templates approved in **Arabic + English** (utility vs marketing categories set correctly):
  - `order_confirmed`
  - `out_for_delivery` (with ETA link)
  - `delivered_review_request`
  - `gift_on_its_way` (to recipient, utility)
  - `abandoned_checkout`
  - `drop_early_access`
  - `points_reminder`
- [ ] Opt-in sources: checkout checkbox, popup, loyalty sign-up, click-to-WhatsApp ads
- [ ] Quiet hours: no marketing 23:00–10:00 Kuwait time; no marketing during prayer-time peaks on Friday noon (optional brand rule)
- [ ] SMS fallback (Klaviyo SMS) for utility messages if WhatsApp undelivered

**Flows (Klaviyo):**

| Flow | Trigger | Channel sequence | Content |
|---|---|---|---|
| Order confirmation | Placed Order | WhatsApp (utility) | Items, date/slot, gift note echo, "Track" link |
| Dispatch & tracking | Fulfilled / Out for delivery | WhatsApp | Driver ETA link; recipient copy if `_is_gift` and allowed |
| Review request | Delivered + 3h | WhatsApp → email (24h) | Judge.me photo review → +points |
| **Abandoned checkout** | Started Checkout, no order | WA 30 min → email 4h → WA 20h (free-delivery nudge) | Cart contents, slot still available ("Today's 6–8 PM slot has 2 left") |
| Browse abandonment | Viewed Product ×2 | Email 2h | Product + reviews |
| Welcome | Popup / consent | WA instant (code) → email series 3 msgs | Free delivery on first order, best-sellers, drop calendar |
| Post-purchase cross-sell | Delivered + 3 days | WA/email | "Loved the Mango Cake? Try the Bites" |
| Occasion reminder | Saved occasion date − 5 days | WA | Pre-built gift box + 1-tap schedule |
| Winback | 45 / 75 days since last order | WA → email | New drop + points balance |
| VIP drop early access | Drop `status=upcoming` → `live` | WA to VIP segment 24h early | Exclusive link |

**Capture popup spec:**
- Mobile bottom sheet, 8s delay or 40% scroll, exit-intent on desktop.
- Suppressed for purchasers and on checkout/cart.
- Offer: **free delivery on first order** (protects margin vs % off).
- Field: phone (+965 prefilled) → optional email on step 2. AR/EN.
- Target capture rate: 6–10%.

### 5.2 Loyalty program: "Only Club" (points as currency)

**Core economics:**
- **Earn:** 10 points per 1 KD spent.
- **Burn:** **100 points = 1 KD** off, so points display as KWD: "You have 3.400 KD in rewards".
- Effective base reward = 10% → **adjust to margin.** Recommended base: **5 points per 1 KD = 5%**, boosted by tiers below.

| Tier | Qualify (rolling 12 months) | Earn rate | Perks |
|---|---|---|---|
| 🥭 **Member** | Join (phone number) | 5 pts / KD (5%) | Birthday treat (free bites box ≥ 10 KD order), drop alerts |
| 🌟 **Gold** | 60 KD spend or 5 orders | 7 pts / KD (7%) | 24h **early access to drops**, free delivery 1×/month |
| 💎 **Diwaniya VIP** | 150 KD spend or 12 orders | 10 pts / KD (10%) | Priority express slots (reserved capacity), free delivery always, off-menu VIP flavour each quarter, WhatsApp concierge line |

**Bonus actions:**

| Action | Points |
|---|---|
| Create account | 200 (= 2 KD) |
| Add birthday + 1 occasion date | 100 each |
| Photo review | 100 · Video review 200 |
| Referral (friend's first order ≥ 10 KD) | Friend gets 2 KD off; referrer gets 300 pts (= 3 KD) |
| Follow Instagram / Snapchat | 50 each (one-time) |
| Late-delivery apology (SLA breach) | 100 (auto) |

**Redemption rules:**
- Min redemption 100 pts (1 KD).
- Max 30% of order value.
- Points can't be combined with the first-order free delivery offer.
- Points expire 12 months after last activity.
- **Product rewards** (Milk Bar model) as an alternative: 500 pts → free Nutella cookies (6).

**Display surfaces:**
- Header account icon shows points as KD.
- PDP: "Earn 39 points (0.390 KD) with this order".
- Drawer: "You have 3.400 KD in rewards. Apply".
- Thank-you page.
- WhatsApp monthly balance message.

---

## 6. Phased Implementation Roadmap

### Phase 1: MVP launch (weeks 1–6)

**Goal:** a fast, bilingual, KNET-ready store with honest delivery promises.

| Workstream | Tasks | Done when |
|---|---|---|
| Foundation | Shopify Grow plan · domain `onlykw.com` + 301s from old URLs (`/product/<cat>/<slug>` → `/products/<handle>`) and `onlymangokw.com` · store timezone Asia/Kuwait · KWD money format set to `{{amount}} د.ك` / `{{amount}} KD`, then verify fils precision (3 decimals, e.g. 7.750) renders in theme, checkout and notifications. If any surface rounds to 2 decimals, price SKUs on 0.250 KD steps and raise a Shopify support ticket. | 0 broken URLs in crawl; ad links redirect correctly |
| Theme | Prestige install + brand tokens · RTL acceptance tests passed · custom sections: `servings-variant-picker`, `storage-badges`, `announcement-countdown`, `delivery-mode-selector` (basic), `whatsapp-cta` | Lighthouse mobile ≥ 70 on home/PDP/collection |
| Localization | Markets: Kuwait (primary, KWD) · Arabic default + English `/en` · Translate & Adapt with human-reviewed AR copy · Arabic search synonyms | All pages, notifications and checkout strings in AR/EN |
| Catalog | Metafield & metaobject definitions (§3.5) · products with variants (servings), 9:16 videos, allergen data · smart collections (category, occasion, same-day, under-10) · Search & Discovery filters | Every SKU has `fulfillment_mode`, `lead_time_hours`, `storage_temperature`, servings |
| Payments | Tap (KNET + Apple Pay + cards) live · COD rules · 20 test transactions incl. in-app-browser KNET return · refund test | ≥ 98% paid-order capture on tests |
| Delivery | Zapiet: zones, fees, lanes (express/same-day/pre-order), cutoffs, capacities, blackout dates · Kuwait address mapping · Order Printer kitchen ticket | Ops dry-run: 30 mock orders across lanes, zero promise conflicts |
| Data | GA4, Meta CAPI, Snap, TikTok via channel apps · Clarity · UTM conventions · purchase dedup verified | Events Manager match quality "Good"; GA4 purchase = Shopify orders ±5% |
| Reviews & messaging | Judge.me installed (import existing reviews) · Klaviyo + WhatsApp transactional templates (confirm, dispatch, delivered) | Messages fire on a real test order |
| QA | Device matrix: iPhone Safari + IG webview, Android Chrome + IG/Snap webview, desktop · AR/EN · each lane · gift vs self | Signed-off checklist |

### Phase 2: Gifting UX & AOV optimization (weeks 7–12)

**Goal:** lift AOV with thresholds, bundles and add-ons, and make gifting effortless.

| Workstream | Tasks | KPI |
|---|---|---|
| Cart drawer | UpCart: progress bar (15 KD free delivery, 25 KD GWP), attach rail, slot widget placement · `lead-time-resolver` section | AOV +20–25% |
| Discounts | Automatic Buy X Get Y GWP · tiered discounts for bundles · Shopify Bundles: Diwaniya / Ghabga / Guests boxes | Bundle share of orders ≥ 25% |
| Gift flow | Full §4.1 flow: card designs, message preview, recipient phone, surprise settings, "hide prices" slip · `_is_gift` hides COD | Gift orders tagged; card attach rate ≥ 30% of gift orders |
| PDP | Attach rail (complementary products) · Tabby widget (≥ 15 KD) · reviews with photos · price-per-person | PDP ATC rate +10% |
| Payments | Tabby/Deema live (threshold) · payment customization Function (COD/BNPL rules) | BNPL share on ≥ 15 KD carts |
| Capture & flows | Popup (WhatsApp-first) · welcome, abandoned checkout, browse, post-purchase flows | Capture 6–10%; flows ≥ 10% of revenue |
| Margin model | Set thresholds and GWP cost from SKU margin + delivery cost per zone | Contribution margin per order ≥ target |

### Phase 3: Retention & scarcity mechanics (months 4–6)

**Goal:** make the second and fifth orders cheap. Turn the menu into an event.

| Workstream | Tasks | KPI |
|---|---|---|
| Monthly drops | `drop` metaobject live · `drop-showcase` with countdown · "Coming next" waitlist (WhatsApp) · drop archive · VIP 24h early access | Drop-week revenue share ≥ 20%; waitlist → buyer ≥ 25% |
| Loyalty | Rivo/BON: Only Club tiers, points-as-KD, referrals, birthdays/occasions, review rewards · surfaces in header/PDP/drawer/thank-you | Repeat rate (60-day) ≥ 25%; members ≥ 40% of orders |
| VIP WhatsApp | Diwaniya VIP segment · concierge line · reserved express capacity · off-menu quarterly flavour | VIP LTV ≥ 3× average |
| Occasion engine | Saved occasions → reminder flow with pre-built boxes | Reminder conversion ≥ 8% |
| Corporate & catering | Bulk-order landing page + form → WhatsApp/CRM · (Plus: B2B catalog & net terms) | Corporate pipeline monthly |
| Optimization | Evaluate Rebuy (AI recs + post-purchase upsell) vs UpCart · A/B tests: threshold levels, hero mode selector, PDP video-first · split-delivery option if ops ready | Statistically significant wins only |
| Expansion readiness | Markets: KSA/UAE/Qatar/Bahrain (local currency, Tap local methods), cross-border shippable SKUs (chocolates, ambient boxes) only | Go/no-go per market |

---

## Appendix A: Component Build Checklist

| Component | Type | Inputs | Phase | Acceptance criteria |
|---|---|---|---|---|
| `announcement-countdown` | Section (JS) | `delivery_rules` | 1 | Correct in Asia/Kuwait time; switches copy at cutoff; AR digits optional |
| `delivery-mode-selector` | Snippet + JS | Cart attributes | 1 → 2 | Persists mode; pre-filters same-day collection; reflected in drawer |
| `servings-variant-picker` | Snippet | Variant metafields | 1 | Shows size/servings/price/per-person; accessible radio group; RTL-correct |
| `storage-badges` | Block | Product metafields | 1 | Auto-renders correct badge set per temperature |
| `whatsapp-cta` | Block | Theme setting (number), product context | 1 | Prefilled localized message with product URL |
| `attach-rail` | Block | Complementary products | 2 | 1-tap add; card opens message sheet; updates drawer totals |
| `lead-time-resolver` | Drawer section | Cart + metafields + Zapiet | 2 | Detects all conflict types; consolidated option sets min date |
| `gift-flow` | Page/drawer steps | Cart attributes, line props | 2 | Validates KW phone; recipient → shipping address; surprise flags on ticket |
| `drop-showcase` | Section | `drop` metaobject | 3 | Upcoming/live/ended states; countdown; waitlist capture |
| `loyalty-surfaces` | App blocks | Loyalty app | 3 | Points shown as KD in 4 surfaces |

## Appendix B: Launch QA Checklist

- [ ] Arabic RTL: header, drawer direction, carousels, filters, cart, checkout, notifications, WhatsApp templates
- [ ] KWD shows 3 decimals everywhere (cards, PDP, drawer, checkout, emails)
- [ ] KNET success/failure/cancel return paths in Safari, Chrome, IG webview, Snap webview
- [ ] Every SKU: lane, lead time, storage temperature, servings, allergens populated
- [ ] Express lane disables at capacity and after cutoff; announcement bar matches
- [ ] Mixed-lane cart triggers resolver; calendar min-date enforced
- [ ] Gift order: recipient address/phone, card message on kitchen ticket, prices hidden on slip, COD hidden
- [ ] GWP auto-adds at 25 KD and removes below threshold
- [ ] Pixels: one Purchase per order (browser + CAPI dedup), correct value in KWD
- [ ] Lighthouse mobile ≥ 70; LCP < 2.5s on 4G for home/PDP
- [ ] 301 redirects from legacy URLs and old domain
- [ ] Legal pages AR/EN: terms, privacy, refund/replacement (perishables), delivery policy
