# Competitor Benchmark Analysis — onlykw.com ("Only", formerly "Only Mango")

_Prepared: 2026-10-08 · Scope: GCC/MENA + global DTC dessert & gifting benchmarks_

---

## 0. Read this first — method, evidence levels & a scope correction

**Scope correction.** The brief framed onlykw.com as an apparel/accessories/lifestyle store. It is not. **onlykw.com is "Only" (rebranded from "Only Mango", old domain `onlymangokw.com`), a Kuwaiti DTC _dessert_ brand** selling mango cake, ice-cream bites, tiramisu, Nutella cookies and combo bundles with local delivery. The competitive set and the audit criteria below were adapted to the right category (premium desserts, cakes & edible gifting). Apparel-specific items (size guides, returns) were remapped to their dessert equivalents (servings guide, freshness/cold-chain guarantee, delivery slot).

**Access limits.** This research environment's network policy blocked direct fetches of onlykw.com and every competitor domain (HTTP 403 at the egress proxy), so **no page source, robots.txt, sitemap, or live mobile walkthrough could be captured**. To compensate:

| Evidence tag | Meaning |
|---|---|
| **[D] Data** | First-party data from the brand's connected Meta Ads account (`Only Mango Ad Acc 1`) and Snapchat account (`only Self Service`) — ad creatives, landing URLs, pixel events, 90-day performance (2026-07-10 → 2026-10-07). |
| **[R] Reported** | Found in public sources via web search (brand pages' indexed snippets, Semrush/Ahrefs snapshots, trade press). |
| **[I] Inferred** | Analyst inference from URL patterns, pricing, or category norms. Verify before acting. |

**Verification to-do (15 min, any normal browser):** view-source on onlykw.com and each competitor → confirm platform (Wappalyzer/BuiltWith), payment badges at checkout (KNET / Apple Pay / Tabby / Deema / COD), popup mechanics, and cart drawer behaviour. Items marked "unverified" in the matrix are exactly these.

---

## 1. Task 1 — onlykw.com Site & Product Taxonomy

### 1.1 Product taxonomy [D] (from ad landing URLs `onlykw.com/product/<category>/<slug>`)

| Category (URL slug) | SKUs observed | Price (KWD) | Notes from ad copy |
|---|---|---|---|
| `cake` | Mango Cake, Tiramisu Cake, (Coffee Cake) | Mango Cake **7.750** | "Serves 7–9"; 3 layers: cake, mango, cream; served cold. Hero SKU. |
| `ice-cream-bites` | Mango, Cocoa, Tiramisu Ice-Cream Bites | Mango Bites **7.950** | Cocoa = "20 pcs covered with milk chocolate". Mango Bites called "the signature". |
| `cookies` | Nutella Cookies (12 pcs) | n/a | Soft cookie, molten Nutella centre. |
| `combo` | Tiramisu Cake + Tiramisu Bites + Nutella Cookies; Tiramisu Cake + Mango Cake + Nutella Cookies | n/a | Positioned as "the strongest offer for gatherings" (العرض الأقوى للجمعات). |

**Positioning [D]:** Kuwaiti-dialect, occasion-driven copy built around family gatherings and guests (يمعتكم وزوارتكم), post-iftar/after-meal cravings, summer heat relief ("a refreshing dessert for Kuwait's heat"), and challenge/confidence hooks ("we challenge anyone with our mango cake"). Value prop: **light, fresh fruit dessert versus heavy sweets, fast and reliable delivery to your door.**

**Price tier [I]:** _Accessible premium._ 7.75–7.95 KWD per hero unit sits at roughly **half** of same-day cakes on Floward/Bleems (15–41 KWD) and below Fantastic Chocolate's large ice-cream cake (14.990 KWD). Cost per serving for the mango cake is about 0.9–1.1 KWD.

**Delivery & payment [I / unverified]:** Copy promises fast and accurate home delivery in Kuwait ("توصيل فوري ومضبوط"). The checkout methods could not be observed. Kuwait norms are KNET, Visa/MC, and Apple Pay, with Tabby/Deema BNPL and COD optional. Confirm what's live.

### 1.2 Tech stack

| Layer | Finding | Evidence |
|---|---|---|
| Storefront/platform | **Not Shopify** (Shopify uses `/products/<handle>`; onlykw uses `/product/<category>/<slug>`). Most likely a Kuwaiti SaaS ordering platform (Ordable-style) or a custom build. | [I] URL structure |
| Meta Pixel | Live, firing ViewContent, AddToCart, InitiateCheckout and Purchase **with values**. | [D] |
| Meta Catalog | Live. Dynamic catalog ads use `{{product.name}}` / `{{product.current_price}}` templates. | [D] |
| Conversions API | Unknown. Click→LPV loss (below) suggests checking pixel/CAPI deduplication and page speed. | [I] |
| Snap Pixel | Implied: 11 Snapchat SALES-objective campaigns, 3 active (Sales Max & Auto Bid, Statics Testing, Only Winning). | [D] |
| Analytics | **No GA4 property for onlykw is connected** to the agency's analytics stack (other clients have one). | [D] |
| Email/SMS/WhatsApp CRM | No evidence of Klaviyo or another ESP. Instagram link-in-bio carries UTMs (`utm_source=ig&utm_medium=social&utm_content=link_in_bio`). | [D]/[I] |

### 1.3 Performance baseline — Meta, last 90 days [D]

Account currency is USD (1 KWD ≈ 3.26 USD).

| Metric | Value |
|---|---|
| Spend | **$10,753** |
| Impressions / Reach / Frequency | 958K / 232K / **4.1** |
| CTR (all) / CPM | 1.18% / $11.2 |
| Link clicks → Landing-page views | 6,522 → 2,784 (**42.7%**, a major leak) |
| View content → Add to cart | 3,353 → 813 (24%) |
| Add to cart → Initiate checkout | 813 → 684 (84%) |
| Initiate checkout → Purchase | 684 → 380 (**55.6%**) |
| Purchases / Revenue | 380 / $13,906 |
| **ROAS / CPA / AOV** | **1.30 / $28.2 / $36.6 (≈ 11.2 KWD)** |
| Device | 99.8% of spend on mobile-app placements (IG/FB in-app browser) |

**Campaign view [D]:**

| Campaign | Spend | Purchases | ROAS | Read |
|---|---|---|---|---|
| Only Winning – 27 Aug | $3,922 | 155 | 1.45 | Scaled winners. Workhorse. |
| New Sales Adv+ – 22 Jul | $3,144 | 80 | **0.97** | Frequency 4.1, LPV rate 37%. Fatigued. |
| Sales Adv+ | $2,170 | 99 | **1.60** | Best efficiency. |
| Only New Creatives – 18 Sep | $955 | 28 | 1.12 | Testing. |
| Only Statics – Adv+ – 24 Aug | $519 | 17 | 1.14 | Static test. |

**Creative view [D]:** "Luqmah cake" ads (2 variants, $5.3K spend, 231 purchases, ROAS 1.51–1.70) carry the account. **Mango Bites – Static has the best return (ROAS 2.12, AOV $46)**. Mango-cake reels underperform statics (0.84–1.10). **Nutella Cookies – Static: $171 spend, 0 purchases.**

**Diagnosis:** the category, price and creative product-market fit are real: 1.2% CTR and a 13.6% LPV→purchase rate are healthy. Profitability is lost to three things:
1. A **57% click-to-page-load drop**, from speed or in-app-browser friction.
2. **No AOV architecture.** AOV ≈ one hero item plus delivery.
3. **No owned-channel retention layer** to make the second order cheap.

At 1.3 ROAS on a food COGS profile, the brand is likely unprofitable on first order.

---

## 2. Task 2 — Competitor Set

### Tier A — GCC & regional high performers

#### A1. Fantastic Chocolate — `fantasticchocolatekw.com/en-kw` · Kuwait — _closest direct competitor_
- **Overlap [R]:**
  - Chocolamo ice-cream cake: S 9.990 KWD (serves 4–5), L 14.990 KWD (serves 8–10).
  - Chocolate ice-cream cake L 12.990.
  - Mango gelato and mango ice-cream cakes, Ice-Cream Kunafa (27 pcs), ice-cream biscuit combos.
- **Offer [R]:** **Free delivery** to most areas, **delivered within 90 minutes**, ordering 10:30–23:30. **Free chocolate box on orders over 20 KWD.** Servings shown per size.
- **Stack [I-strong]:** Shopify with Markets (`/en-kw/collections/…`, `/blogs/news/…`). Runs an SEO blog ("Best Ice Cream Cakes in Kuwait").
- **Traffic [I]:** 20–60K visits a month. Channels: IG/Snap paid social plus content SEO and brand search.

#### A2. Floward — `floward.com/en-kw` · Kuwait-founded, GCC + UK
- **Overlap [R]:** same-day cakes at 15–41 KWD, personalised photo cake 25 KWD, add-ons (balloons 1 KWD, cards). Competes for **gifting occasions** at about 2x Only's price.
- **Offer [R]:** delivery date/slot picker or same-day; free delivery over 25 KWD; average fulfilment about 90 min. Bank promos (NBK 15% off).
- **Stack [I]:** custom build plus native iOS/Android apps. Payments unverified.
- **Traffic [R]:** Semrush about 205–236K web visits a month (KSA 37%, UAE 14.5%, Egypt 12.4%). Most volume is in the app. Channels: direct/app, brand search, paid search for "send flowers/cake [city]".

#### A3. Bleems — `bleems.com/kw` · Kuwait gifting marketplace, GCC
- **Overlap [R]:** about 5,400 confection SKUs from Kuwaiti home-grown bakeries, e.g. Mango Trifle Cake 20 KWD, tiramisu 18 KWD, bento cakes from 7 KWD; ice-cream category. **This is the shelf where Only's local rivals compete.**
- **Offer [R]:** "90-minute delivery", "Same day", "Pick a date".
- **Stack [R]:** custom build on Azure; app-first (iOS 4.2★, about 12K ratings).
- **Traffic:** Ahrefs about 9.9K organic visits a month (51% Kuwait) [R]. Total about 100–250K a month, app/direct dominant [I].

#### A4. Bateel — `bateel.com/en_kw` · KSA/UAE premium, Kuwait boutique at The Avenues
- **Overlap [R]:** premium gift boxes (dates, chocolate, gourmet), occasion collections (Ramadan, National Day). Competes for **gifting share-of-wallet**, not cakes.
- **Offer [R]:** free shipping above 9 KWD; 24h processing, **2–5 day delivery (no same-day)**; estimated-delivery widget on PDP.
- **Stack [I]:** Magento 2 (`/en_kw/…html` store-code URLs).
- **Traffic [I]:** 150–400K visits a month GCC-wide. Brand search and direct dominate.

#### A5. Khobz — `khobzkw.net` · Kuwait artisan bakery
- **Overlap [R]:** Tiramisu cake 12 KWD; minimum order 3 KWD.
- **Offer [R]:** **next-day only, 3 PM cutoff.**
- **Stack [I]:** Shopify (`/products/<slug>`).
- **Traffic [I]:** under 10K visits a month, Instagram-driven.
- _Same-tier peers:_ Bakerista and November & Co (Ordable storefronts), Cakena (same-day in 2–4h), FNP Kuwait (mango cake 12 KWD / 500 g, 21 KWD / 1 kg) [R].

#### A6. Saadeddin — `saadeddin.com` · KSA chain (about 127 stores)
- **Overlap [R]:** large cakes 169.9–199.9 SAR (about 13.9–16.3 KWD), slices 19.9–24.9 SAR.
- **Channel [R]:** orders flow mainly through HungerStation, ToYou and Ninja; own site is secondary.
- **Read [I]:** a KSA expansion would need a Salla/Zid store **and** aggregator presence.

### Tier B — Global DTC benchmarks

#### B1. Milk Bar — `milkbarstore.com` · US nationwide shipping
- **Overlap [R]:** cakes, truffles, cookie tins, **combo/gift boxes** ("cake + truffles combo"). Priced at 3–6x Only, plus $15–60 shipping.
- **Stack [R/I]:** Shopify. Email/SMS consolidated from Klaviyo + Attentive + Yotpo into **Sendlane** (+27% email/SMS revenue in 3 months, vendor claim). Separate multi-address gifting tool.
- **Traffic [R]:** about 124–233K visits a month; organic 40–47%, direct 38–44%.
- **Wins:**
  - Delivery-date picker up to 30 days out, with lead-time copy.
  - Gift notes; recipient-scheduled e-gift (recipient picks date and flavour).
  - Free shipping at $100+.
  - **First Bite Club** loyalty: auto-enrol, points for purchase, birthday, review, referral and receipt upload; rewards paid in product.
  - Seasonal "shops" as drops.

#### B2. Magnolia Bakery — `magnoliabakery.com` · US stores + nationwide; GCC franchise incl. Kuwait 360 Mall
- **Overlap [R]:** **hero SKU (banana pudding) ≈ Only's mango cake.** Bundle "large pudding + 2 cupcakes" about $35 is close to Only's AOV.
- **Stack [R]:** Shopify across all points of sale; Sailthru email (historic); Amex Offers (more than 10x ROI on acquisition).
- **Traffic [R]:** about 109–229K visits a month, seasonal peaks.
- **Wins:**
  - Site split into 3 jobs (find bakery / grocery / order).
  - Same-day local versus scheduled national flows.
  - **Monthly rotating flavour of the hero SKU** (lifted category sales by more than 5%).
  - Segmentation and A/B testing lifted conversion rate by about 40%; returning-customer rate about 30%.
  - Aggregator-exclusive flavours.

#### B3. Crumbl — `crumblcookies.com` + app · US/Canada, 1,000+ stores
- **Overlap [R]:** 4-pack $16–20, 6-pack $23–27, party boxes. **Price points ≈ Only's 7–8 KWD.**
- **Stack [I]:** proprietary app plus web; pushes first-party pickup over aggregators.
- **Traffic [R]:** about 5.9–6.5M web visits a month; organic 47%, direct 40%. Instagram is 35% of social referrals. Top-6 Food & Drink app (500K downloads in one December).
- **Wins:**
  - **Weekly menu drop** (4–6 flavours revealed Sunday night, retired after a week: manufactured scarcity).
  - Points-as-cash wallet (100 Crumbs = $10).
  - "Taste Weekly" subscription.
  - Pack tiers anchor AOV.

#### B4. Salt & Straw — `saltandstraw.com` · US West Coast + nationwide shipping
- **Overlap [R]:** frozen dessert in packs, comparable to the ice-cream bites.
- **Stack [I]:** Shopify.
- **Traffic [I]:** 100–300K visits a month.
- **Wins:**
  - **5-pint minimum, then a 6th pint for $10** (forced bundle plus a discounted add-on).
  - **Melt-Free Guarantee** (free reship if not frozen).
  - **Pints Club** subscription: skip-able, prepaid 3/6/12-month at 10/15/20% off.
  - New rewards program (June 2026) with early access to drops and "buy 4 get 5th free".

### 2.1 Competitor summary table

| # | Brand | Market | Price overlap vs Only (7.75–7.95 KWD) | Platform | Est. monthly visits | Dominant channels |
|---|---|---|---|---|---|---|
| A1 | Fantastic Chocolate | KW | High: 9.99–14.99 KWD ice-cream cakes | Shopify [I] | 20–60K [I] | Paid social, SEO blog, brand |
| A2 | Floward | KW/GCC | Medium: 15–41 KWD gifting cakes | Custom + app | ~205–236K web [R] + app | App/direct, paid search, bank partnerships |
| A3 | Bleems | KW/GCC | High: 7–20 KWD local bakery cakes | Custom (Azure) + app | 100–250K [I] | App/direct, organic |
| A4 | Bateel | GCC | Low–Med: gifting boxes | Magento 2 [I] | 150–400K [I] | Brand search, direct |
| A5 | Khobz (+ Ordable peers) | KW | Med: 12 KWD tiramisu | Shopify [I] | <10K [I] | Instagram |
| A6 | Saadeddin | KSA | Med: ~14–16 KWD cakes | Unverified | n/a (aggregator-led) | HungerStation/ToYou |
| B1 | Milk Bar | US | Format overlap (combos) | Shopify | 124–233K [R] | Organic, direct |
| B2 | Magnolia Bakery | US (+KW franchise) | Hero-SKU model | Shopify | 109–229K [R] | Organic, direct, Amex |
| B3 | Crumbl | US/CA | Pack prices ≈ Only | Proprietary app | 5.9–6.5M [R] | Organic, direct, IG/TikTok |
| B4 | Salt & Straw | US | Frozen packs ≈ bites | Shopify [I] | 100–300K [I] | Brand, store locator |
| — | **onlykw.com** | KW | — | Non-Shopify SaaS/custom [I] | ~10–20K [I]* | **Paid social (Meta + Snap)** |

\*Estimate: about 2.8K Meta LPVs in 90 days plus Snap and IG organic suggests a site that is almost entirely paid-social-dependent, with little organic or direct demand captured.

---

## 3. Task 3 — UX & Conversion Architecture Audit

Legend: ✅ strong · ◐ partial · ❌ absent/weak · ❓ unverified for onlykw (fetch blocked; verify on device). Competitor cells marked ¹ are reported, not directly observed.

### 3.1 Mobile navigation & search

| Capability | onlykw | Fantastic Choc. | Floward | Bleems | Bateel | Milk Bar | Magnolia | Crumbl | Salt & Straw |
|---|---|---|---|---|---|---|---|---|---|
| Category depth / filters (occasion, servings, price) | ◐ 4 flat categories [D] | ◐ collections | ✅ occasion + price + same-day | ✅ price/vendor/delivery-type filters | ✅ occasion collections | ✅ occasion shops | ✅ 3-job IA | ✅ weekly menu | ✅ collections + flavours |
| "Same-day / deliver today" as a nav filter | ❓ | ✅¹ | ✅ | ✅ | ❌ | n/a | ✅¹ local | ✅ | n/a |
| Search autocomplete | ❓ (small catalog: low priority) | ◐¹ | ✅¹ | ✅¹ | ✅¹ | ◐¹ | ◐¹ | n/a (app) | ◐¹ |
| Arabic/English toggle | ❓ (ads are Arabic-first) | ✅ | ✅ | ✅ | ✅ | n/a | n/a | n/a | n/a |
| Sticky header / sticky ATC | ❓ | ❓ | ✅¹ | ✅¹ | ❓ | ❓ | ❓ | ✅ app | ❓ |

### 3.2 PDP anatomy (dessert-adapted)

| Capability | onlykw | Fantastic Choc. | Floward | Bleems | Bateel | Milk Bar | Magnolia | Crumbl | Salt & Straw |
|---|---|---|---|---|---|---|---|---|---|
| 9:16 video / reel on PDP | ❓ (has strong reels in ads [D]) | ❓ | ◐ | ❌ | ◐ | ◐ | ◐ | ✅ app | ◐ |
| Servings guide ("serves 7–9") | ◐ in ads only [D] | ✅ | ◐ | ◐ | n/a | ✅ | ✅ | ✅ pack sizes | ✅ |
| Size/variant ladder (S/L, 6/12/20 pcs) | ❌ single size [D] | ✅ S/L | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ 4/6/party | ✅ 5+1 |
| Delivery date & slot picker | ❓ | ◐ (cakes 1 day ahead) | ✅ | ✅ 90-min / same-day / date | ✅ ETA widget | ✅ 30-day | ✅ | ✅ | ✅ |
| Gift message / card / candles / balloons | ❓ | ◐ | ✅ | ✅ | ✅ | ✅ + e-gift | ✅ | ◐ | ◐ |
| Freshness / cold-chain guarantee | ❌ | ◐ | ◐ (edibles excluded) | ❌ | ✅ | ✅ | ◐ | n/a | ✅ Melt-Free |
| Reviews / UGC | ❓ (UGC-style ads win [D]) | ❓ | ✅ | ✅ | ◐ | ✅ | ✅ | ✅ | ✅ |
| Urgency (cutoff countdown, limited drop) | ❓ | ◐ ordering hours | ✅ same-day cutoff | ✅ | ❌ | ◐ | ✅ monthly flavour | ✅ weekly drop | ✅ monthly flavours |
| Local payments on PDP (KNET/Apple Pay/Tabby badges) | ❓ | ❓ | ◐¹ bank promos | ❓ | ❓ | n/a | n/a | n/a | n/a |

### 3.3 Cart & checkout friction

| Capability | onlykw | Fantastic Choc. | Floward | Bleems | Bateel | Milk Bar | Magnolia | Crumbl | Salt & Straw |
|---|---|---|---|---|---|---|---|---|---|
| Slide-out cart with upsell | ❓ | ❓ | ✅ add-ons | ✅ add-ons | ◐ | ✅ | ◐ | ✅ | ✅ 6th pint |
| Free-delivery / gift threshold | ❌ none seen | ✅ free delivery + gift >20 KWD | ✅ free >25 KWD | ◐ | ✅ free >9 KWD | ✅ $100 | ◐ | ◐ | ✅ min 5 |
| Bundles / combos | ✅ 2 combos [D] | ✅ | ✅ | ◐ | ✅ | ✅ | ✅ | ✅ boxes | ✅ |
| Express pay (Apple Pay / Shop Pay) | ❓ | ❓ (Shopify: likely) | ✅¹ app | ✅¹ app | ❓ | ◐ | ✅ Shop Pay¹ | ✅ app wallet | ✅ Shop Pay¹ |
| Guest checkout & phone-first login | ❓ | ❓ | ✅ | ✅ | ✅ | ✅ | ✅ | app | ✅ |
| **Measured IC→Purchase** | **55.6% [D]** | — | — | — | — | — | — | — | — |

_IC→Purchase of 55.6% is below a healthy ~65–75% for a single-market, payment-native checkout [I]. Payment step friction (KNET redirect drop-off, OTP failures, address form) is the prime suspect._

### 3.4 Retention & capture

| Capability | onlykw | Fantastic Choc. | Floward | Bleems | Bateel | Milk Bar | Magnolia | Crumbl | Salt & Straw |
|---|---|---|---|---|---|---|---|---|---|
| Email/SMS capture popup | ❓ (no ESP evidence) | ❓ | ✅ app | ✅ app | ✅ | ✅ (free ship 1st order¹) | ✅ | ✅ app | ✅ |
| **WhatsApp opt-in / order updates** | ❓ (Meta shows 31 messaging convos) | ◐ | ✅ | ✅ | ◐ | n/a (SMS) | n/a | n/a | n/a |
| Loyalty program | ❌ | ❌ | ◐ | ◐ | ✅ | ✅ First Bite Club | ◐ | ✅ Crumbs-as-cash | ✅ Spoons |
| Referral | ❌ | ❌ | ✅ | ◐ | ❌ | ✅ $15 | ❌ | ◐ | ◐ |
| Subscription / club | ❌ | ❌ | ✅ flower subs | ❌ | ❌ | ◐ | ❌ | ✅ Taste Weekly | ✅ Pints Club |
| Drops / rotating flavour | ◐ new bite flavours launched [D] | ◐ | seasonal | vendor-driven | seasonal | ✅ | ✅ monthly | ✅ weekly | ✅ monthly |
| Occasion/birthday reminders | ❌ | ❌ | ✅ | ✅ | ✅ | ✅ | ◐ | ◐ | ◐ |
| Native app | ❌ | ❌ | ✅ | ✅ | ✅ | ❌ | ❌ | ✅ | ✅ |

---

## 4. Estimated operational metrics (benchmarks vs onlykw)

| Metric | onlykw (actual / est.) | GCC dessert DTC benchmark [I] | Global best-in-class [R/I] |
|---|---|---|---|
| Meta ROAS (7d click/1d view) | **1.30** [D] | 2.0–3.0 | 3.0+ |
| Meta CPA | **$28.2 (~8.6 KWD)** [D] | 4–6 KWD | — |
| AOV | **~11.2 KWD** [D] | 14–20 KWD (with thresholds) | Milk Bar $60–70; Crumbl ~$25 |
| Click → LPV | **42.7%** [D] | 70–85% | 80%+ |
| LPV → Purchase | 13.6% [D] (strong) | 5–10% | 3–6% (cold traffic) |
| IC → Purchase | **55.6%** [D] | 65–75% | 70%+ (Shop Pay / app wallet) |
| Frequency (90d) | 4.1 [D] | <3.5 for 90d prospecting | — |
| Returning-customer rate | Unknown (no CRM data) | 25–35% | Magnolia ~30% [R] |
| Delivery promise | "Fast, accurate" (unquantified) | **90 min, free** (Fantastic Choc., Bleems, Floward) | Same-day local + scheduled national |
| Owned-channel revenue share (email/WA/SMS) | ~0% [I] | 15–25% | 25–35% |

## 5. What competitors win on (and onlykw can copy)

1. **A quantified delivery promise.** "90 minutes, free" is the regional table stakes. Only's copy says "fast" but never quantifies it.
2. **Threshold-driven AOV.** Free delivery or a free gift at 20–25 KWD (Fantastic Chocolate, Floward). Only has none, so AOV sits at about 1 item.
3. **Servings and size ladders.** S/L and 6/12/20-piece tiers convert the same visitor at different budgets.
4. **Gifting UX.** Date/slot picker, gift card message, candles and balloons add-ons. Kuwait is occasion-driven (diwaniya, ghabga, guests).
5. **Scarcity drops.** Crumbl, Magnolia and Salt & Straw turn new flavours into weekly or monthly events. Only already launches new bite flavours but doesn't frame them as drops.
6. **Retention layer.** Loyalty-as-cash, clubs and WhatsApp/SMS flows. Every global benchmark gets 25–35% of revenue from owned channels.
7. **Category SEO.** Fantastic Chocolate's "Best Ice-Cream Cakes in Kuwait" blog captures demand Only currently has to buy.
8. **Marketplace presence as a channel, not a threat.** Bleems already sells Kuwaiti mango/tiramisu cakes, so a listing there is cheap reach for gifting.

---

### Sources

- Meta Ads & Snapchat Ads accounts for Only (first-party, via ZaneConnect), pulled 2026-10-08.
- Floward: floward.com/en-kw/order-cakes-online · floward.com/en-kw/Terms · semrush.com/website/floward.com/overview
- Bleems: bleems.com/kw/confections/cakes · bleems.com/ar/kw/confectionery/joyconfections/mango-trifle-cake · apps.apple.com/app/id569788924 · ahrefs.com/websites/bleems.com
- Fantastic Chocolate: fantasticchocolatekw.com/en-kw/collections/ice-cream-cakes-treats · fantasticchocolatekw.com/en-kw/blogs/news/best-ice-cream-cakes-in-kuwait
- Bateel: bateel.com/en_kw/occasions/saudi-national-day/majd-al-akhdar-gift-set.html
- Kuwait bakeries: khobzkw.net/products/tiramisu-cake · kw.fnp.com · bakerista.ordable.com · novemberandcokw.ordable.com
- Saadeddin: toyou.io/en/riyadh/desserts-coffee/saadeddin/ · gulfood.com exhibitor listing
- Magnolia Bakery Kuwait: imagesretailme.com/magnolia-bakery-opens-at-kuwaits-360-mall/
- Milk Bar: sendlane.com/customerstories/milk-bar · tryperdiem.com · barrelny.com · semrush milkbarstore.com
- Magnolia Bakery: shopify.com/blog/how-to-perfect-the-shopping-experience-for-customers-no-matter-where-they-are · foodchainmagazine.com · signals.cmgroup.com · semrush magnoliabakery.com
- Crumbl: nrn.com/marketing-branding/how-crumbl-cookies-created-one-of-the-most-popular-apps-in-the-industry · placer.ai · modernretail.co · semrush crumblcookies.com · thepricer.org
- Salt & Straw: qsrmagazine.com (rewards launch) · fastcasual.com · saltandstraw.com/pages/faq · particl.com/company/salt-and-straw
- Talabat background: en.wikipedia.org/wiki/Talabat · Deliveroo Kuwait desserts: deliveroo.com.kw/en/cuisines/dessert-takeaway/kuwait
