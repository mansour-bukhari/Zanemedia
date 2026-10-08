# Growth Action Plan — onlykw.com ("Only")

_Prepared: 2026-10-08 · Companion to `COMPETITOR_BENCHMARK_ANALYSIS.md`_

---

## 1. The one-paragraph thesis

Only has proven product–market fit:
- 1.2% CTR on Meta.
- A 13.6% landing-page-view → purchase rate.
- A hero SKU (Mango Cake, 7.750 KWD, serves 7–9) priced at roughly half of what Floward and Bleems charge for same-day cakes.

The business loses money in three places:
1. **57% of paid clicks never load the page** (6,522 link clicks → 2,784 LPVs).
2. **AOV is about one item** (~11.2 KWD), with no threshold, size ladder or add-ons.
3. **There is no owned retention channel**, so every order is bought at a ~8.6 KWD CPA.

Fix those three, in that order, before increasing spend.

### Target scorecard (90-day goal)

| KPI | Now (Meta, last 90d) | 90-day target | Rationale |
|---|---|---|---|
| Click → LPV | 42.7% | **≥ 70%** | Regional/global norm 70–85% |
| IC → Purchase | 55.6% | **≥ 65%** | Payment-native checkout norm |
| AOV | ~11.2 KWD ($36.6) | **≥ 14 KWD** | Threshold + bundles (Fantastic Choc. 20 KWD, Floward 25 KWD) |
| Meta ROAS | 1.30 | **≥ 2.2** | See impact model below |
| Meta CPA | $28.2 | **≤ $19** | |
| Owned-channel revenue share (WhatsApp/email) | ~0% | **≥ 15%** | Global benchmarks 25–35% |
| Repeat-purchase rate (60d) | unknown | **measure → ≥ 25%** | Magnolia ~30% |

### Impact model (estimates, Meta only, same spend)

| Lever | Multiplier on ROAS | Cumulative ROAS |
|---|---|---|
| Baseline | — | 1.30 |
| Click→LPV 42.7% → 70% (assume only ~60% of the gain converts at today's rates) | × ~1.38 | ~1.80 |
| IC→Purchase 55.6% → 65% | × 1.17 | ~2.10 |
| AOV 11.2 → 14 KWD | × 1.25 | **~2.6** |

_These are directional. The model doesn't count repeat revenue from the retention layer, which is pure upside on top._

---

## 2. Prioritised roadmap

Priority = Impact × Confidence ÷ Effort. **P0 = this week**, P1 = weeks 2–4, P2 = month 2, P3 = month 3+.

### Phase 0 — Week 1: Measure & stop the bleeding

| # | Action | Owner | Effort | Why / competitor proof |
|---|---|---|---|---|
| P0-1 | **Page-speed and in-app-browser audit.** Test onlykw.com in the Instagram, Facebook and Snapchat in-app browsers on a mid-range Android over 4G. Measure LCP and TTFB with PageSpeed Insights mobile. Target LCP < 2.5s. Compress hero images to WebP/AVIF ≤ 150 KB, lazy-load below-fold, remove render-blocking scripts, preconnect to the CDN and payment gateway. | Dev | S | 57% click→LPV loss is the single largest leak. |
| P0-2 | **Check pixel firing.** Check that the Meta Pixel's PageView/LPV fires early, before heavy scripts. Add **Meta Conversions API** (server-side) and **Snap CAPI** with event deduplication. | Dev / Media | S–M | Part of the LPV gap may be under-measurement. CAPI also improves optimisation signal. |
| P0-3 | **Install GA4 + funnel events** (`view_item`, `add_to_cart`, `begin_checkout`, `add_payment_info`, `purchase`) and connect it to the agency's GA4 stack. Use consistent UTMs on every Meta, Snap and IG link-in-bio URL. | Dev / Media | S | No GA4 property exists for onlykw today, so the funnel can't be seen beyond Meta's view. |
| P0-4 | **Checkout drop-off diagnosis.** Record 20 sessions (Microsoft Clarity, free) and log payment-step failures (KNET redirect returns, OTP timeouts). Confirm **Apple Pay** is live and shown first on iOS. | Dev | S | IC→Purchase 55.6% vs 65–75% norm. |
| P0-5 | **Media hygiene.** Cut **Nutella Cookies – Static** ($171, 0 purchases). Cap or refresh **New Sales Adv+ (22 Jul)** (ROAS 0.97, frequency 4.1). Shift budget to **Sales Adv+** (1.60) and the **Luqmah cake** and **Mango Bites – Static** (2.12) creatives. | Media | S | Immediate efficiency gain. |

### Phase 1 — Weeks 2–4: AOV & conversion architecture

| # | Action | Effort | Competitor reference |
|---|---|---|---|
| P1-1 | **Quantified delivery promise everywhere**: header bar, PDP, cart, ads. E.g. "توصيل خلال ٩٠ دقيقة" / "Delivered in 90 min" or a same-day cutoff ("Order by 9 PM, delivered today"). Only promise what operations can hit 95% of the time. | S | Fantastic Chocolate, Bleems, Floward all lead with "90 min". |
| P1-2 | **Free-delivery threshold at ~15 KWD** (≈1.35× current AOV), with a **progress bar in cart**: "Add 2.250 KD for free delivery 🚚". Optional second tier: free gift at 20 KWD (e.g. 6 Nutella cookies). | S | Fantastic Choc. free gift >20 KWD; Floward free >25 KWD; Milk Bar $100. |
| P1-3 | **Size/quantity ladder** on hero SKUs: Mango Cake **Small (serves 4–5) / Large (serves 7–9)**; Bites **10 / 20 / Party 40 pcs**. Display **"serves X"** and **price per person** prominently. | M (ops + menu) | Fantastic Choc. S/L with servings; Crumbl 4/6/party. |
| P1-4 | **Rebuild combos as "Gathering Boxes"**, named for occasions: _Diwaniya Box_, _Ghabga Box_, _Guests Box_. E.g. Mango Cake + 10 Mango Bites at ~14.5 KWD (vs 15.7 separately). Make one box the default hero on the homepage. | S | Magnolia hero + sides bundle; Milk Bar combos. |
| P1-5 | **Slide-out cart drawer with 1-tap add-ons**: candles, a "Happy Birthday" topper/card, 6-pc cookies, a second bites flavour at a small discount ("Add Cocoa Bites for 5.950 instead of 7.950"). | M | Salt & Straw "6th pint for $10"; Floward balloons/cards. |
| P1-6 | **PDP rebuild (mobile-first)**: <br>• **9:16 video first** (reuse the winning reels/UGC) <br>• Servings + price-per-person <br>• "Best served cold — keep refrigerated, enjoy within 48h" freshness note <br>• **Delivery date/slot picker** with same-day cutoff countdown <br>• Gift-message field <br>• Payment badges (KNET, Apple Pay, Visa/MC, Tabby/Deema if offered) <br>• Reviews/UGC block <br>• Sticky "Add to cart" bar | M | Milk Bar date picker + gift notes; Bateel ETA widget; Salt & Straw guarantee copy. |
| P1-7 | **Freshness guarantee**: "Arrives cold & perfect, or we replace it free." | S | Salt & Straw Melt-Free Guarantee. |
| P1-8 | **Checkout**: phone-number-first (Kuwait mobile) with OTP login, **guest checkout**, **Kuwait address autocomplete by Area → Block → Street → House** with Google Maps pin, Apple Pay express button above the form, saved addresses for repeat buyers. | M | All GCC leaders; reduces the 44% IC drop. |
| P1-9 | **Ad → page message match**: send each creative to its product page or Gathering Box, never the homepage. Today 50+ creatives point to the homepage. Add a Mango-Bites-first landing page for the 2.12 ROAS static. | S | — |

### Phase 2 — Month 2: Owned channels & retention engine

**Channel choice:** WhatsApp is the GCC's SMS. Use **Klaviyo** as CRM/ESP (email + WhatsApp, already in the agency toolset) or a WhatsApp-native BSP (e.g. WATI, Interakt). Meta Business verification and template approval are needed (see the agency's `klaviyo-whatsapp-architect` SOP).

| # | Playbook | Mechanics | Expected effect [I] |
|---|---|---|---|
| P2-1 | **Capture** | Mobile popup after 8s or 40% scroll. Offer **free delivery on first order** (not a % discount: protects margin) in exchange for a **WhatsApp number** (primary) or email. Checkout opt-in checkbox for WhatsApp order updates (pre-ticked where compliant). Target: 6–10% capture rate. | List growth of ~1–2K/month at current traffic |
| P2-2 | **Transactional WhatsApp** | Order confirmed → out for delivery (driver ETA) → delivered + "Rate your dessert ⭐" (collects reviews for PDP). | Trust, fewer "where's my order" DMs, review volume |
| P2-3 | **Abandoned checkout** | WhatsApp at 30 min ("Your mango cake is waiting 🥭"), email at 4h, WhatsApp at 20h with free-delivery nudge. | Recovers 8–15% of abandoned checkouts (~300/90d today) |
| P2-4 | **Browse abandonment** | Email/WA at 2h for identified visitors who viewed a PDP. | — |
| P2-5 | **Post-purchase cross-sell** | Day 3: "Tried the Mango Cake? Meet the Tiramisu Bites." Day 10: Gathering Box for the weekend. | Drives 2nd order |
| P2-6 | **Occasion calendar** | Capture birthday/anniversary at checkout ("Remind me before…"). Automated reminder 3 days before with a pre-built box. Seasonal pushes: Ramadan (post-iftar, already a proven hook in ads), Eid, National Day/Liberation Day (Feb 25–26), back-to-school, summer heat. | High-intent repeat orders |
| P2-7 | **Winback** | 45/75 days since last order: new-flavour drop + free delivery. | — |
| P2-8 | **Meta/Snap audiences from CRM** | Sync purchaser lists for exclusion from prospecting and as 1%–3% lookalike seeds. Retarget ATC/IC 7-day with a Gathering Box creative. | Lowers CPA. Stops paying to re-acquire customers. |

### Phase 3 — Month 3+: Loyalty, drops & channel expansion

| # | Initiative | Detail | Reference |
|---|---|---|---|
| P3-1 | **"Only Club" loyalty, shown as KWD** | 1 point per 100 fils. **1,000 pts = 1 KWD off**. Bonus points for account creation, birthday, review with photo, referral. Phone-number based (no app needed). | Crumbl "100 Crumbs = $10"; Milk Bar First Bite Club. |
| P3-2 | **Referral: give 2 KWD, get 2 KWD** | Shareable WhatsApp link (Kuwait shares on WhatsApp, not email). | Milk Bar $15 referral. |
| P3-3 | **Monthly flavour drop** | One limited bite or cake flavour per month (e.g. Pistachio Bites, Saffron-Mango Cake, Lotus Tiramisu). Teased on Snap/IG Sunday night; **WhatsApp list gets 24h early access**. Retire it on schedule (manufactured scarcity). | Crumbl weekly drop; Magnolia monthly pudding (+5% category sales); Salt & Straw early access. |
| P3-4 | **"Bites Club" subscription** | Weekly or monthly bites box, skip-able. Prepaid 3/6 months at 10/15% off. Start with a waitlist to validate demand. | Salt & Straw Pints Club; Crumbl Taste Weekly. |
| P3-5 | **Corporate & events** | Bulk-order form (offices, diwaniyas, weddings, Ramadan ghabgas) with tiered pricing. | Floward/Milk Bar corporate gifting. |
| P3-6 | **Marketplace as a channel** | List the Mango Cake and a Gathering Box on **Bleems** (gifting reach) and test Talabat/Deliveroo for impulse demand at marketplace-adjusted prices. Use insert cards to pull those buyers to the DTC site and loyalty. | Bleems already hosts Kuwaiti mango/tiramisu rivals; Magnolia uses aggregator-exclusive flavours. |
| P3-7 | **Category SEO (Arabic + English)** | Build collection/landing pages and 6–8 articles targeting "كيكة مانجو الكويت", "حلى توصيل الكويت", "mango cake Kuwait", "ice cream bites Kuwait", "best desserts for gatherings Kuwait". Add Product + Review schema and a Google Business Profile. | Fantastic Chocolate's "Best Ice-Cream Cakes in Kuwait" blog. |
| P3-8 | **Google Search & Shopping** | Brand defence plus "mango cake delivery Kuwait" exact match; Performance Max fed from the existing Meta product catalog/feed. | Diversifies away from 100% paid social. |

---

## 3. Tech stack enhancements

| Layer | Current (observed / inferred) | Recommendation | Priority |
|---|---|---|---|
| Platform | Non-Shopify SaaS/custom (`/product/<cat>/<slug>`) [I] | If the current platform can't support a cart drawer, thresholds, a slot picker, a size ladder and fast mobile load **within 4 weeks**, evaluate **Shopify (Markets, KWD) + a GCC-native payment app** (Tap / MyFatoorah / UPayments for KNET, Apple Pay, Tabby/Deema). Otherwise optimise in place. **Don't re-platform before P0 is done.** | P1 decision |
| Payments | Unverified | KNET + Apple Pay (express, above the fold on iOS) + Visa/MC. Test Tabby/Deema only on boxes ≥ 15 KWD. | P0–P1 |
| Tracking | Meta Pixel ✅, Catalog ✅, Snap Pixel (implied), GA4 ❌ | GA4 + Meta CAPI + Snap CAPI + TikTok Pixel/Events API (before testing TikTok) + Microsoft Clarity. | P0 |
| CRM/ESP | None evident | Klaviyo (email + WhatsApp + reviews) or WhatsApp BSP + ESP. | P2 |
| Reviews/UGC | None evident | Post-delivery WhatsApp review request → on-site reviews with photos → reused in ads. | P2 |
| Loyalty/referral | None | Klaviyo-native points or a lightweight loyalty app. | P3 |
| Delivery ops | Unknown | Slot capacity management, driver-ETA link in WhatsApp, delivery-zone fee table. Cutoff time shown live on the site. | P1 |

---

## 4. Creative & media playbook (from first-party data)

1. **Scale what works.** "Luqmah cake"-style UGC (231 purchases, ROAS 1.51–1.70) and the **Mango Bites static** (ROAS 2.12, AOV $46). Brief 5 new variants of each per fortnight: same hook, new opener, new talent, new caption.
2. **Statics beat polished reels for the cake.** Mango-cake reels run at 0.84–1.10 versus 1.58 for the static. Keep reels for awareness/Snap; use statics and UGC for conversion.
3. **Lead with the offer once P1 ships.** "Gathering Box — serves 10 — 14.5 KD — delivered in 90 min, free delivery."
4. **Account structure.** Consolidate into one Advantage+ Sales campaign for scaled winners, one testing campaign (~20% of budget), and one retargeting/CRM-exclusion setup. Keep 90-day prospecting frequency under 3.5.
5. **Snapchat.** Keep Sales objective. Mirror the Meta winners in 9:16. Add Snap CAPI (P0-2) before judging Snap ROAS.
6. **Hooks bank (Arabic, proven tone).**
   - Challenge: "نتحدى فيها"
   - Self-indulgence: "خلصت العلبة بروحي"
   - Moment: "بارد بعد الفطور"
   - Climate: "حلى منعش يناسب حر الكويت"
   - Hosting: "حلو يبيض الوجه"
   - **New:** "يكفي ١٠ أشخاص بأقل من دينار للشخص" (serves 10 for under 1 KD per person: a value-per-serving angle competitors don't use).

---

## 5. 30-60-90 checklist

**Days 1–7 (P0)**
- [ ] Page-speed fixes shipped; in-app browser test passed
- [ ] GA4 + CAPI (Meta, Snap) live with dedup verified in Events Manager
- [ ] Clarity recording; payment-step failure log
- [ ] Nutella Cookies static paused; budget moved to winners

**Days 8–30 (P1)**
- [ ] Delivery promise quantified site-wide
- [ ] 15 KWD free-delivery threshold + cart progress bar
- [ ] Gathering Boxes live; size ladder on Mango Cake and Bites
- [ ] PDP rebuild (video, servings, slot picker, gift note, badges, sticky ATC)
- [ ] Checkout: phone-first, Apple Pay express, Kuwait address format
- [ ] Ads deep-link to PDPs/boxes

**Days 31–60 (P2)**
- [ ] WhatsApp Business API verified; Klaviyo (or BSP) connected
- [ ] Popup capture live (free delivery on first order)
- [ ] Flows: transactional, abandoned checkout, browse, post-purchase, winback, occasion reminders
- [ ] Purchaser audiences synced to Meta/Snap

**Days 61–90 (P3)**
- [ ] First monthly flavour drop with WhatsApp early access
- [ ] Only Club loyalty + referral
- [ ] Bleems listing live; SEO pages published; Google Search/PMax test
- [ ] Bites Club waitlist launched

---

## 6. Open questions for the Only team

1. Real delivery SLA and coverage. Can operations commit to "90 minutes" or a same-day cutoff?
2. Current platform and payment provider. What can be changed without the vendor?
3. Gross margin per SKU and delivery cost per order. This sets the threshold (15 KWD proposed) and the max CPA.
4. Can production support a small/large cake and a 40-pc party size?
5. Repeat-purchase data from the order database (export by phone number) to set the retention baseline.
6. Is the "Only Mango" → "Only" rebrand complete? `onlymangokw.com` should 301-redirect to onlykw.com, and both IG handles should be consistent.
