# Red Hat HTML Presentation Skill

An AI agent skill and asset library for generating brand-consistent Red Hat HTML presentations. Produces single-file, self-contained `.html` slideshows — no build tools, no dependencies beyond Google Fonts.

Built from real presentations created at Red Hat Open Innovation Labs (APAC).

---

## What this is

A **branding rule** + **skill** (read by AI agents) + a **template library** (copy-paste HTML) for anyone who needs to create Red Hat-branded presentations.

- **`.cursor/rules/branding.mdc`** — owns brand values (colours, fonts, accessibility, print)
- **`SKILL.md`** — owns the presentation workflow (layout, slide types, checklist)
- **`template/`** — canonical HTML/CSS starting point

Works with:
- [Cursor](https://cursor.sh) (rule + skill)
- [Claude](https://claude.ai) (via `~/.claude/skills/`)
- [Antigravity](https://antigravity.dev) / Google IDE (via `~/.gemini/config/skills/`)

---

## Quick start

### For AI agents
Point your agent at `SKILL.md`. It defers to `.cursor/rules/branding.mdc` for all brand values and contains the full presentation specification — file structure, slide types, component CSS classes, logo rules, and print instructions.

### For humans
1. Copy `template/base-presentation.html` to your project folder.
2. Replace placeholder content slide by slide.
3. Open in Chrome and press `Cmd+P` → Save as PDF to export.

---

## Repository structure

```
redhat-presentation-skill/
├── .cursor/rules/
│   └── branding.mdc                  # Brand values and constraints
├── SKILL.md                          # Agent instruction file — read this first
├── assets/
│   └── logos/
│       ├── RedHat-logo.svg                                          # Red Hat horizontal logo
│       ├── Logo-Red_Hat-Open_Innovation_Labs-A-Standard-RGB.svg     # OIL logo (colour)
│       └── Logo-Red_Hat-Open_Innovation_Labs-A-White-RGB.svg        # OIL logo (white, for dark backgrounds)
├── template/
│   ├── base-presentation.html        # Canonical starting point — copy and fill in
│   └── component-library.html        # Live demo of all 13 component types
└── references/
    └── html-elements/                # Per-component markup patterns and constraints
        ├── title-slide.yaml
        ├── slide-header.yaml
        ├── metric-card.yaml
        ├── bar-chart.yaml
        ├── quote-block.yaml
        ├── challenge-list.yaml
        ├── rec-card.yaml
        ├── stop-card.yaml
        ├── tech-tile.yaml
        ├── data-table.yaml
        ├── dark-contrast-panel.yaml
        ├── nav-boilerplate.yaml
        └── print-guide.yaml
```

---

## Brand constants

Brand values are defined in `.cursor/rules/branding.mdc`. Key tokens for presentations:

| Token | Value |
|-------|-------|
| Red Hat Red | `#EE0000` |
| Dark Red | `#CC0000` |
| UX Black | `#151515` |
| Light grey | `#f5f5f5` |
| Dark grey | `#595959` |
| Headings | `'Red Hat Display'` |
| Body | `'Red Hat Text'` |
| Slide size | 1400 × 900 px (16:9) |

---

## Slide types

| Type | CSS Class(es) | Use for |
|------|--------------|---------|
| Title / Closing | `.slide.title-slide` | Opening and closing slides — full-bleed red |
| Standard content | `.slide` + `.slide-header` | Every information slide |
| Agenda | `.slide` + `<ul>` | Topic list (slide 2) |
| Metric grid | `.metric-grid` + `.metric-card` | KPIs and stats — 2 to 4 cards |
| Bar chart | `.bar-chart` + `.bar-item` + `.bar` | Category comparison with percentages |
| Quote grid | `.quote-grid` + `.quote` | Verbatim feedback or testimonials |
| Challenge list | `.challenge-list` | Pain points, blockers, requirements |
| Recommendations | `.rec-grid` + `.rec-card` | Next steps — title + detail + action line |
| Step cards | `.stops-grid` + `.stop-card` | Journey stages — numbered, 4-col grid |
| Tech tiles | `.tech-grid` + `.tech-tile` | Product/solution portfolio — 3-col grid |
| Data table | `.table-container` + `.leads-table` | Accounts, comparisons, structured data |
| Two columns | `.two-col` + `.col` | Side-by-side content |
| Dark contrast panel | `.dark-panel` | Problem/solution pairs on dark background |

---

## Logo rule

- **Slide header**: always inline SVG Red Hat logo — copy the path data from `assets/logos/RedHat-logo.svg`, never use `<img src="...">`.
- **Footer**: OIL logo via CSS `::after` on `.slide:not(.title-slide)`, referencing `assets/logos/Logo-Red_Hat-Open_Innovation_Labs-A-Standard-RGB.svg`.
- **Title slides**: no logos (both header and footer are suppressed via CSS).

---

## Printing / PDF export

1. Open the `.html` file in **Chrome** or **Edge** — not Safari (it strips background colours).
2. Press `Cmd+P` → Save as PDF.
3. Set: Layout = Landscape, Margins = None, enable **Background graphics**.
4. Save — one slide per A4 landscape page.

The `@media print` block handles:
- Showing all slides simultaneously (overriding the interactive display logic)
- `break-after: page` for one slide per page
- `print-color-adjust: exact` on all coloured elements to preserve brand colours
- Dark contrast panels (`.dark-panel`) converted to light cards for ink efficiency

See `references/html-elements/print-guide.yaml` for the complete print CSS block. General print rules are in `.cursor/rules/branding.mdc` Section 8.

---

## Installing as an agent skill

### Cursor (recommended — install both rule and skill)

```bash
# Branding rule (always-on brand values)
mkdir -p ~/.cursor/rules
cp .cursor/rules/branding.mdc ~/.cursor/rules/

# Presentation skill (workflow + templates)
mkdir -p ~/.cursor/skills/red-hat-html-presentation
cp -r . ~/.cursor/skills/red-hat-html-presentation/
```

### Claude

```bash
cp -r . ~/.claude/skills/rh-presentation-skills
```

Claude does not load Cursor rules automatically — agents should read `.cursor/rules/branding.mdc` from the skill directory for brand values.

### Antigravity (Google IDE)

```bash
cp -r . ~/.gemini/config/skills/varkrish/rh-presentation-html
```

---

## Examples

Real presentations built with this template:

- **1-to-1 Meeting decks** — weekly manager check-ins with agenda, metrics, and key topics
- **Ansible Quest Post-Event Report** — 11-slide event report with survey data, bar charts, quotes, recommendation cards, and dark contrast panels
- **Field Enablement Decks** — customer-facing presentations with tech tile grids and challenge lists

---

## License

MIT — see [LICENSE](LICENSE).  
Logos are Red Hat trademarks — use in accordance with [Red Hat brand guidelines](https://brand.redhat.com).
