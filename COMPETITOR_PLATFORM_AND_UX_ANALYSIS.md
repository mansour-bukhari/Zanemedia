# Competitor Platform & UX Analysis
### Premium dessert, confectionery & edible-gifting DTC: GCC/MENA and international

_Prepared: 2026-10-08_

---

## Platform Comparison Matrix

| Competitor | URL | Region / Market | Detected CMS / Platform | Theme / Design Style | Primary USP | Key Feature Worth Emulating |
|---|---|---|---|---|---|---|
| **Fantastic Chocolate** | fantasticchocolatekw.com/en-kw | Kuwait | **Shopify** ✅ DNS + Shopify Markets URLs | Catalog-heavy, promo-banner driven, bilingual | Free delivery **within 90 min**, 10:30–23:30 | Servings per size (S 4–5 / L 8–10) and a **free gift over 20 KD** threshold |
| **Saadeddin** | saadeddin.com | KSA (100+ branches) | **Shopify** ✅ DNS | Heritage/traditional sweets catalog | Brand legacy plus wide aggregator coverage | Runs its own Shopify store alongside HungerStation, Ninja and ToYou |
| **Mirzam** | mirzam.com | UAE → GCC | **Shopify** ✅ DNS | Minimalist luxury, editorial, origin storytelling | Bean-to-bar, Arabian-spice flavours | Gift-wrap option and occasion boxes (Ramadan dates from 45 AED) |
| **Bateel** | bateel.com/en_kw | KSA/UAE + Kuwait boutique | **Magento 2 / Adobe Commerce** ✅ agency case study, behind Cloudflare | Luxury gourmet, gold/black, occasion collections | Premium gifting; free shipping above 9 KWD | Elasticsearch navigation and a PDP estimated-delivery widget |
| **Floward** | floward.com/en-kw | Kuwait-founded, GCC + UK | **Custom build** (Cloudflare; Angular + Braze per RocketReach, unverified) + native apps | App-first, occasion-led, bright gifting UI | Same-day delivery (~90 min average), date/slot scheduling | Occasion → recipient → slot flow, add-ons (balloons, cards), free delivery over 25 KWD |
| **Bleems** | bleems.com/kw | Kuwait → GCC (6 markets) | **Custom marketplace** (Azure-hosted ✅ DNS) + iOS/Android | Dense marketplace grid, vendor storefronts | 3 delivery modes: **90 min / same day / pick a date** | Delivery mode as a first-class filter; ~5,400 confection SKUs filterable by price band |
| **Joy Confections** (Kuwait home-grown tier) | joyconfections.com | Kuwait | **Zyda** ✅ DNS CNAME `joyconfections.zyda.com` | Template ordering menu | Local bakery, zero-commission ordering | Delivery-zone pricing and WhatsApp/social order intake out of the box |
| **Milk Bar** | milkbarstore.com | US, nationwide shipping | **Shopify** ✅ DNS | Playful maximalist, bold colour, illustrated | Iconic cult SKUs; shipped nationwide | Delivery-date picker (up to 30 days), recipient-scheduled e-gift, "First Bite Club" loyalty |
| **Magnolia Bakery** | magnoliabakery.com | US + int'l franchises (incl. Kuwait 360 Mall) | **Shopify** ✅ DNS (Shopify case study) | Classic, soft pastel, hero-SKU-led | Hero SKU (banana pudding), same-day local + national shipping | Monthly rotating flavour of the hero SKU; IA split into 3 jobs (shop / find store / grocery) |
| **Crumbl** | crumblcookies.com + app | US/Canada (1,000+ stores) | **Proprietary app + web** (Cloudflare) | App-first, pink brand system, weekly menu cards | Weekly rotating menu (scarcity) | Weekly drop mechanic, points shown as cash (100 Crumbs = $10) |
| **Salt & Straw** | saltandstraw.com | US + nationwide shipping | **Shopify** ✅ DNS | Craft/artisan, flavour-story-led | Chef-driven seasonal flavours | 5-pack minimum + discounted 6th unit; Melt-Free Guarantee; "Pints Club" subscription |

✅ = confirmed by DNS fingerprint (CNAME `shops.myshopify.com` / Shopify IP 23.227.38.x, Zyda CNAME, Azure IP) or a primary source. Everything else is labelled per row.

### Platform distribution (DNS-verified, wider sample)

| Platform | Brands |
|---|---|
| **Shopify / Shopify Plus** | Fantastic Chocolate, Khobz (KW), Saadeddin (KSA), Mirzam (UAE), Milk Bar, Magnolia Bakery, Salt & Straw, Levain Bakery, Jeni's, Last Crumb, Godiva |
| **Magento / Adobe Commerce** | Bateel (case study), Lenôtre (`prod.magentocloud.map.fastly.net`) |
| **GCC ordering SaaS** | Joy Confections (**Zyda**), Bakerista and November & Co (**Ordable** subdomains) |
| **Custom / headless** | Floward, Bleems (Azure), Crumbl, FNP |
| **Site builders** | Bubbies Mochi (**Webflow**), The Gelato Shop (**Wix**) |
| **Enterprise CDN, platform masked** | Al Rifai (Akamai), Patchi (Cloudflare) |

**Read-out:** Shopify dominates single-brand dessert DTC in both markets, including GCC (Fantastic Chocolate, Saadeddin, Mirzam, Khobz). Custom stacks appear only at marketplace or multi-vendor scale (Floward, Bleems) or app-first franchise scale (Crumbl). Local ordering SaaS (Zyda, Ordable) is the entry tier for Kuwaiti home-grown bakeries. It is fast to launch, but design and app extensibility are limited.

---

## Methodology & Verification

- **Platform detection:** live DNS resolution of each storefront hostname. A CNAME to `shops.myshopify.com` or an A record in Shopify's 23.227.38.0/24 range means Shopify. `*.zyda.com` means Zyda. `magentocloud…fastly.net` means Adobe Commerce Cloud. `cdn.webflow.com` and `wixdns.net` mean Webflow and Wix. This is a reliable platform signal.
- **Not observed directly:** this research environment's network policy blocked HTTPS fetches of every storefront. So **page source, theme names and third-party app scripts could not be read**. App and UX details below come from the brands' indexed pages, app-store listings, case studies and trade press. They are tagged **[Observed-indexed]**, **[Reported]** or **[Inferred]**.
- **5-minute verification per site** (desktop Chrome, view-source / DevTools → Network):

| Signal | Look for |
|---|---|
| Shopify | `cdn.shopify.com`, `Shopify.theme` (gives the **theme name** + id), `/products/<handle>.js`, `shopify-digital-wallet` meta |
| Magento | `/static/version…/frontend/`, `mage/`, `requirejs-config.js`, `form_key` |
| Salla / Zid | `cdn.salla.sa`, `salla.config`; `media.zid.store`, `zid.store` |
| WooCommerce | `wp-content/plugins/woocommerce`, `wc-ajax` |
| Next.js / headless | `__NEXT_DATA__`, `/_next/static/` |
| Angular | `ng-version` attribute |
| Reviews | `loox.io`, `staticw2.yotpo.com`, `okendo`, `judge.me`, `stamped.io` |
| Email/SMS/WA capture | `static.klaviyo.com`, `attn.tv` (Attentive), `postscript`, `privy`, `wati`/`interakt` widgets |
| Upsell / cart | `rebuyengine.com`, `upcart`, `monster-cart`; subscriptions `rechargecdn`, `skio` |
| Search | `algolia`, `searchanise`, `boost-commerce`, `klevu` |
| Loyalty | `smile.io`, `loyaltylion`, `yotpo-loyalty`, `rivo` |

---

## Tier A — GCC / MENA Competitors

### A1. Fantastic Chocolate — fantasticchocolatekw.com (Kuwait)

**1. Platform & stack**
- **Shopify** ✅: apex on 23.227.38.32; `www` CNAME → `shops.myshopify.com`.
- **Shopify Markets** sub-folder localisation: `/en-kw/collections/…` [Observed-indexed].
- A secondary storefront domain, `fantasticchocolate.shop`, also on Shopify ✅, is likely a separate market or campaign store.
- Native Shopify blog (`/blogs/news/…`) used for SEO content.
- **WhatsApp ordering line** (98821515) shown on collection pages [Observed-indexed].
- Theme and apps: unverified. Check the `Shopify.theme` object.

**2. Design & UX**
- Catalog-heavy, promo-banner-led homepage with best-sellers rails. Collections by type: Cakes & Basbosa, Ice-Cream Cakes & Treats, Best Sellers [Observed-indexed].
- **PDP:** variant selector by size, with **servings stated per variant** (Small 4–5 / Large 8–10) and the price change shown per size (9.990 / 14.990 KWD) [Observed-indexed].
- Handling and storage guidance in content: delivered frozen in insulated packaging; take out 15–20 min before serving.
- Cart: standard Shopify cart/checkout [Inferred].
- **Friction point:** the "90-minute delivery" banner conflicts with "order ice-cream cakes a day ahead". The promise isn't scoped per product [Observed-indexed].

**3. USPs & promotions**
- **Free delivery** · **delivered within 90 minutes** · ordering hours 10:30 AM–11:30 PM.
- **Free chocolate box on orders ≥ 20 KD** (gift-with-purchase threshold).
- Content-SEO hooks: "Best Ice Cream Cakes in Kuwait", "Best Ice Cream Flavors to Try in Kuwait".

**4. Conversion & retention**
- WhatsApp as the assisted-sales and support channel.
- Popup and loyalty: not evidenced.

**Emulate:** servings-per-variant on the PDP, a gift-with-purchase threshold, Shopify Markets bilingual sub-folders, and category blog posts targeting "best X in Kuwait" queries.

---

### A2. Saadeddin — saadeddin.com (KSA)

**1. Platform & stack**
- **Shopify** ✅: `www` CNAME → `shops.myshopify.com`; apex on 23.227.38.65.
- A notable contrast to its aggregator-first ordering. The brand keeps its own Shopify store while most delivery volume runs through **HungerStation, Ninja, ToYou, Talabat and Snoonu** [Reported].
- BNPL (Tabby/Tamara): not evidenced.

**2. Design & UX**
- Heritage sweets catalog: pastries, cakes, chocolates, Arabian sweets, ice-cream cakes, chocolate baklava [Reported].
- Large range, so filtering and category depth matter more than PDP storytelling [Inferred].

**3. USPs & promotions**
- Legacy brand (100+ branches), breadth of range, and nationwide availability through delivery apps.

**4. Conversion & retention**
- Not evidenced on the web store. Retention likely sits in branches and aggregators [Inferred].

**Emulate:** use the DTC site for brand, catering and pre-orders, and the aggregators for impulse demand. Don't force one channel to do both jobs.

---

### A3. Mirzam Chocolate Makers — mirzam.com (UAE → GCC)

**1. Platform & stack**
- **Shopify** ✅: `www` CNAME → `shops.myshopify.com`.
- Website plus an app referenced for Ramadan ordering [Reported].
- Products are wholesaled to third-party Shopify retailers (TWIGS, Bar & Cocoa) [Observed-indexed].

**2. Design & UX**
- Minimalist luxury: origin and spice-route storytelling, illustrated packaging as the visual hero.
- Products split into bars, truffles, gift boxes and seasonal (Ramadan dates).

**3. USPs & promotions**
- Bean-to-bar, Arabian-inspired flavours (saffron, rose, cardamom, dates).
- **GCC-wide shipping** with a **gift-wrapping option** [Reported].
- Ramadan date boxes from 45 AED.

**4. Conversion & retention**
- Seasonal campaigns (Ramadan, Eid, National Day). Loyalty: not evidenced.

**Emulate:** packaging-as-hero product photography, a gift-wrap toggle on the PDP or in the cart, and a seasonal capsule collection page.

---

### A4. Bateel — bateel.com/en_kw (KSA/UAE, Kuwait boutique)

**1. Platform & stack**
- **Magento 2 / Adobe Commerce** ✅. A Krish TechnoLabs case study covers managed support and a redesign. Store-view URLs: `/en_kw/…html`.
- Behind Cloudflare.
- **Elasticsearch** for search and navigation, **multiple payment gateways**, integrated inventory/OMS and **express delivery** [Reported].
- Agency-reported results (unverified): +237.8% conversions, +18.25% revenue, 235 AED AOV.

**2. Design & UX**
- Luxury gourmet: dark/gold palette, large lifestyle imagery, occasion-led navigation (Ramadan, National Day, corporate).
- **PDP:** estimated-delivery widget, gift-set compositions [Observed-indexed].
- Multi-store selector (country/language).

**3. USPs & promotions**
- **Free shipping above 9 KWD** (100 AED UAE).
- Processing within 24h, **2–5 working-day delivery (no same-day)**.
- Corporate gifting.

**4. Conversion & retention**
- Boutique and café integration; seasonal collections. Loyalty programme: unverified.

**Emulate:** occasion collections as top-level nav, a PDP ETA widget, and visual-storytelling PDPs. Avoid the slow delivery promise: it's Bateel's weak spot.

---

### A5. Floward — floward.com/en-kw (Kuwait-founded; GCC + UK)

**1. Platform & stack**
- **Custom platform** (Cloudflare-fronted). Third-party tech profile lists **Angular, Braze (CRM/push), Google Tag Manager** [Reported, RocketReach, unverified].
- AWS/PostgreSQL backend per the CTO's public profile.
- **Native iOS/Android apps** carry much of the volume.
- Product URLs: `/buy-and-send-…-<id>.html`.

**2. Design & UX**
- App-first gifting UI. Navigation by **occasion → product type → recipient**.
- Collections such as "Same-day cakes".
- **PDP:** add-ons (helium balloons 1 KWD, cards), personalised photo cakes.
- **Checkout:** delivery date + time slot, or same-day [Observed-indexed].
- **Friction point:** the on-time guarantee excludes edible items [Observed-indexed].

**3. USPs & promotions**
- Same-day delivery (~90 min average fulfilment per the founder).
- **Free delivery over 25 KWD** (seen on a PDP).
- **Bank partnerships** (NBK 15% code), Floward Cards (Boubyan prepaid Visa) [Observed-indexed].

**4. Conversion & retention**
- App push and CRM via Braze [Reported], occasion reminders, subscriptions (flowers).

**Emulate:** an add-on rail on the PDP and in the cart, a date/slot picker, bank-card promo partnerships, and occasion reminders.

---

### A6. Bleems — bleems.com/kw (Kuwait → 6 GCC markets)

**1. Platform & stack**
- **Custom marketplace**: `www.bleems.com` resolves to Microsoft **Azure** (51.104.28.64), with a `bleems-pci.azurewebsites.net` mirror [Observed-indexed]. Likely .NET [Inferred].
- **iOS app** 4.2★ from about 12K ratings [Reported].

**2. Design & UX**
- Dense marketplace grid. Vendor storefronts (e.g. `/confectionery/joyconfections/…`).
- **Filters:** price bands (under 10 / 10–20 / 20–30 KWD), vendor, and **delivery type**.
- **Delivery mode as a top-level choice:** "90 minutes delivery" / "Same day delivery" / "Pick a date" [Observed-indexed].
- Ordering steps: choose when and where to deliver plus a personalised message; combos bundle items [Reported].

**3. USPs & promotions**
- Breadth (~5,400 confection SKUs), 90-minute option, GCC coverage, gifting combos.

**4. Conversion & retention**
- App-driven; order tracking. Loyalty: not evidenced.

**Emulate:** **delivery-speed filtering** ("Deliver in 90 min") and price-band filters. It's also a listing channel for local dessert brands.

---

### A7. Kuwait home-grown tier — Joy Confections (Zyda), Bakerista & November & Co (Ordable), Khobz (Shopify)

| Brand | Platform (verified) | Notes |
|---|---|---|
| Joy Confections | **Zyda** ✅ CNAME `joyconfections.zyda.com` | Template menu; delivery-zone pricing; social/WhatsApp order intake; zero commission; online payments (KNET etc.) [Reported] |
| Bakerista / November & Co | **Ordable** ✅ subdomains | Kuwaiti zero-commission storefront; supports KNET, Tap, MyFatoorah, UPayments, Hesabe [Reported] |
| Khobz | **Shopify** ✅ | Next-day only, **3 PM cutoff**, 3 KWD minimum order; tiramisu cake 12 KWD [Observed-indexed] |

**Read-out:** Zyda and Ordable give fast KNET-ready launch and zone-based delivery fees, but little design differentiation, few marketing apps, and weak SEO. Brands that move to Shopify (Khobz, Fantastic Chocolate) gain theme control, Markets localisation and the app ecosystem.

---

## Tier B — International DTC Benchmarks

### B1. Milk Bar — milkbarstore.com (US)

**1. Platform & stack**
- **Shopify** ✅ (Plus-scale brand).
- Email/SMS: migrated **Klaviyo + Attentive + Yotpo → Sendlane** (2023), reporting +27% email/SMS revenue in 3 months (vendor claim) [Reported].
- Separate multi-recipient gifting platform [Reported].
- Cart/upsell and review apps: unverified.

**2. Design & UX**
- Playful maximalist brand system: bright colour blocks, hand-drawn type, product-as-character photography.
- Nav by product (cakes, truffles, cookies) and **occasion/seasonal "shops"** (Fall, Summer, Holiday).
- **PDP:** shipping and packaging explained (insulated, ice-packed); "schedule arrival 3+ days before your celebration" copy.
- **Checkout:** delivery-date picker up to 30 days ahead (adding items can change date options), gift note [Observed-indexed].
- **E-gift flow:** recipient picks date, address, even flavour [Reported].

**3. USPs & promotions**
- Cult SKUs, gift-ready packaging, **free shipping on $100+** collections, combo boxes ("cake + truffles").

**4. Conversion & retention**
- **First Bite Club** loyalty, auto-enrolled on account creation:
  - 1 pt per $1
  - birthday +10
  - review +15
  - referral +100
  - rewards paid in product (e.g. a pie slice)
- **$15 referral.**
- Birthday reminders [Reported].

**Emulate:** a date picker with lead-time copy, recipient-led e-gifting, and points that redeem for product rather than discounts.

---

### B2. Magnolia Bakery — magnoliabakery.com (US + franchises)

**1. Platform & stack**
- **Shopify** ✅, used "to streamline all points of sale" [Reported: Shopify blog].
- Sailthru email (historic); Amex Offers acquisition partnership (>10x ROI) [Reported].
- Also sells on Goldbelly, Uber Eats and DoorDash.

**2. Design & UX**
- Classic, soft pastel, nostalgic photography.
- **IA split into three jobs:** order online · find a bakery · find grocery products (dynamic store locator) [Reported].
- Same-day local delivery/pickup separated from nationwide shipping flows.
- **Hero SKU** (banana pudding) anchors navigation and bundles. E.g. large pudding + 2 cupcakes ≈ $35 [Reported, unofficial].

**3. USPs & promotions**
- Iconic hero product.
- **Monthly rotating pudding flavour** (12+ flavours; lifted category sales by more than 5%).
- Aggregator-exclusive flavours.

**4. Conversion & retention**
- Segmentation and A/B testing → ~40% conversion-rate lift; ~30% returning-customer rate [Reported: CM Group session].

**Emulate:** a hero-SKU-centred IA, a monthly flavour rotation of the hero, and separate fulfilment flows for "today" and "scheduled".

---

### B3. Crumbl — crumblcookies.com + app (US/Canada)

**1. Platform & stack**
- **Proprietary native app + web ordering** (Cloudflare-fronted; not Shopify) [DNS + Inferred].
- First-party app pushes pickup and delivery to avoid aggregator markups [Reported].

**2. Design & UX**
- App-first, signature pink brand system, overhead product shots on uniform backgrounds.
- **Weekly menu cards** are the primary navigation: 4–6 rotating flavours + a permanent classic.
- Pack-size selector (single, 4-pack, 6-pack, party box).

**3. USPs & promotions**
- **Weekly drop:** flavours revealed Sunday night/Monday and retired after a week (manufactured scarcity).
- 4-pack $16–20, 6-pack $23–27.

**4. Conversion & retention**
- **Crumbl Rewards:** "Crumbs" on every order, **100 Crumbs = $10** Crumbl Cash, account-creation bonus.
- "Taste Weekly" subscription.
- Instagram is ~35% of social referrals; massive TikTok presence [Reported].

**Emulate:** a drop calendar with weekly or monthly reveals, points expressed as cash, and pack-size tiers as the default AOV ladder.

---

### B4. Salt & Straw — saltandstraw.com (US)

**1. Platform & stack**
- **Shopify** ✅ (apex and `www` on 23.227.38.32).
- Subscription and loyalty apps: unverified. Check for `rechargecdn` / Skio and the rewards widget.

**2. Design & UX**
- Craft/artisan aesthetic, flavour-story-led PDPs (ingredients and maker narrative).
- Shipping logic surfaced in the cart: **5-pint minimum to ship**; merch ships separately [Observed-indexed].
- FAQ-level trust content on dry-ice packaging.

**3. USPs & promotions**
- **5-pack minimum + 6th pint for $10** (forced bundle + discounted add-on).
- **Melt-Free Guarantee:** free reship if not frozen.
- Monthly flavour series.

**4. Conversion & retention**
- **Pints Club:** 5 pints/month, choose Monthly Flavors / Best Sellers / Dairy-Free, skip-able. Prepaid 3/6/12 months at 10/15/20% off [Reported].
- **Rewards (launched June 2026):** 10 "Spoons" per $1 via app or phone number at checkout; early access to drops; buy 4 get the 5th free [Reported].

**Emulate:** a pack minimum + discounted next unit, a product-quality guarantee badge, phone-number-based loyalty with no app required, and early access to drops for members.

---

## Cross-Competitor Feature Patterns

| Pattern | Who does it best | Implementation note |
|---|---|---|
| Quantified delivery promise ("90 min", cutoff time) | Fantastic Chocolate, Bleems, Floward | Scope the promise per product type: Fantastic Chocolate's 90-min vs "order a day ahead" conflict is a trust leak |
| Delivery mode / date as a filter or first step | Bleems, Floward, Milk Bar | Slot picker on the PDP or in the cart; lead-time warnings |
| Servings & size ladder on PDP | Fantastic Chocolate, Crumbl | Variant label = size + servings + price |
| Threshold mechanics | Fantastic Chocolate (gift ≥ 20 KD), Floward (free delivery ≥ 25 KWD), Bateel (free ≥ 9 KWD), Milk Bar ($100) | Pair with a cart progress bar |
| Forced bundle / discounted next unit | Salt & Straw | "Add one more for X" in the cart drawer |
| Add-on rail (cards, candles, balloons, gift wrap) | Floward, Mirzam | Low-cost, high-margin attach items |
| Rotating drops | Crumbl (weekly), Magnolia, Salt & Straw (monthly) | Drop calendar with member early access |
| Loyalty as cash / product | Crumbl, Milk Bar, Salt & Straw | Phone-number identity suits GCC (WhatsApp-native) |
| Subscription club | Salt & Straw, Crumbl | Skip-able plus prepaid discount tiers |
| Content SEO | Fantastic Chocolate | "Best ___ in Kuwait" articles on the native blog |
| Bank / card partnerships | Floward (NBK), Magnolia (Amex) | Low-CAC acquisition in the GCC |

---

## Sources

- DNS fingerprints: resolved 2026-10-08 from the research environment (CNAME / A-record lookups for every hostname listed).
- Fantastic Chocolate: [Home](https://www.fantasticchocolatekw.com/en-kw) · [Cakes](https://www.fantasticchocolatekw.com/en-kw/collections/cakes) · [Best sellers](https://www.fantasticchocolatekw.com/en-kw/collections/fantastic-best-sellers) · [Best Ice Cream Cakes in Kuwait](https://www.fantasticchocolatekw.com/en-kw/blogs/news/best-ice-cream-cakes-in-kuwait) · [Best Ice Cream Flavors](https://www.fantasticchocolatekw.com/en-kw/blogs/news/best-ice-cream-flavors-to-try)
- Saadeddin: [Talabat](https://www.talabat.com/ksa/saadeddin-pastry) · [HungerStation](https://hungerstation.com/sa-en/restaurant/saadeddin%20pastry/riyadh/al-ulaya/4000) · [Ninja](https://ananinja.com/sa/en/restaurants/saadeddin-7931) · [Snoonu](https://snoonu.com/restaurants/saadeddin-sweets) · [LinkedIn](https://www.linkedin.com/company/saadeddinpastry)
- Mirzam: [TradeArabia](https://www.tradearabia.com/news/RET_335940.html) · [Arabian Business](https://www.arabianbusiness.com/gourmet/397220-ramadan-vegan-chocolate-dates-launched-in-dubai) · [TWIGS](https://twigs.ae/products/mirzam-bustan-truffles-selection-box-of-32)
- Bateel: [Krish TechnoLabs case study](https://www.casestudies.com/company/krish-technoLabs/case-study/bateel-boosts-revenue-1825-with-krish-technolabs) · bateel.com/en_kw (indexed pages)
- Floward: [RocketReach tech profile](https://rocketreach.co/floward-technology-stack_b4573791fca642ce) · [Netguru Disruption Talks](https://podpulse.ai/podcast-notes-and-takeaways/disruption-talks-by-netguru-ep-104-how-technology-can-transform-the-flower-delivery-industry-disruption-talks-with-floward) · floward.com/en-kw (indexed pages)
- Bleems: [App Store](https://apps.apple.com/us/app/-/id569788924) · [Cakes](https://www.bleems.com/kw/confections/cakes) · [Ahrefs](https://ahrefs.com/websites/bleems.com)
- Zyda: [Wamda](https://www.wamda.com/2021/02/zyda-expands-ecommerce-platform-egypt) · [Salaam Gateway](https://salaamgateway.com/story/zyda-expands-into-egypt-offering-restaurants-e-commerce-solutions) · [Foodics portfolio](https://www.foodics.com/portfolio/zyda)
- Ordable: [Foodics portfolio](https://www.foodics.com/portfolio/ordable/) · [Kuwait Times](https://kuwaittimes.com/article/11279/business/ordable-empowering-individuals-to-realize-their-business-dreams/amp)
- Milk Bar: [Sendlane case study](https://sendlane.com/customerstories/milk-bar) · tryperdiem.com · barrelny.com teardown
- Magnolia Bakery: [Shopify blog](https://www.shopify.com/blog/how-to-perfect-the-shopping-experience-for-customers-no-matter-where-they-are) · [Food Chain Magazine](https://foodchainmagazine.com/magnolia-bakery-continues-to-rise-celebrating-global-expansion-and-menu-innovation/)
- Crumbl: [NRN](https://nrn.com/marketing-branding/how-crumbl-cookies-created-one-of-the-most-popular-apps-in-the-industry) · [Nosh](https://www.nosh.com/news/2022/crumbl-sees-rise-in-dtc-rankings-amid-utah-cookie-wars) · placer.ai · thepricer.org
- Salt & Straw: qsrmagazine.com (rewards launch) · fastcasual.com · saltandstraw.com FAQ (indexed)
