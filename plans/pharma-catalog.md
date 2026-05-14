# Plan: Contoso Pharma Drug Catalog Website

## Summary

Build a single-file (`pharma-catalog.html`) pharmaceutical drug catalog website with a clinical, trustworthy design. The site includes a hero with search, category chip filters, a drug card grid (8 drugs), drug detail/safety section, patient reviews, newsletter signup, and a footer. All HTML, CSS, and JavaScript live in one file. The design system uses CSS custom properties (medical-blue, mint, amber, crimson palette), Playfair Display + DM Sans fonts, and follows the existing Contoso project conventions (BEM-inspired classes, semantic HTML, IntersectionObserver scroll reveals, no frameworks). Indian Rupee pricing with Rx/OTC badges.

---

## File

**All work targets a single file:** `c:\Projects\AGentsDemo2\pharma-catalog.html`

Because this is a single-file architecture, steps are broken down by **section** within the file. Each step indicates which section it writes (CSS, HTML, or JS) so the orchestrator can determine parallelism and merge order.

---

## Implementation Steps

### Step 1 — HTML Document Shell & Head
**Section:** HTML structure (document skeleton)
**Dependencies:** None
**Assigns:** Top of file

Create the `<!DOCTYPE html>`, `<html lang="en">`, `<head>` block:

1. `<meta charset="UTF-8">`, `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
2. `<title>Contoso Pharma — Drug Catalog</title>`
3. Google Fonts link for **Playfair Display** (weights 400, 700) and **DM Sans** (weights 300, 400, 500, 700)
4. Open `<style>` tag (CSS content from Step 2 goes here)
5. Close `</head>`, open `<body>`

---

### Step 2 — CSS: Custom Properties & Base Styles
**Section:** CSS (inside `<style>` in `<head>`)
**Dependencies:** Step 1 (needs `<style>` tag to exist)
**Assigns:** CSS block — `:root`, reset, typography, layout primitives

Write these CSS sub-sections in order:

1. **`:root` variables:**
   ```
   --bg: #f4f8fb
   --ink: #0f1f2e
   --medical-blue: #2a73c9
   --mint: #4cc2a3
   --amber: #e8a93a
   --crimson: #d24b4b
   --surface: #ffffff
   --muted: #6b7a87
   ```
2. **CSS reset:** `*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }`
3. **Body base:** `font-family: 'DM Sans', sans-serif; background: var(--bg); color: var(--ink); line-height: 1.65;`
4. **Heading defaults:** `font-family: 'Playfair Display', serif; font-weight: 700;` for `h1–h6`
5. **Section scaffolding:** `.section-header` flex with space-between, `.section-label` (uppercase, small, medical-blue, letter-spacing: 0.18em), `.section-title` with `clamp(1.6rem, 3vw, 2.4rem)`
6. **`.view-all`** link style (medical-blue, no underline, hover underline)
7. **Container utility:** max-width 1200px, margin auto, padding
8. **`img` defaults:** `max-width: 100%; display: block;`

---

### Step 3 — CSS: Component Styles
**Section:** CSS (inside `<style>`, after base styles)
**Dependencies:** Step 2 (needs variables and base to be defined)
**Assigns:** CSS block — component-specific styles

Write these component CSS blocks:

1. **Nav bar** (`.navbar`): fixed top, white bg, box-shadow, flex layout, logo (Playfair Display), nav links, cart icon with counter badge
2. **Hero** (`.hero`): tall section (~70vh min), gradient overlay on a bg color or subtle pattern, centered text, search bar
3. **Search bar** (`.search-box`): white bg, border-radius 100px (pill), flex with input + button, box-shadow, icon prefix
4. **Category chips** (`.category-filters`): flex wrap, gap, `.cat-chip` buttons with border-radius 100px, border 1px solid var(--medical-blue), transparent bg, hover/active fills with medical-blue + white text. Active state class: `.cat-chip.active`
5. **Drug card grid** (`.drug-grid`): CSS Grid with `repeat(auto-fill, minmax(280px, 1fr))`, gap 1.5rem
6. **Drug card** (`.drug-card`): white bg, border-radius 18px, overflow hidden, transition translateY(-6px) + box-shadow on hover, `.drug-img-wrap` with fixed height (200px) + `object-fit: cover` on img
7. **Drug badge** (`.drug-badge`): absolute positioned top-right of image, small pill, `--amber` bg for Rx, `--mint` for OTC
8. **Drug body** (`.drug-body`): padding 1.5rem, `.drug-generic` (muted, small, uppercase), `h3` (brand name), `.drug-meta` (flex, small, muted icons), `.drug-footer` (flex, space-between, price + add button)
9. **Drug price** (`.drug-price`): medical-blue, bold, `sub` element smaller + muted
10. **Add button** (`.add-btn`): medical-blue bg, white text, border-radius 100px, hover darken
11. **Safety section** (`.safety-info`): grid or flex, cards with icon, title, description. Use crimson accent for warnings, amber for caution, mint for safe
12. **Review cards** (`.review-card`): white bg, border-radius 18px, avatar placeholder, star rating (Unicode ★), reviewer name, quote text
13. **Newsletter** (`.newsletter`): medical-blue bg, white text, email input + submit button in a flex row, border-radius pill
14. **Footer** (`.site-footer`): dark bg (--ink), white/muted text, grid columns for links, disclaimer text
15. **Scroll reveal** (`.reveal`): initial `opacity: 0; transform: translateY(30px)`, transition 0.6s. `.reveal.visible`: `opacity: 1; transform: translateY(0)`

---

### Step 4 — CSS: Responsive Breakpoints
**Section:** CSS (inside `<style>`, after component styles)
**Dependencies:** Step 3 (needs component classes to exist)
**Assigns:** CSS block — media queries

1. **`@media (max-width: 900px)`:**
   - Nav collapses: hamburger icon toggles `.open` class, vertical nav links
   - Hero section: reduce padding, font sizes
   - Drug grid: `repeat(auto-fill, minmax(240px, 1fr))`
   - Section padding: `4rem 1.5rem`
   - Footer grid: single column stack

2. **`@media (max-width: 600px)`:**
   - Drug grid: single column
   - Category chips: horizontal scroll with `overflow-x: auto; flex-wrap: nowrap`
   - Search bar: full width, stacked button below if needed
   - Review cards: single column
   - Newsletter input + button: stack vertically

---

### Step 5 — HTML: Navigation Bar
**Section:** HTML (first child of `<body>`)
**Dependencies:** Step 1 (needs `<body>` tag)
**Assigns:** `<nav class="navbar">`

1. Logo: `<a class="nav-logo" href="#">Contoso<span>Pharma</span></a>` — "Contoso" in Playfair Display, "Pharma" accent in medical-blue
2. Nav links: `<ul class="nav-links">` with items: Home, Catalog, Categories, Reviews, Contact
3. Cart icon: `<div class="nav-cart">` with SVG/emoji cart icon + `<span class="cart-count">0</span>` badge
4. Hamburger button: `<button class="nav-toggle" aria-label="Toggle menu">☰</button>` (visible only on mobile)

---

### Step 6 — HTML: Hero Section
**Section:** HTML (after nav)
**Dependencies:** Step 5 (sequential in DOM order)
**Assigns:** `<section class="hero" id="hero">`

1. `<h1>` — "Your Trusted Online Pharmacy" with `clamp()` font size
2. `<p class="hero-subtitle">` — "Browse 10,000+ medicines — delivered to your doorstep with care"
3. Search bar:
   ```html
   <div class="search-box">
     <span class="search-icon">🔍</span>
     <input type="text" id="drug-search" placeholder="Search by drug name, generic, or category..." aria-label="Search drugs"/>
     <button class="search-btn">Search</button>
   </div>
   ```

---

### Step 7 — HTML: Category Filter Chips
**Section:** HTML (after hero)
**Dependencies:** Step 6
**Assigns:** `<section class="categories" id="categories">`

1. Section header with label "Browse By" and title "Therapeutic Categories"
2. Filter chip bar:
   ```html
   <div class="category-filters">
     <button class="cat-chip active" data-cat="all">All</button>
     <button class="cat-chip" data-cat="antibiotics">💉 Antibiotics</button>
     <button class="cat-chip" data-cat="cardiac">❤️ Cardiac</button>
     <button class="cat-chip" data-cat="diabetes">🩸 Diabetes</button>
     <button class="cat-chip" data-cat="pain-relief">💊 Pain Relief</button>
     <button class="cat-chip" data-cat="vitamins">🌿 Vitamins</button>
   </div>
   ```

---

### Step 8 — HTML: Drug Catalog Grid (8 Drug Cards)
**Section:** HTML (after categories)
**Dependencies:** Step 7
**Assigns:** `<section class="catalog" id="catalog">` containing `.drug-grid`

Create 8 drug cards using the drug card pattern from the requirements. Each card must include:
- `data-category` attribute matching its therapeutic category (lowercase, hyphenated)
- Drug image (use Unsplash pharmaceutical/medicine images with `?w=600&h=400&fit=crop`)
- Rx badge (for prescription drugs) or OTC badge styling
- Generic name, brand name + strength, composition, form/pack
- Price in ₹ with `/strip` sub-label
- "Add to Cart" button
- `loading="lazy"` on all images
- `alt` text with drug name + strength
- Class `reveal` for scroll animation

**Drug data to encode:**

| # | Brand | Generic | Strength | Category | Price | Manufacturer | Rx/OTC |
|---|---|---|---|---|---|---|---|
| 1 | Crocin Advance | Paracetamol | 500mg | pain-relief | ₹35.50 | GSK | OTC |
| 2 | Azithral 500 | Azithromycin | 500mg | antibiotics | ₹98.00 | Alembic | Rx |
| 3 | Metformin SR | Metformin | 500mg | diabetes | ₹45.00 | USV | Rx |
| 4 | Ecosprin 75 | Aspirin | 75mg | cardiac | ₹22.50 | USV | Rx |
| 5 | Shelcal 500 | Calcium + Vitamin D3 | — | vitamins | ₹155.00 | Torrent | OTC |
| 6 | Dolo 650 | Paracetamol | 650mg | pain-relief | ₹30.00 | Micro Labs | OTC |
| 7 | Amoxicillin 250 | Amoxicillin | 250mg | antibiotics | ₹65.00 | Cipla | Rx |
| 8 | Telma 40 | Telmisartan | 40mg | cardiac | ₹120.00 | Glenmark | Rx |

---

### Step 9 — HTML: Safety Information Section
**Section:** HTML (after catalog)
**Dependencies:** Step 8
**Assigns:** `<section class="safety-info" id="safety-info">`

1. Section header: label "Important", title "Drug Safety Information"
2. 3–4 safety info cards in a grid:
   - **⚠️ Prescription Required** — "Drugs marked Rx require a valid prescription from a licensed practitioner. Upload your prescription at checkout."
   - **🚫 Side Effects** — "All medications may cause side effects. Consult your doctor if you experience dizziness, nausea, or allergic reactions."
   - **📦 Storage & Expiry** — "Store medicines in a cool, dry place. Never use medication past its expiry date printed on the packaging."
   - **🔒 Verified Suppliers** — "All products sourced from licensed manufacturers and verified through Contoso's supply chain audit."
3. Each card gets class `reveal` for scroll animation

---

### Step 10 — HTML: Patient Reviews Section
**Section:** HTML (after safety info)
**Dependencies:** Step 9
**Assigns:** `<section class="reviews" id="reviews">`

1. Section header: label "Testimonials", title "What Patients Say"
2. 3 review cards in a flex/grid row:
   - **Reviewer 1:** Ananya S. — ★★★★★ — "Fast delivery and genuine medicines. The Rx upload process was seamless. Highly recommend Contoso Pharma!"
   - **Reviewer 2:** Rajesh M. — ★★★★☆ — "Good prices on diabetes medications. Packaging was excellent. Wish they had more ayurvedic options."
   - **Reviewer 3:** Priya K. — ★★★★★ — "My go-to pharmacy for monthly refills. The reminders feature is a lifesaver. Customer support is top-notch."
3. Each card: avatar circle (initial letter or placeholder), name, star rating, verified badge, review text
4. Each card gets class `reveal`

---

### Step 11 — HTML: Newsletter Signup Section
**Section:** HTML (after reviews)
**Dependencies:** Step 10
**Assigns:** `<section class="newsletter" id="newsletter">`

1. Medical-blue background section, white text
2. Heading: "Stay Healthy, Stay Informed"
3. Subtitle: "Get health tips, new product alerts, and exclusive offers delivered to your inbox."
4. Form with email input (pill shape) + subscribe button
5. Small disclaimer text: "We respect your privacy. Unsubscribe anytime."
6. `<form>` with `novalidate` attribute — JS handles validation

---

### Step 12 — HTML: Footer
**Section:** HTML (after newsletter, before `</body>`)
**Dependencies:** Step 11
**Assigns:** `<footer class="site-footer">`

1. Footer grid (3–4 columns on desktop):
   - **Column 1:** Contoso Pharma logo + brief tagline + social icons
   - **Column 2:** Quick Links — Home, Catalog, Upload Rx, Track Order
   - **Column 3:** Categories — Antibiotics, Cardiac, Diabetes, Pain Relief, Vitamins
   - **Column 4:** Contact — Email, phone, address
2. Bottom bar: `<div class="footer-bottom">`
   - Disclaimer: *"This website is for informational purposes only. Consult a registered medical practitioner before taking any medication."*
   - Copyright: `© 2026 Contoso Pharma. All rights reserved.`

---

### Step 13 — JavaScript: Search Filter
**Section:** JavaScript (inside `<script>` at bottom of `<body>`)
**Dependencies:** Steps 6, 8 (needs search input and drug cards in DOM)
**Assigns:** JS block — search functionality

1. Grab `#drug-search` input and all `.drug-card` elements
2. Listen for `input` event (real-time filtering as user types)
3. For each card, check if the search term appears in:
   - `h3` text (brand name)
   - `.drug-generic` text (generic name)
   - `data-category` attribute
4. Show/hide cards by toggling `display: none` or a `.hidden` class
5. If no results match, show a "No drugs found" placeholder message

---

### Step 14 — JavaScript: Category Filter
**Section:** JavaScript (inside `<script>`, after search)
**Dependencies:** Steps 7, 8 (needs chips and drug cards in DOM)
**Assigns:** JS block — category chip filtering

1. Grab all `.cat-chip` buttons and all `.drug-card` elements
2. On chip click:
   - Remove `.active` from all chips, add `.active` to clicked chip
   - Read `data-cat` attribute from clicked chip
   - If `all`, show all cards
   - Otherwise, show only cards where `data-category` matches
   - Clear the search input when a category is selected
3. Use `forEach` loop — no jQuery

---

### Step 15 — JavaScript: Scroll Reveal (IntersectionObserver)
**Section:** JavaScript (inside `<script>`, after filters)
**Dependencies:** Steps 8–10 (needs `.reveal` elements in DOM)
**Assigns:** JS block — scroll animation

1. Select all `.reveal` elements
2. Create `IntersectionObserver` with options: `{ threshold: 0.15, rootMargin: '0px 0px -50px 0px' }`
3. Callback: when `entry.isIntersecting`, add `.visible` class and `unobserve` the element
4. Observe each `.reveal` element

---

### Step 16 — JavaScript: Add to Cart Interaction
**Section:** JavaScript (inside `<script>`, after scroll reveal)
**Dependencies:** Steps 5, 8 (needs nav cart badge and drug cards)
**Assigns:** JS block — cart counter

1. Use **event delegation** on `.drug-grid` for `.add-btn` clicks
2. On click:
   - Increment a `cartCount` variable
   - Update `.cart-count` badge text
   - Brief visual feedback: change button text to "✓ Added" for 1.5 seconds, then revert
   - Optionally add a subtle scale animation on the cart icon

---

### Step 17 — JavaScript: Mobile Nav Toggle
**Section:** JavaScript (inside `<script>`, after cart)
**Dependencies:** Step 5 (needs nav toggle button)
**Assigns:** JS block — mobile menu

1. Grab `.nav-toggle` button and `.nav-links` element
2. On click, toggle `.open` class on `.nav-links`
3. Toggle hamburger icon between ☰ and ✕
4. Close menu when a nav link is clicked (for single-page scroll)

---

### Step 18 — JavaScript: Newsletter Form Validation
**Section:** JavaScript (inside `<script>`, after nav toggle)
**Dependencies:** Step 11 (needs newsletter form)
**Assigns:** JS block — email validation

1. Grab the newsletter `<form>` and email `<input>`
2. On `submit`, prevent default
3. Validate email using `input.validity.typeMismatch` or a simple regex
4. If valid: show a success message (e.g., swap form content to "Thanks for subscribing! 🎉")
5. If invalid: show inline error styled with `--crimson`

---

## Dependency Graph & Parallelization

```
Step 1 (Shell)
  └──> Step 2 (CSS Base)
         └──> Step 3 (CSS Components)
                └──> Step 4 (CSS Responsive)
  └──> Step 5 (Nav HTML)
         └──> Step 6 (Hero HTML)
                └──> Step 7 (Categories HTML)
                       └──> Step 8 (Drug Grid HTML)
                              ├──> Step 9 (Safety HTML)
                              │      └──> Step 10 (Reviews HTML)
                              │             └──> Step 11 (Newsletter HTML)
                              │                    └──> Step 12 (Footer HTML)
                              ├──> Step 13 (JS: Search)
                              ├──> Step 14 (JS: Category Filter)
                              ├──> Step 15 (JS: Scroll Reveal)
                              └──> Step 16 (JS: Cart)
         └──> Step 17 (JS: Mobile Nav)
  └──> Step 18 (JS: Newsletter Validation) [depends on Step 11]
```

### Recommended Execution Phases (for single-file build)

Since everything lives in one file, **true parallelization is limited**. However, these phases represent logical groupings that could be written by separate agents and then merged:

| Phase | Steps | Agent | Description |
|---|---|---|---|
| **Phase 1** | 1 | Coder | Create document shell with `<head>`, font links, empty `<style>` and `<script>` |
| **Phase 2** | 2, 3, 4 | Designer | Write all CSS (variables → components → responsive) inside `<style>` |
| **Phase 3** | 5, 6, 7, 8, 9, 10, 11, 12 | Coder | Write all HTML sections in DOM order (nav through footer) |
| **Phase 4** | 13, 14, 15, 16, 17, 18 | Coder | Write all JavaScript inside `<script>` |

> **Note:** Phases 2 and 3 could potentially run in parallel if each agent writes to a separate temporary file and the results are merged in order. Phase 4 depends on Phase 3 (JS references DOM elements).

---

## Edge Cases to Handle

1. **Search with no results** — Display a "No medicines found for '[query]'. Try a different search term." message inside the grid area
2. **Empty category** — If a category filter yields zero cards, show a similar empty-state message
3. **Search + category interaction** — Decide behavior: searching should reset category to "All", OR search within the active category. Recommended: search resets category to "All" for simplicity
4. **Cart count overflow** — If count exceeds 99, display "99+"
5. **Long drug names** — Ensure card text truncates with `text-overflow: ellipsis` or wraps gracefully
6. **Image load failure** — Add a CSS fallback background (light gray with a pill icon) on `.drug-img-wrap` so broken images still look intentional
7. **Keyboard accessibility** — Category chips and add-to-cart buttons must be keyboard-focusable with visible focus rings
8. **Mobile nav overlay** — When mobile menu is open, prevent body scroll (`overflow: hidden` on body)
9. **Newsletter double-submit** — Disable the submit button after successful submission
10. **Scroll reveal on fast scroll** — IntersectionObserver handles this natively, but verify elements above the fold start visible (don't apply `.reveal` to hero/nav)

---

## Open Questions

1. **Drug images:** Should we use generic Unsplash pharmaceutical images, or placeholder colored boxes? Unsplash URLs may break over time. *Recommendation: Use Unsplash with `?w=600&h=400&fit=crop` queries for demo purposes, note in comments that production should use local images.*
2. **Add to Cart persistence:** Should cart state survive page refresh (localStorage)? *Recommendation: Skip for v1 — keep it in-memory only.*
3. **Drug detail modal:** The requirements mention "Drug Details" as a feature. Should clicking a card open a modal/overlay with full details (composition, batch, expiry, manufacturer), or is the card itself sufficient? *Recommendation: Add a simple modal on card click for v2 scope; for v1, show key details inline on the card.*
4. **Accessibility audit level:** Should we aim for WCAG AA or AAA? *Recommendation: AA compliance (4.5:1 contrast, focus indicators, aria-labels).*

---

## Verification Checklist (Post-Implementation)

- [ ] File opens correctly in browser with no console errors
- [ ] All 8 drug cards render with correct data
- [ ] Search filters cards in real-time by brand, generic, and category
- [ ] Category chips filter correctly; "All" resets the view
- [ ] Rx badges show on prescription drugs; OTC drugs have no badge or a mint "OTC" badge
- [ ] Scroll reveal animates cards on scroll
- [ ] Add to Cart increments counter and shows feedback
- [ ] Mobile nav toggle works at ≤900px
- [ ] Newsletter form validates email and shows feedback
- [ ] All images have `alt` text and `loading="lazy"`
- [ ] No hardcoded hex colors (all use CSS variables)
- [ ] No `var` keyword in JavaScript
- [ ] Semantic HTML elements used throughout
- [ ] Footer disclaimer is visible
- [ ] Page is responsive at 600px, 900px, and 1200px viewports
