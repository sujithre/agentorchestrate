# 💊 Contoso Pharma – Drug Catalog Website
## Project Instructions

---

## Overview

**Contoso Pharma** is a clean, clinical drug catalog website built with pure HTML, CSS, and vanilla JavaScript. It showcases a curated list of pharmaceutical products with their key values — composition, dosage, price, manufacturer, and therapeutic category. No frameworks or build tools required — just open `pharma-catalog.html` in a browser.

---

## Project Structure

```
contoso-pharma/
├── pharma-catalog.html        # Main website (all-in-one file)
├── INSTRUCTIONS.md            # This file
└── .github/
    └── copilot-instructions.md  # GitHub Copilot custom instructions
```

---

## Getting Started

### 1. Prerequisites
- A modern browser (Chrome, Firefox, Safari, Edge)
- A code editor (VS Code recommended)
- Internet connection (for Google Fonts and product images)

### 2. Run Locally
Simply open the HTML file in your browser:
```bash
# Option A: Double-click the file in your file explorer

# Option B: Using a local server (recommended for development)
npx serve .
# or
python -m http.server 8000
```
Then visit `http://localhost:8000/pharma-catalog.html`

### 3. Live Preview in VS Code
Install the **Live Server** extension and click **"Go Live"** in the bottom status bar.

---

## Features

| Feature | Description |
|---|---|
| 🔍 Search Bar | Search drugs by brand, generic name, or therapeutic category |
| 💊 Drug Catalog Grid | Card grid showing drug name, image, strength, and price |
| 🧪 Categories | Filter by Antibiotics, Cardiac, Diabetes, Pain Relief, Vitamins |
| 📋 Drug Details | Composition, dosage, manufacturer, batch info, expiry |
| ⚠️ Safety Info | Warnings, side effects, prescription-required (Rx) badges |
| ⭐ Patient Reviews | 3 verified patient feedback cards |
| 📧 Newsletter | Health tips & new product launches signup |
| 📱 Responsive | Mobile-friendly layout with media queries |
| 🎞 Scroll Reveal | Cards animate in as the user scrolls |

---

## Customisation Guide

### 🎨 Changing Colors
All colors are defined as CSS variables at the top of the `<style>` block. The palette is intentionally clinical and trustworthy:
```css
:root {
  --bg: #f4f8fb;
  --ink: #0f1f2e;
  --medical-blue: #2a73c9;   /* Primary accent — change this first */
  --mint: #4cc2a3;            /* Healthy / in-stock indicator */
  --amber: #e8a93a;           /* Warning / prescription badge */
  --crimson: #d24b4b;         /* Critical / out-of-stock */
  --surface: #ffffff;
  --muted: #6b7a87;
}
```

### 🖼 Changing Images
Drug images are loaded from [Unsplash](https://unsplash.com) or Contoso's own CDN. To use your own:
1. Replace the `src` attribute of any `<img>` tag
2. Use white-background product shots at least **600×600px**
3. Host them in an `/images/drugs/` folder alongside the HTML file

```html
<!-- Before -->
<img src="https://images.unsplash.com/photo-xxx?w=600" alt="Paracetamol 500mg"/>

<!-- After (local image) -->
<img src="./images/drugs/paracetamol-500.jpg" alt="Paracetamol 500mg"/>
```

### 💊 Adding/Editing Drugs
Find the `.drug-grid` section and duplicate a `.drug-card`:
```html
<div class="drug-card" data-category="pain-relief">
  <div class="drug-img-wrap">
    <img src="YOUR_IMAGE_URL" alt="Drug Name"/>
    <span class="drug-badge">Rx</span>
  </div>
  <div class="drug-body">
    <p class="drug-generic">Generic Name</p>
    <h3>Brand Name 500 mg</h3>
    <div class="drug-meta">
      <span>🧪 <strong>Composition</strong></span>
      <span>💊 <strong>Tablet · 10s</strong></span>
    </div>
    <div class="drug-footer">
      <div class="drug-price">₹XX.XX <sub>/ strip</sub></div>
      <button class="add-btn">Add to Cart</button>
    </div>
  </div>
</div>
```

### 🧪 Adding a New Category
1. Add a filter chip in the `.category-filters` section:
   ```html
   <button class="cat-chip" data-cat="oncology">Oncology</button>
   ```
2. Tag drug cards with `data-category="oncology"`
3. The existing JS filter will pick it up automatically.

### 💱 Changing Currency
Search for `₹` (the Indian Rupee symbol) in the file and replace with your preferred currency symbol (e.g., `$`, `€`, `£`).

---

## Sample Drug Data Schema

Each drug card represents the following data shape — useful when wiring up a backend later:
```json
{
  "id": "DRG-00123",
  "brand": "Crocin Advance",
  "generic": "Paracetamol",
  "strength": "500 mg",
  "form": "Tablet",
  "pack": "10 tablets / strip",
  "category": "pain-relief",
  "price": 35.50,
  "currency": "INR",
  "manufacturer": "GSK",
  "prescription": false,
  "stock": "in-stock",
  "expiry": "2027-06"
}
```

---

## Extending the Project

### Add a Backend (for real orders & inventory)
Connect a backend using:
- **Node.js + Express** — for a JavaScript stack
- **Django / Flask** — for Python
- **Supabase / Firebase** — for serverless / no-code backends

### Add a Payment Gateway
Integrate one of these after the "Add to Cart" flow:
- [Razorpay](https://razorpay.com) — best for India
- [Stripe](https://stripe.com) — international
- [PayU](https://payu.in) — popular in South Asia

### Make it Multi-page
Split sections into separate HTML files:
```
index.html          → Hero + Search + Featured drugs
catalog.html        → Full drug catalog with filters
drug.html           → Single drug detail page
cart.html           → Cart & prescription upload
checkout.html       → Address + payment
confirmation.html   → Order confirmation
```

### Add Prescription Upload
For Rx-required drugs, accept a prescription image or PDF before checkout:
```html
<input type="file" accept="image/*,.pdf" id="rx-upload" />
```
Validate with vanilla JS using the `File` API (size, MIME type) before enabling the checkout button.

---

## Compliance Reminders

> ⚠️ This is a demo project. A real pharma e-commerce site must comply with regional regulations.

- **India**: Drugs and Cosmetics Act, 1940 — Schedule H / H1 / X drugs require a valid prescription
- **US**: FDA labeling requirements + HIPAA for any patient data
- **EU**: EMA guidelines + GDPR for personal data
- Always show a clear **disclaimer**: *"Information is for educational purposes only — consult a registered medical practitioner before use."*

---

## Browser Support

| Browser | Support |
|---|---|
| Chrome 90+ | ✅ Full |
| Firefox 88+ | ✅ Full |
| Safari 14+ | ✅ Full |
| Edge 90+ | ✅ Full |
| IE 11 | ❌ Not supported |

---

## Fonts Used
- **Playfair Display** — section headings (Google Fonts)
- **DM Sans** — body text and UI (Google Fonts)

Both loaded via CDN. To use locally, download from [fonts.google.com](https://fonts.google.com).

---

## Performance Tips
- Compress drug images before going live ([Squoosh](https://squoosh.app) is free)
- Add `loading="lazy"` to drug cards below the fold
- Minify the CSS/JS for production using [cssnano](https://cssnano.co) or [terser](https://terser.org)

---

## Deployment

### Netlify (Recommended — Free)
1. Go to [netlify.com](https://netlify.com) → New Site
2. Drag & drop your project folder
3. Done! You'll get a live URL instantly.

### GitHub Pages (Free)
1. Push your files to a GitHub repository
2. Go to Settings → Pages → Source: `main` branch
3. Your site will be live at `https://yourusername.github.io/repo-name`

### Vercel
```bash
npm i -g vercel
vercel
```

---

## License
This project is open source. Feel free to use, modify, and distribute it.

---

*Made with 💊 by Contoso Pharma*