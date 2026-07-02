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

## 1. Brand Authority

**All colour values, font assignments, and accessibility rules come from the branding rule** (`.cursor/rules/branding.mdc`). Do not redefine brand constants here — read them from the rule.

Key points from the branding rule that apply to presentations:
- Use `#ee0000` / `#cc0000` for the title-slide gradient.
- Body text uses 'Red Hat Text'; headings use 'Red Hat Display'.
- UX Black is `#151515`, not `#000000`.
- Sentence case for all headlines.
- Print blocks require `print-color-adjust: exact`.

If the branding rule and this skill conflict, the branding rule wins.

**Non-Cursor environments** (Claude, Antigravity): read `.cursor/rules/branding.mdc` in this repo for brand values.

---

## 2. Quick-Start Protocol

When asked to create a Red Hat presentation:

1. **Copy** `template/base-presentation.html` as the starting skeleton.
2. **Replace** placeholder content slide by slide with real content.
3. **Pick components** from `references/html-elements/` for each slide's content type.
4. **Logo rule**: slide-header uses inline SVG (pre-baked into base template). Footer uses the OIL logo SVG via `::after` CSS, path: `../assets/logos/Logo-Red_Hat-Open_Innovation_Labs-A-Standard-RGB.svg` — or inline the SVG if the file must be self-contained.
5. **Output**: a single `.html` file named `<topic>-<date>.html` (e.g. `1to1-23-jun-26.html`).

---

## 3. Presentation-Specific Constants

These extend the branding rule for slide layouts only:

| Property | Value |
|----------|-------|
| Light grey (slide backgrounds) | `#f5f5f5` |
| Dark grey (captions) | `#595959` |
| Slide aspect ratio | 16:9 (max 1400 × 900px) |
| Font stack fallback | `'Red Hat Display', 'Red Hat Text', 'Helvetica Neue', Arial, sans-serif` |

---

## 4. HTML File Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><!-- Deck title --></title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;700&family=Red+Hat+Text:wght@400;700&family=Red+Hat+Mono:wght@400;700&display=swap" rel="stylesheet">
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

## 5. Slide Types Reference

| Slide Type | CSS Class(es) | When to Use |
|-----------|---------------|-------------|
| Title / Closing | `.slide.title-slide` | First and last slide; full-bleed red gradient |
| Content (standard) | `.slide` + `.slide-header` | Every information slide |
| Agenda | `.slide` + `<ul>` | Second slide; list of topics |
| Metrics | `.slide` + `.metric-grid` + `.metric-card` | KPIs, highlights (2–4 cards) |
| Bar Chart | `.slide` + `.bar-chart` | Category comparison with percentages |
| Quotes | `.slide` + `.quote-grid` + `.quote` | Verbatim feedback or testimonials |
| Challenge List | `.slide` + `.challenge-list` | Pain points, blockers, requirements |
| Recommendations | `.slide` + `.rec-grid` + `.rec-card` | Action items, next steps |
| Stop / Step Grid | `.slide` + `.stops-grid` + `.stop-card` | Journey stages, numbered steps (4 per row) |
| Tech Tile Grid | `.slide` + `.tech-grid` + `.tech-tile` | Product/solution portfolio (3-col grid) |
| Data Table | `.slide` + `.leads-table` | Tabular data: accounts, comparisons |
| Two-Column | `.slide` + `.two-col` | Side-by-side content panels |
| Dark Contrast Panel | `.dark-panel` | Problem/solution pairs with dark card |

Detailed markup patterns for each: see `references/html-elements/`.

---

## 6. Standard Content Slide Pattern

Every non-title slide follows this pattern:

```html
<div class="slide">
  <div class="slide-header">
    <svg class="rh-logo" viewBox="0 0 613 145" xmlns="http://www.w3.org/2000/svg">
      <path fill="#e00" d="M127.47,83.49c12.51,0,30.61-2.58,30.61-17.46a14,14,0,0,0-.31-3.42l-7.45-32.36c-1.72-7.12-3.23-10.35-15.73-16.6C124.89,8.69,103.76.5,97.51.5,91.69.5,90,8,83.06,8c-6.68,0-11.64-5.6-17.89-5.6-6,0-9.91,4.09-12.93,12.5,0,0-8.41,23.72-9.49,27.16A6.43,6.43,0,0,0,42.53,44c0,9.22,36.3,39.45,84.94,39.45M160,72.07c1.73,8.19,1.73,9.05,1.73,10.13,0,14-15.74,21.77-36.43,21.77C78.54,104,37.58,76.6,37.58,58.49a18.45,18.45,0,0,1,1.51-7.33C22.27,52,.5,55,.5,74.22c0,31.48,74.59,70.28,133.65,70.28,45.28,0,56.7-20.48,56.7-36.65,0-12.72-11-27.16-30.83-35.78"/>
      <path d="M579.74,92.8c0,11.89,7.15,17.67,20.19,17.67a52.11,52.11,0,0,0,11.89-1.68V95a24.84,24.84,0,0,1-7.68,1.16c-5.37,0-7.36-1.68-7.36-6.73V68.3h15.56V54.1H596.78v-18l-17,3.68V54.1H568.49V68.3h11.25Zm-53,.32c0-3.68,3.69-5.47,9.26-5.47a43.12,43.12,0,0,1,10.1,1.26v7.15a21.51,21.51,0,0,1-10.63,2.63c-5.46,0-8.73-2.1-8.73-5.57m5.2,17.56c6,0,10.84-1.26,15.36-4.31v3.37h16.82V74.08c0-13.56-9.14-21-24.39-21-8.52,0-16.94,2-26,6.1l6.1,12.52c6.52-2.74,12-4.42,16.83-4.42,7,0,10.62,2.73,10.62,8.31v2.73a49.53,49.53,0,0,0-12.62-1.58c-14.31,0-22.93,6-22.93,16.73,0,9.78,7.78,17.24,20.19,17.24m-92.44-.94h18.09V80.92h30.29v28.82H506V36.12H487.93V64.41H457.64V36.12H439.55ZM370.62,81.87c0-8,6.31-14.1,14.62-14.1A17.22,17.22,0,0,1,397,72.09V91.54A16.36,16.36,0,0,1,385.24,96c-8.2,0-14.62-6.1-14.62-14.09m26.61,27.87h16.83V32.44l-17,3.68V57.05a28.3,28.3,0,0,0-14.2-3.68c-16.19,0-28.92,12.51-28.92,28.5a28.25,28.25,0,0,0,28.4,28.6,25.12,25.12,0,0,0,14.93-4.83ZM320,67c5.36,0,9.88,3.47,11.67,8.83H308.47C310.15,70.3,314.36,67,320,67M291.33,82c0,16.2,13.25,28.82,30.28,28.82,9.36,0,16.2-2.53,23.25-8.42l-11.26-10c-2.63,2.74-6.52,4.21-11.14,4.21a14.39,14.39,0,0,1-13.68-8.83h39.65V83.55c0-17.67-11.88-30.39-28.08-30.39a28.57,28.57,0,0,0-29,28.81M262,51.58c6,0,9.36,3.78,9.36,8.31S268,68.2,262,68.2H244.11V51.58Zm-36,58.16h18.09V82.92h13.77l13.89,26.82H292l-16.2-29.45a22.27,22.27,0,0,0,13.88-20.72c0-13.25-10.41-23.45-26-23.45H226Z"/>
    </svg>
    <h1>Slide title here</h1>
  </div>
  <h2>Optional subheading — one line max</h2>
  <!-- component markup here -->
</div>
```

**Rules**:
- `.slide-header` always contains the inline SVG logo + `<h1>` slide title.
- `<h2>` immediately after `.slide-header` is the subheading (optional but recommended).
- Never put the logo as an `<img src="...">` — always inline SVG.
- Footer OIL logo appears via CSS `::after` on `.slide:not(.title-slide)`.

---

## 7. Title Slide Pattern

```html
<div class="slide active title-slide">
  <div class="title-content">
    <h1 class="main-title">Presentation title</h1>
    <p class="subtitle">Event or date</p>
  </div>
  <div class="presenters">
    <div class="presenter">
      <div class="presenter-name">Full Name</div>
      <div class="presenter-title">Job title</div>
    </div>
  </div>
</div>
```

- Background: `linear-gradient(135deg, #ee0000 0%, #cc0000 100%)`.
- No header logo or footer logo on title/closing slides.
- For a closing slide: omit `.presenters`, increase `font-size` on `.main-title`.

---

## 8. Assets in This Skill

| File | Use |
|------|-----|
| `.cursor/rules/branding.mdc` | Brand values and constraints (colour, fonts, a11y, print) |
| `assets/logos/RedHat-logo.svg` | Source for inline SVG (copy path data) |
| `assets/logos/Logo-Red_Hat-Open_Innovation_Labs-A-Standard-RGB.svg` | Footer logo (OIL standard colour) |
| `assets/logos/Logo-Red_Hat-Open_Innovation_Labs-A-White-RGB.svg` | Footer logo on dark backgrounds |
| `template/base-presentation.html` | Canonical copy-paste starting point |
| `template/component-library.html` | Live demo of every component |
| `references/html-elements/*.yaml` | Per-component markup + constraints |

---

## 9. Confidentiality Designator

Add to title slide when classification is required:

```html
<div class="confidential">CONFIDENTIAL — Red Hat associates only</div>
```

---

## 10. Print / PDF Export

Follow the branding rule's print guidance (Section 8). Additionally for presentations:

1. Open in **Chrome** or **Edge** (Safari strips backgrounds).
2. `Ctrl+P` → "Save as PDF" → Landscape, Margins: None, Background graphics: On.
3. Each slide prints as one landscape page via `break-after: page`.

The `@media print` block in `template/base-presentation.html` must:
- Show all slides simultaneously (`display: flex !important`).
- Hide `.navigation` and `.progress-bar`.
- Force brand colours with `print-color-adjust: exact`.
- Override `.dark-panel` to a light card with red left border for readability.

When generating a new deck, always include the full `@media print` block from the template. Never strip or abbreviate it. Do not hardcode a slide count — the JS auto-detects it.

See `references/html-elements/print-guide.yaml` for the complete print CSS block.

---

## 11. Generating a New Deck — Checklist

- [ ] Start from `template/base-presentation.html`
- [ ] Set `<title>` to the deck name
- [ ] Slide 1: title slide with presenter names and date (sentence case)
- [ ] Slide 2: agenda (if deck has 5+ slides)
- [ ] Content slides: pick component type, apply correct CSS classes
- [ ] Last slide: closing title slide
- [ ] All text uses 'Red Hat Text' for body, 'Red Hat Display' for headings
- [ ] UX Black `#151515` used (not `#000000`)
- [ ] Sentence case on all headlines
- [ ] No external image references (inline SVG or data URIs only)
- [ ] Full `@media print` block included
- [ ] Nav JS auto-detects slide count (no hardcoded number)

---

## 12. PPTX Reference (legacy)

The original Red Hat Standard PPTX template rules are preserved in:
- `references/elements/` — per-element PPTX constraints
- `references/sections/` — section-level PPTX narrative patterns

These apply when the user explicitly requests a PowerPoint file.
