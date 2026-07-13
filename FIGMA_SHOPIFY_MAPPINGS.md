# Figma → Shopify Code Mappings

> Complete mapping between Figma "Smart Furniture Final" (JcVbMMKaKPB1kiuusv2tHQ)
> and Shopify Prestige theme codebase. Generated from design context analysis of
> every component and screen.

---

## Design System: Color Palette

Extracted from Figma design tokens — map to Prestige CSS variables or custom scheme overrides.

| Figma Token | Hex | Prestige Mapping | Notes |
|---|---|---|---|
| Shades/Blue/Dark | `#001D43` | `--button-background` / scheme-3 bg | Primary CTA, nav bg |
| Shades/Blue/Normal | `#002659` | Announcement bar bg, footer buttons | Slightly lighter blue |
| Shades/Blue/Dark :hover | `#001735` | Footer headings | Hover/dark variant |
| Shades/Blue/Dark :active | `#001128` | Footer bottom bar bg | Darkest blue |
| Color Palette/Peach | `#EE7857` | Accent/highlight color | Installments CTA, "Last Chance", price callouts |
| Color Palette/Light Blue | `#57B4A9` | Sale badge bg | Discount badges |
| Color Palette/Gray | `#79858D` | Footer subtitle | Muted text |
| Shades/Beige/Normal | `#E8D5BC` | Footer main bg | Warm beige |
| Shades/Beige/Light :active | `#F8F2EA` | Footer upper section bg | Light beige |
| Green (`#05DF72`) | — | 48h delivery badge | No Prestige equivalent |
| Red (`#CB000A` / `#FB2C36` / `#D10000`) | — | Stock warning, Last Chance | No Prestige equivalent |
| Text/Primary | `#0A0A0A` | `--text-color` | Near-black |
| Text/Secondary | `#797979` / `#99A1AF` | `text-subdued` | Gray text |

### Typography

| Figma Font | Weight | Prestige Mapping |
|---|---|---|
| Avenir Regular | 400 | `--text-font-family` (currently Nunito) — **OUTLIER: font mismatch** |
| Avenir Heavy/Black | 800/900 | `--heading-font-family` (currently Instrument Sans) — **OUTLIER** |
| Nexa Bold | 700 | Footer headings, tagline — **OUTLIER: 3rd font not in theme** |
| Inter Medium/Semi Bold | 500/600 | Product card category/title — **OUTLIER: 4th font** |

---

## Component Mappings

### 1. Container (Announcement/USP Bar)
**Figma Node**: `244:4150`
**Shopify**: `sections/announcement-bar.liquid`

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| 4-column USP strip (Factory-direct, Free delivery, 5-year warranty, 30+ showrooms) | Prestige announcement bar supports scrolling text blocks | **OUTLIER**: Figma shows a rich icon+title+subtitle layout per USP; Prestige announcement bar is simple text. Need `sections/text-with-icons.liquid` or a custom section |
| Navy circle icons (`#141E44`, 36px rounded) | Not in announcement-bar | Custom icon styling required |
| Full-width with dividers | Supported via blocks | Divider borders need CSS override |

**Recommendation**: Map to `sections/text-with-icons.liquid` instead. It supports icon + heading + text columns natively.

---

### 2. Header (Left variant)
**Figma Node**: `190:2011` (Property 1=left)
**Shopify**: `sections/header.liquid`

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| Announcement bar (blue `#002659`, delivery/call/branches) | `sections/announcement-bar.liquid` | Content match, needs color scheme override |
| Logo (SF logo, left-aligned, 207×80px) | `header.settings.logo` + `logo_position: "left"` | Direct match |
| Nav items (Bedrooms, Living Rooms, Dining, Storage & More, Kitchens, Collections) | `header.settings.menu` → Shopify menu | Direct match — create menu in Shopify admin |
| "Last Chance" pill (red dot + text, drop shadow) | **OUTLIER**: No equivalent in header nav | Custom mega-menu link styling needed |
| "Installments" orange CTA button in nav | **OUTLIER**: Prestige header doesn't support CTA buttons in nav | Custom CSS/liquid for highlight nav item |
| Search icon | `header-search.liquid` snippet | Direct match |
| Heart/wishlist icon | **OUTLIER**: No native Shopify wishlist | Requires wishlist app (e.g., Wishlist Plus) |
| Catalog icon | **OUTLIER**: Custom icon not in Prestige | Need custom nav icon |
| EN / ع language toggle | `localization-selector.liquid` | Direct match |
| User account avatar (circle, bordered) | `<shopify-account>` custom element | Mostly match — styling override |
| Cart with count badge | `<cart-count>` + `<cart-dot>` | Direct match |

---

### 3. Footer (Beige variant)
**Figma Node**: `440:7604` (Property 1=Beige Footer)
**Shopify**: `sections/footer.liquid`

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| Beige bg (`#F8F2EA` / `#E8D5BC`) | `color_scheme` setting | Need custom color scheme |
| Logo + tagline "Built in Egypt. For Egypt" | Footer supports logo + text block | Direct match via blocks |
| Description paragraph | Rich text block | Direct match |
| Social icons (Facebook, Email, YouTube, LinkedIn, WhatsApp) | `snippets/social-media.liquid` | Direct match — configure URLs in theme settings |
| 4-column link grid (Shop, Company, Help, My Account) | Footer supports multiple menu blocks | Direct match — create 4 menus in Shopify admin |
| "Last Chance" link with icon highlight | **OUTLIER**: Colored/icon links within menu | Custom liquid for menu item highlighting |
| "Installments" highlight in orange | **OUTLIER**: Colored links within menu | Same — custom styling per-link |
| Newsletter signup (email + Subscribe button) | `sections/newsletter.liquid` or footer email block | Direct match |
| Bottom bar (dark `#001128`, policy links + copyright) | Footer bottom bar | Direct match — styling override for dark bg |

---

### 4. Product Card (Container)
**Figma Node**: `244:5577`
**Shopify**: `snippets/product-card.liquid`

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| Card with rounded corners (16px) | `.product-card` | Override `border-radius` — Prestige default is 0 |
| Product image with light gray bg (`#F9FAFB`) | `.product-card__figure` | Direct match — bg color via surface/color scheme |
| Wishlist heart button (top-right, pill shadow) | **OUTLIER**: No wishlist in Prestige | Requires app integration |
| "15% Off" badge (teal `#57B4A9`, pill) | `snippets/product-badges.liquid` → `<on-sale-badge>` | Partial match — color override needed |
| Category label (e.g., "BEDROOM", gray, 12px) | Product type / vendor display | Map to `product.type` display |
| Product title (Inter Medium, 16px) | `.product-card__info` title | Direct match — font override |
| Price with compare-at (20px + strikethrough) | `snippets/price-list.liquid` → `<price-list>` | Direct match |
| Installment callout ("or EGP 2,075 / mo. Valu") | **OUTLIER**: No installment display in product cards | Custom liquid snippet needed |
| "Add to Cart" button (navy `#001D43`, rounded 14px) | `snippets/product-quick-buy.liquid` | Partial match — color/radius override |

---

### 5. Small Card (Horizontal Product Card)
**Figma Node**: `209:11122`
**Shopify**: `snippets/product-card-horizontal.liquid`

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| Horizontal layout (image left, info right) | `product-card-horizontal.liquid` | Structure matches |
| Rounded border container (14px, gray border) | Styling override | Direct — CSS change |
| "15% Off" badge (teal pill on image) | `product-badges.liquid` | Direct match |
| "Delivered in 48h" green pill badge | **OUTLIER**: Custom badge, no Prestige equivalent | Custom metafield + badge snippet |
| Category + product name | Card info area | Direct match |
| Price + installment line | `price-list.liquid` + custom | Partial — installment custom |
| "Add to Cart" outlined button | `product-quick-buy.liquid` | Outline style variant |

---

### 6. Final Stock Card
**Figma Node**: `209:11370`
**Shopify**: `snippets/product-card.liquid` (variant)

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| Vertical card, no border, rounded 13px | `.product-card` variant | Styling override |
| "ONLY 1 Left in Stock" red badge (top-right) | **OUTLIER**: Prestige badges don't show exact inventory count | Custom `snippets/inventory.liquid` integration |
| "Delivered in 48h" green pill (bottom of image, dark bg) | **OUTLIER**: Same as small card | Custom badge |
| "15% Off" teal pill (top-left) | `product-badges.liquid` | Direct match |
| White "Add to Cart" button (on dark card bg) | `product-quick-buy.liquid` | Color scheme variant |

---

### 7. Kitchen Card
**Figma Node**: `267:8795`
**Shopify**: `snippets/product-card.liquid` (variant)

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| Larger card (356px wide, 508px tall, 24px radius) | `.product-card` variant | CSS sizing override |
| Kitchen specs subtitle ("Modern · Matte white · 3m linear") | **OUTLIER**: No product spec line in Prestige cards | Custom metafield display |
| "Delivered in 48h" dark bg pill | **OUTLIER**: Custom badge | Same custom badge |
| "Request This Kitchen" CTA (not "Add to Cart") | **OUTLIER**: Different CTA text and behavior | Conditional button text via product type/tag |
| Arrow icon in button | **OUTLIER**: Prestige buy buttons don't include icons | Custom button template |

---

### 8. 48h Card
**Figma Node**: `280:12091`
**Shopify**: `snippets/product-card.liquid` (variant)

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| Same structure as Container card | `.product-card` | Close match |
| Wishlist heart (top-right, smaller 28px) | **OUTLIER**: Wishlist app | Same wishlist gap |
| "Ready in 48h" badge (dark bg pill) | **OUTLIER**: Custom badge | Same custom badge |
| "Only 4 left in stock" red text | **OUTLIER**: Inventory display | `snippets/inventory.liquid` — Prestige has this but not styled this way |
| "Delivered & assembled in 48h" green text with dot | **OUTLIER**: Delivery promise | Custom metafield/snippet |

---

### 9. Catalog Card
**Figma Node**: `493:8079`
**Shopify**: **No direct equivalent** — needs custom section

| Figma Element | Gap Analysis |
|---|---|
| PDF/digital catalog viewer card | **MAJOR OUTLIER**: Not a product — a downloadable catalog |
| "Updated Apr 2025 · Arabic & English" metadata | Custom content type |
| "View Catalog" + download button | Custom CTA linking to PDF/page |
| Large format (400×552px) | Custom card sizing |

**Recommendation**: Create `sections/catalog-cards.liquid` custom section with blocks for each catalog.

---

### 10. Catalog #2 Card
**Figma Node**: `501:8200`
**Shopify**: **No direct equivalent** — same custom section as Catalog

| Figma Element | Gap Analysis |
|---|---|
| Smaller catalog card (273×409px) | Size variant of Catalog card |
| "Hot" green badge | Custom badge |
| Promotional catalog (Ramadan 2025 Offers) | Seasonal content |

**Recommendation**: Same `sections/catalog-cards.liquid` with a compact block variant.

---

### 11. Separates Card
**Figma Node**: `570:8758`
**Shopify**: `snippets/product-card.liquid` (variant)

| Figma Element | Shopify Element | Gap Analysis |
|---|---|---|
| Nearly identical to Container card | `.product-card` | Close match |
| `object-contain` instead of `object-cover` on image | Image fit setting | **OUTLIER**: Different image scaling — product shown full, not cropped |
| Same wishlist, badge, price, button pattern | Same as Container | Same gaps |

---

## Screen-Level Mappings

| # | Figma Screen | Node ID | Template | Key Sections | Outlier Issues |
|---|---|---|---|---|---|
| 1 | Home Page | `372:9256` | `index.json` | slideshow, featured-collections, text-with-icons | Heavy customization of homepage layout |
| 2 | Product Listing Page | `372:10103` | `collection.json` | collection-banner, main-collection | Product card style overrides |
| 3 | Product Listing "Separates" | `570:7971` | `collection.json` (alt template) | main-collection with separates card | `object-contain` image variant |
| 4 | Sidebar Filter | `372:10133` | Within main-collection | facets, active-facets | Filter UI matches Prestige closely |
| 5 | Product Detail Page | `372:10426` | `product.json` | main-product | **See PDP outliers below** |
| 6 | PDP Option #2 | `574:9195` | `product.json` (alt) | main-product | Different gallery layout |
| 7 | Express Kitchens | `372:10746` | `collection.json` | collection-banner, main-collection | Kitchen cards need custom card variant |
| 8 | Customizable Kitchens | `372:10899` | Custom page template | **MAJOR OUTLIER**: configurator | Needs custom section for kitchen builder |
| 9 | Last Chance | `372:11427` | `collection.json` | collection-banner, main-collection | Countdown/urgency elements |
| 10 | Installments | `372:11671` | `page.json` | Custom content section | **OUTLIER**: Payment calculator/Valu integration |
| 11 | About | `372:11897` | `page.json` | main-page, image-with-text | Relatively standard |
| 12 | Catalog | `372:11978` | Custom page template | Custom catalog-cards section | **MAJOR OUTLIER**: needs new section |
| 13 | Contact & Showrooms | `460:7096` | `page.contact.json` | contact, map integration | **OUTLIER**: showroom locations/map |
| 14 | Checkout | `372:12438` | Shopify Checkout | Not theme-controlled | **NOT IMPLEMENTABLE** in theme |
| 15 | Order Confirmed | `372:12710` | Shopify Checkout | Not theme-controlled | **NOT IMPLEMENTABLE** in theme |
| 16 | Your Cart | `372:12890` | `cart.json` | main-cart, cart-drawer | Installment info in cart |
| 17 | Careers | `372:13083` | `page.json` | Custom careers section | **OUTLIER**: job listing functionality |
| 18 | My Account — Settings | `372:13360` | `customers/account.json` | main-customers-account | Standard |
| 19 | My Account — Orders | `372:13513` | `customers/order.json` | main-customers-order | Standard |
| 20 | My Account — Wishlist | `372:13716` | Custom | **MAJOR OUTLIER**: needs app | No native Shopify wishlist |
| 21 | My Account — Addresses | `372:13851` | `customers/addresses.json` | main-customers-addresses | Standard |

---

## Outlier Summary — Priority List

### CRITICAL (require new sections/apps/major work)

1. **Wishlist System** (Heart icon in header + product cards + My Account Wishlist page)
   - Affects: Header, all product cards, account page
   - Solution: Wishlist app (Wishlist Plus, Wishlist Hero) + app block integration
   - Figma nodes: `372:13716`, heart icons across all cards

2. **Installment/Valu Integration** ("or EGP 2,075 / mo. Valu" on every product)
   - Affects: ALL product cards, PDP, cart
   - Solution: Custom snippet calculating installment from price, Valu payment gateway
   - Figma nodes: Present in every card component

3. **Catalog Cards Section** (PDF catalog viewer/downloader)
   - Affects: Catalog page (`372:11978`)
   - Solution: New `sections/catalog-cards.liquid` custom section
   - Figma nodes: `493:8079`, `501:8200`

4. **Customizable Kitchens Configurator** (`372:10899`)
   - Affects: Kitchen category
   - Solution: Custom section or app for kitchen configuration
   - Requires deep investigation of this Figma screen

5. **Font System Mismatch**
   - Figma uses: Avenir (body), Nexa (footer headings), Inter (card text)
   - Prestige has: Nunito (body), Instrument Sans (headings)
   - Solution: Update `config/settings_data.json` font settings + add custom font files

### HIGH (require custom CSS/liquid modifications)

6. **"Delivered in 48h" Badge** — Custom green pill badge on product images
   - Solution: Product tag/metafield → custom badge in `product-badges.liquid`

7. **"Only X left in stock" Display** — Red inventory warning
   - Solution: Enhanced `snippets/inventory.liquid` with Figma styling

8. **Header CTA Buttons** ("Last Chance" pill + "Installments" orange button in nav)
   - Solution: Custom mega-menu link styling in `header.liquid`

9. **Kitchen Card "Request This Kitchen" CTA**
   - Solution: Conditional button text based on product type/tag

10. **Product Card Border Radius** — 14-24px vs Prestige's 0px default
    - Solution: Override `--button-border-radius` and card radius in CSS

### MEDIUM (styling overrides, achievable with theme settings + CSS)

11. **Color Scheme Alignment** — Create custom Prestige color schemes matching Figma palette
12. **Announcement Bar → Text-with-Icons** — Use existing section with icon blocks
13. **Footer Beige Color Scheme** — New color scheme in `settings_data.json`
14. **Product Card Wishlist Button Position** — CSS absolute positioning overlay
15. **Cart Badge Styling** — Minor CSS adjustments

### LOW (standard Shopify admin configuration)

16. **Navigation Menus** — Create in Shopify admin matching Figma structure
17. **Social Media URLs** — Configure in theme settings
18. **Logo Upload** — Upload SF logo in theme editor
19. **Footer Menu Structure** — 4 menus (Shop, Company, Help, My Account)

---

## Figma → Shopify Quick Reference

```
FIGMA COMPONENT          → SHOPIFY FILE                        STATUS
─────────────────────────────────────────────────────────────────────
Container (USP Bar)      → sections/text-with-icons.liquid     Remap needed
Header (left)            → sections/header.liquid              Partial + custom
Header (middle)          → sections/header.liquid              Partial + custom  
Footer (beige)           → sections/footer.liquid              Match + scheme
Footer (blue)            → sections/footer.liquid              Match + scheme
Container (product card) → snippets/product-card.liquid        Match + overrides
small card               → snippets/product-card-horizontal    Match + overrides
final stock              → snippets/product-card.liquid        Match + custom badge
Kitchen Card             → snippets/product-card.liquid        Partial + custom CTA
48 h card                → snippets/product-card.liquid        Match + custom badges
Catalog                  → NEW: sections/catalog-cards.liquid  Build from scratch
Catalog #2               → NEW: sections/catalog-cards.liquid  Build from scratch
Separates                → snippets/product-card.liquid        Match + image-fit
```
