# GitHub Copilot Custom Instructions
## Contoso – Travel Booking Website

---

## Project Context

This is **Contoso**, a travel booking website built with:
- **HTML5** (semantic markup)
- **CSS3** (custom properties, Grid, Flexbox, keyframe animations)
- **Vanilla JavaScript** (ES6+, IntersectionObserver, DOM events)
- **No frameworks** — no React, no Vue, no build tools
- **No external JS libraries** (unless adding a date picker like flatpickr)

The entire site lives in one file: `travel-booking.html`.

---

## Code Style Preferences

### HTML
- Use **semantic elements**: `<section>`, `<nav>`, `<footer>`, `<article>`, `<main>`
- Always include `alt` text on images
- Use `class` names that follow a **BEM-inspired flat style**: `.dest-card`, `.pkg-body`, `.search-box`
- Prefer double quotes for attributes: `class="hero"` not `class='hero'`
- Indent with **2 spaces**

### CSS
- Use **CSS custom properties** (`--variable-name`) for all colors, radii, and spacing constants
- Define variables in `:root {}`
- Prefer `clamp()` for responsive font sizes: `font-size: clamp(1rem, 3vw, 2rem)`
- Use `transition` for hover effects — keep durations between `0.15s` and `0.5s`
- Use `@keyframes` for entrance animations — prefer `fadeUp` and `fadeDown` patterns
- Avoid `!important` unless absolutely necessary
- Use `border-radius: 100px` for pill shapes, and specific values (e.g. `18px`) for cards
- Responsive breakpoints: use `@media (max-width: 900px)` for tablet/mobile

### JavaScript
- Use `const` and `let` — never `var`
- Prefer `document.querySelectorAll` and `forEach` loops
- Use `IntersectionObserver` for scroll-reveal animations
- Attach events via `addEventListener`, never inline HTML `onclick=""`
- Keep JS at the bottom of the `<body>`, inside a `<script>` tag
- No jQuery — use native DOM APIs

---

## Design System

### Color Palette (CSS Variables)
```css
--sand: #f5f0e8;
--ink: #1a1410;
--terracotta: #c9603a;   /* Primary accent */
--gold: #d4a843;          /* Badges / highlights */
--sage: #7a9e7e;          /* Secondary accent */
--cream: #faf7f2;         /* Page background */
--muted: #8a7f72;         /* Subdued text */
```

### Typography
- **Display font**: `'Playfair Display', serif` — headings, logo
- **Body font**: `'DM Sans', sans-serif` — body text, UI elements
- Section titles: `font-family: 'Playfair Display', serif; font-weight: 700`
- Body text: `font-weight: 300` or `400`, `line-height: 1.65–1.7`
- Labels: `font-size: 0.72rem; letter-spacing: 0.18em; text-transform: uppercase`

### Spacing Rhythm
- Section padding: `6rem 4rem` (desktop), `4rem 1.5rem` (mobile)
- Card padding: `1.5rem` to `2rem`
- Grid gaps: `1.2rem` to `1.5rem`

### Component Patterns
- **Cards**: white background, `border-radius: 18px`, hover: `translateY(-6px)` + box-shadow
- **Buttons (primary)**: `background: var(--terracotta)`, `border-radius: 100px`, white text
- **Buttons (dark)**: `background: var(--ink)`, hover to `var(--terracotta)`
- **Section labels**: uppercase, small, terracotta color, spaced tracking
- **Overlays on images**: `linear-gradient(to top, rgba(26,20,16,0.7), transparent 55%)`

---

## Copilot Behaviour Guidelines

### When suggesting new components:
1. Match the existing **visual language**: earthy tones, Playfair headings, DM Sans body
2. Reuse existing CSS variables — do **not** introduce hardcoded hex colours
3. Include hover states and transitions on interactive elements
4. Keep markup semantic and accessible (use `aria-label` where needed)

### When writing CSS:
- Group related properties: positioning → box model → typography → visual → animation
- Add a comment above major component blocks: `/* ── CARD ── */`
- Suggest `clamp()` for any font-size on heading elements

### When writing JavaScript:
- Suggest `IntersectionObserver` for any scroll-based reveal
- Suggest event delegation when handling list/grid item events
- Avoid adding third-party libraries unless the task genuinely requires one

### When adding new sections:
Follow this HTML pattern:
```html
<section class="[section-name]" id="[section-name]">
  <div class="section-header">
    <div>
      <p class="section-label">Short Label</p>
      <h2 class="section-title">Section Heading</h2>
    </div>
    <a href="#" class="view-all">View all →</a>
  </div>
  <!-- Section content here -->
</section>
```

### When adding images:
- Use `<img>` with `object-fit: cover` inside a fixed-height container
- Always add descriptive `alt` text
- Suggest adding `loading="lazy"` for below-the-fold images

---

## Common Tasks & Suggestions

| Task | Copilot Should Suggest |
|---|---|
| New destination card | Copy `.dest-card` pattern with overlay and `.dest-info` |
| New package | Copy `.pkg-card` with `.pkg-img-wrap`, `.pkg-body`, `.pkg-footer` |
| New color variable | Add to `:root {}` at the top of `<style>` |
| Date picker | Use `flatpickr` CDN (lightweight, no build step) |
| Modal/overlay | Use `position: fixed; inset: 0` with `backdrop-filter: blur()` |
| Form validation | Vanilla JS with `input.validity` API — no jQuery |
| Scroll animation | `IntersectionObserver` with `opacity` + `transform` transition |
| Mobile nav | Toggle a `.open` class on `<nav>` with CSS transitions |
| Booking form | Use `<form>` with `novalidate` + custom JS validation |

---

## What to Avoid

- ❌ Do **not** suggest React, Vue, Angular, or any JS framework
- ❌ Do **not** suggest npm packages or build tools (Webpack, Vite, etc.)
- ❌ Do **not** use `var` for variables
- ❌ Do **not** hardcode colors — always use CSS custom properties
- ❌ Do **not** use inline styles in HTML (`style="color: red"`)
- ❌ Do **not** use Bootstrap or Tailwind — all styles are hand-written
- ❌ Do **not** suggest `!important` unless there is no other option
- ❌ Do **not** add unnecessary dependencies for simple UI tasks

---

## Accessibility Reminders

- All `<img>` tags must have meaningful `alt` attributes
- Interactive elements must be keyboard-focusable
- Color contrast: text on backgrounds must meet WCAG AA (4.5:1 ratio)
- Use `aria-label` on icon-only buttons
- Form inputs must have associated `<label>` elements

---

## File Structure (Single-file Architecture)

Since the entire project is in one HTML file, structure it in this order:
1. `<!DOCTYPE html>` + `<head>` (meta, fonts, `<style>`)
2. `<body>` → `<nav>`
3. `<section class="hero">`
4. Feature sections (destinations, packages, why-us, etc.)
5. `<footer>`
6. `<script>` (at the very bottom of `<body>`)

---

*These instructions help GitHub Copilot generate code that stays consistent with the Contoso project's design system, code style, and single-file architecture.*