---
name: red-hat-html-presentation
description: >-
  Red Hat branded HTML slideshow template and component library.
  Use this skill whenever asked to create a Red Hat presentation, deck, report,
  or slideshow. Produces a single self-contained .html file — no build tools,
  no dependencies beyond Google Fonts.
tags:
  - redhat
  - presentation
  - html
  - slide-design
  - red-hat-standard
---

# Red Hat HTML Presentation — Agent Skill

> **Read this file completely before generating or editing any Red Hat presentation.**
> The canonical format is a **single `.html` file**. Never produce a PPTX unless explicitly asked.

---

## 1. Quick-Start Protocol

When asked to create a Red Hat presentation:

1. **Copy** `template/base-presentation.html` as the starting skeleton.
2. **Replace** placeholder content slide by slide with real content.
3. **Pick components** from `references/html-elements/` for each slide's content type.
4. **Logo rule**: slide-header uses inline SVG (pre-baked into base template). Footer uses the OIL logo SVG via `::after` CSS, path: `../assets/logos/Logo-Red_Hat-Open_Innovation_Labs-A-Standard-RGB.svg` — or inline the SVG if the file must be self-contained.
5. **Output**: a single `.html` file named `<topic>-<date>.html` (e.g. `1to1-12-jun-26.html`).

---

## 2. Brand Constants (never change)

| Property | Value |
|----------|-------|
| Primary red | `#EE0000` |
| Dark red | `#CC0000` |
| Black | `#000000` |
| White | `#FFFFFF` |
| Light grey | `#f5f5f5` |
| Dark grey | `#595959` |
| Font | `'Red Hat Display', 'Helvetica Neue', Arial, sans-serif` |
| Google Fonts URL | `https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;700&display=swap` |
| Slide aspect ratio | 16:9 (max 1400×900px) |

---

## 3. HTML File Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><!-- Deck title --></title>
  <!-- Google Font -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;700&display=swap" rel="stylesheet">
  <style>/* === PASTE FULL CSS FROM base-presentation.html === */</style>
</head>
<body>
  <div class="progress-bar" id="progressBar"></div>
  <div class="presentation-container">
    <div class="deck-container">

      <!-- SLIDE 1: TITLE (always first) -->
      <div class="slide active title-slide"> ... </div>

      <!-- SLIDE N: CONTENT SLIDES -->
      <div class="slide"> ... </div>

      <!-- LAST SLIDE: CLOSING (title-slide variant) -->
      <div class="slide title-slide"> ... </div>

    </div>
  </div>

  <!-- Navigation bar -->
  <div class="navigation">
    <button class="nav-btn" id="prevBtn" onclick="changeSlide(-1)">&lsaquo;</button>
    <span class="slide-counter"><span id="currentSlide">1</span> / <span id="totalSlides"></span></span>
    <button class="nav-btn" id="nextBtn" onclick="changeSlide(1)">&rsaquo;</button>
  </div>

  <script>/* === PASTE NAV JS FROM base-presentation.html === */</script>
</body>
</html>
```

---

## 4. Slide Types Reference

| Slide Type | CSS Class(es) | When to Use |
|-----------|---------------|-------------|
| Title / Closing | `.slide.title-slide` | First and last slide; full-bleed red background |
| Content (standard) | `.slide` + `.slide-header` | Every information slide |
| Agenda | `.slide` + `<ul>` | Second slide; list of topics |
| Metrics | `.slide` + `.metric-grid` + `.metric-card` | KPIs, event stats, highlights (2–4 cards) |
| Bar Chart | `.slide` + `.bar-chart` | Category comparison with percentages |
| Quotes | `.slide` + `.quote-grid` + `.quote` | Verbatim feedback or testimonials |
| Challenge List | `.slide` + `.challenge-list` | Pain points, blockers, requirements |
| Recommendations | `.slide` + `.rec-grid` + `.rec-card` | Action items, next steps |
| Stop / Step Grid | `.slide` + `.stops-grid` + `.stop-card` | Journey stages, numbered steps (4 per row) |
| Tech Tile Grid | `.slide` + `.tech-grid` + `.tech-tile` | Product/solution portfolio (3-col grid) |
| Data Table | `.slide` + `.leads-table` | Tabular data: accounts, comparisons |
| Two-Column | `.slide` + `.two-col` | Side-by-side content panels |
| Dark Contrast Panel | `<div style="background:#1a1a1a; ...">` | Problem/solution pairs with dark card |

Detailed markup patterns for each: see `references/html-elements/`.

---

## 5. Standard Content Slide Pattern

Every non-title slide follows this pattern exactly:

```html
<div class="slide">
  <div class="slide-header">
    <!-- Inline Red Hat SVG logo — always use this exact SVG block -->
    <svg class="rh-logo" viewBox="0 0 613 145" xmlns="http://www.w3.org/2000/svg">
      <path fill="#e00" d="M127.47,83.49c12.51,0,30.61-2.58,30.61-17.46a14,14,0,0,0-.31-3.42l-7.45-32.36c-1.72-7.12-3.23-10.35-15.73-16.6C124.89,8.69,103.76.5,97.51.5,91.69.5,90,8,83.06,8c-6.68,0-11.64-5.6-17.89-5.6-6,0-9.91,4.09-12.93,12.5,0,0-8.41,23.72-9.49,27.16A6.43,6.43,0,0,0,42.53,44c0,9.22,36.3,39.45,84.94,39.45M160,72.07c1.73,8.19,1.73,9.05,1.73,10.13,0,14-15.74,21.77-36.43,21.77C78.54,104,37.58,76.6,37.58,58.49a18.45,18.45,0,0,1,1.51-7.33C22.27,52,.5,55,.5,74.22c0,31.48,74.59,70.28,133.65,70.28,45.28,0,56.7-20.48,56.7-36.65,0-12.72-11-27.16-30.83-35.78"/>
      <path d="M579.74,92.8c0,11.89,7.15,17.67,20.19,17.67a52.11,52.11,0,0,0,11.89-1.68V95a24.84,24.84,0,0,1-7.68,1.16c-5.37,0-7.36-1.68-7.36-6.73V68.3h15.56V54.1H596.78v-18l-17,3.68V54.1H568.49V68.3h11.25Zm-53,.32c0-3.68,3.69-5.47,9.26-5.47a43.12,43.12,0,0,1,10.1,1.26v7.15a21.51,21.51,0,0,1-10.63,2.63c-5.46,0-8.73-2.1-8.73-5.57m5.2,17.56c6,0,10.84-1.26,15.36-4.31v3.37h16.82V74.08c0-13.56-9.14-21-24.39-21-8.52,0-16.94,2-26,6.1l6.1,12.52c6.52-2.74,12-4.42,16.83-4.42,7,0,10.62,2.73,10.62,8.31v2.73a49.53,49.53,0,0,0-12.62-1.58c-14.31,0-22.93,6-22.93,16.73,0,9.78,7.78,17.24,20.19,17.24m-92.44-.94h18.09V80.92h30.29v28.82H506V36.12H487.93V64.41H457.64V36.12H439.55ZM370.62,81.87c0-8,6.31-14.1,14.62-14.1A17.22,17.22,0,0,1,397,72.09V91.54A16.36,16.36,0,0,1,385.24,96c-8.2,0-14.62-6.1-14.62-14.09m26.61,27.87h16.83V32.44l-17,3.68V57.05a28.3,28.3,0,0,0-14.2-3.68c-16.19,0-28.92,12.51-28.92,28.5a28.25,28.25,0,0,0,28.4,28.6,25.12,25.12,0,0,0,14.93-4.83ZM320,67c5.36,0,9.88,3.47,11.67,8.83H308.47C310.15,70.3,314.36,67,320,67M291.33,82c0,16.2,13.25,28.82,30.28,28.82,9.36,0,16.2-2.53,23.25-8.42l-11.26-10c-2.63,2.74-6.52,4.21-11.14,4.21a14.39,14.39,0,0,1-13.68-8.83h39.65V83.55c0-17.67-11.88-30.39-28.08-30.39a28.57,28.57,0,0,0-29,28.81M262,51.58c6,0,9.36,3.78,9.36,8.31S268,68.2,262,68.2H244.11V51.58Zm-36,58.16h18.09V82.92h13.77l13.89,26.82H292l-16.2-29.45a22.27,22.27,0,0,0,13.88-20.72c0-13.25-10.41-23.45-26-23.45H226Z"/>
    </svg>
    <h1>Slide Title Here</h1>
  </div>
  <h2>Optional subheading — one line max</h2>
  <!-- component markup here -->
</div>
```

**Rules**:
- `.slide-header` always contains the inline SVG logo + `<h1>` slide title.
- `<h2>` immediately after `.slide-header` is the subheading (optional but recommended).
- Never put the logo as an `<img src="...">` in content slides — always inline SVG.
- Footer OIL logo appears automatically via CSS `::after` on `.slide:not(.title-slide)`.

---

## 6. Title Slide Pattern

```html
<div class="slide active title-slide">
  <div class="title-content">
    <h1 class="main-title">Presentation Title</h1>
    <p class="subtitle">Event or Date</p>
  </div>
  <div class="presenters">
    <div class="presenter">
      <div class="presenter-name">Full Name</div>
      <div class="presenter-title">Job Title</div>
    </div>
    <!-- add more presenter divs as needed -->
  </div>
</div>
```

- Background is the red gradient: `linear-gradient(135deg, #EE0000 0%, #CC0000 100%)`.
- No header logo or footer logo on title/closing slides.
- For a closing/thank-you slide: omit `.presenters`, increase `font-size` on `.main-title`.

---

## 7. Assets in This Skill

| File | Use |
|------|-----|
| `assets/logos/RedHat-logo.svg` | Source for inline SVG (copy path data) |
| `assets/logos/Logo-Red_Hat-Open_Innovation_Labs-A-Standard-RGB.svg` | Footer logo (OIL standard colour) |
| `assets/logos/Logo-Red_Hat-Open_Innovation_Labs-A-White-RGB.svg` | Footer logo on dark backgrounds |
| `template/base-presentation.html` | Canonical copy-paste starting point |
| `template/component-library.html` | Live demo of every component |
| `references/html-elements/*.yaml` | Per-component markup + constraints |

---

## 8. Confidentiality Designator

Add to title slide above the title content when classification is required:

```html
<div class="confidential">CONFIDENTIAL — Red Hat associates only</div>
```

CSS for `.confidential`:
```css
.confidential {
  position: absolute;
  top: 20px;
  right: 24px;
  font-size: 0.7em;
  color: rgba(255,255,255,0.7);
  letter-spacing: 0.1em;
  text-transform: uppercase;
}
```

---

## 9. Print / PDF Export

### How to export a deck to PDF
1. Open the `.html` file in **Chrome** or **Edge** (not Safari — it strips backgrounds).
2. Press `Cmd+P` (macOS) or `Ctrl+P` (Windows).
3. Set **Destination** → "Save as PDF".
4. Under **More settings**: Layout = Landscape, Margins = None, enable **Background graphics**.
5. Save. Each slide prints as one A4 landscape page.

### What the `@media print` block does
The template includes a complete `@media print` block that:
- Sets `@page { margin: 0; size: A4 landscape; }` — removes browser margins, forces landscape.
- Shows all `.slide` divs simultaneously (`display: flex !important`), each on its own page via `break-after: page`.
- Hides `.navigation` and `.progress-bar`.
- Forces brand colours back on with `print-color-adjust: exact; -webkit-print-color-adjust: exact;` on every coloured element (browsers strip backgrounds by default unless this is set).
- Locks grid layouts (`stops-grid`, `rec-grid`, `metric-grid`) to their intended columns.

### Dark contrast panels and print
Slides using dark contrast panels (`.dark-panel`, `background:#1a1a1a`) will print dark by default.
Add the class `dark-panel` to the div alongside the inline styles:
```html
<div class="dark-panel" style="background:#1a1a1a; ...">
```
The `@media print` block in the template overrides `.dark-panel` to a light card with a red left border,
matching the challenge-list print style — preserving readability without wasting ink.

### Agent rule
When generating a new deck, always include the full `@media print` block from `template/base-presentation.html`.
Never strip or abbreviate it. Do not hardcode a slide count — the JS auto-detects it.

---

## 10. Accessibility Rules

- Minimum body text: `0.8em` (≥ 12px at base 16px).
- Slide title `<h1>` in `.slide-header`: `1.6em`.
- Never use colour alone to distinguish data series — add labels or patterns.
- `print-color-adjust: exact` must be present on every coloured background, border, and text element in the `@media print` block.

---

## 11. Generating a New Deck — Checklist

- [ ] Start from `template/base-presentation.html`
- [ ] Set `<title>` to the deck name
- [ ] Slide 1: title slide with presenter names and date
- [ ] Slide 2: agenda (if deck has 5+ slides)
- [ ] Content slides: pick component type, apply correct CSS classes
- [ ] Last slide: closing title slide ("Thank You" or summary)
- [ ] Verify nav JS `totalSlides` counter renders correctly (it's auto-calculated)
- [ ] All slide `<h1>` titles ≤ one line; all `<h2>` subheadings ≤ two lines
- [ ] No external image references in generated file (use inline SVG or data URIs)

---

## 12. PPTX Reference (legacy)

The original Red Hat Standard PPTX template rules are preserved in:
- `references/elements/` — per-element PPTX constraints
- `references/sections/` — section-level PPTX narrative patterns

These apply when the user explicitly requests a PowerPoint file.
