# Copilot instructions — Hidsa Collection

## Quick summary
- This is a **single-page static website** (HTML + inline CSS) at `index.html`. There is no build system, framework, or server-side code.
- Content and styles live in `index.html`; images are in `img/` (and `img/images/` in this repo). Product cards are plain HTML blocks inside the `.produk-grid` container.

---

## How to run / preview locally ✅
- Recommended: Use VS Code **Live Server** extension (right-click `index.html` → "Open with Live Server") for fast live reloads.
- Alternatively: from repo root run a simple HTTP server:
  - Python: `python -m http.server 8000` then open `http://localhost:8000`
  - Node: `npx serve .`
- Manually opening `index.html` in the browser is fine for basic checks, but some assets and font loading behave better over HTTP.

---

## Project structure & important files
- `index.html` — single source of truth: HTML markup, CSS (inline), and site content.
- `img/` and `img/images/` — media assets (logo, banner, product photos)

---

## Key patterns & conventions AI agents should follow 🔧
- Modifying content: edit `index.html` directly. Product items are repeated `.card` blocks inside `.produk-grid` (image → `.info` with `<h3>`, `<p>` price, `<a>` detail).
- Responsive behavior: grid columns are controlled by `.produk-grid` and media queries: 3 columns (desktop), 2 columns @ <900px, 1 column @ <600px.
- Styles are inline in `index.html`. Prefer making small CSS fixes in place; for larger refactors consider extracting to `styles.css` and updating the HTML accordingly, but document the change in PR.

---

## Common edits — examples
- Add a product: copy an existing `.card` block and update the `img` src, name, and price.
- Fix an image path mismatch: product images currently reference `images/produk1.jpg` etc. In this repository images live in `img/images/`. Either:
  - Update `src="images/produk1.jpg"` → `src="img/images/produk1.jpg"`, or
  - Move product images into a top-level `images/` folder and update the repo accordingly.

Example snippet to add/change a card:

```html
<div class="card">
  <img src="img/images/produk1.jpg" alt="Gamis Aulia">
  <div class="info">
    <h3>Gamis Aulia</h3>
    <p>Rp 120.000</p>
    <a href="#">Detail</a>
  </div>
</div>
```

---

## Notable issues & fixes to prioritize ⚠️
These are discoverable in `index.html` and should be addressed by any AI agent before submitting visual/content changes:
- Invalid CSS: `z-index: 100;5u` (typo) — should be `z-index: 100;`.
- HTML structure problems:
  - `<link rel="stylesheet" href="...font-awesome...">` is placed after `</head>` and before `<body>`; move it inside `<head>`.
  - `.social-float` markup is placed outside `<body>`; move the social links into the `<body>` to ensure valid HTML.
- Missing `alt` attributes on product `<img>` tags — add descriptive `alt` text for accessibility.
- Duplicate/overlapping media queries: check and consolidate repeated `@media (max-width: 600px)` blocks.
- External links should include `rel="noopener noreferrer"` when using `target="_blank"` for security.

---

## Testing and QA checklist ✅
- Start local server and verify at least Chrome/Firefox and a mobile viewport (responsive). Take screenshots for PRs.
- Verify Font Awesome icons load (move `<link>` into `<head>` if broken).
- Confirm all product images display (fix image paths or move files).
- Check for console errors (missing files, MIME, CORS) in DevTools.

---

## PR guidance / commit notes
- Keep changes scoped to small commits (e.g., "fix: correct image paths", "fix: move fontawesome into head").
- For visual changes add before/after screenshots in the PR description.
- Document any refactor that extracts CSS into a new file and keep the change minimal in the same PR.

---

If anything in this file is unclear or you want more detail (for example, a suggested CSS refactor or a canonical asset layout), tell me which area to expand and I will update this doc. ✨