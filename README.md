# Kiln

Mockup-only control-plane UI for a hypothetical in-house chip fab operated by Aetheron, a fictional AI/robotics/space-compute company.

Forge-aesthetic reskin (Tailwind Play CDN, zinc palette, shadcn-style components) of operational surfaces drawn from `~/Desktop/scm/` and `~/Desktop/forge/`.

## Pages

| File | Purpose | Source pattern |
|---|---|---|
| `dashboard.html` | Fab Floor — attention cards, KPI strip, active lots | SCM `dashboard.html` |
| `tools.html` | Tool fleet — ASML, AMAT, LAM, TEL, KLA list | SCM `vendors.html` |
| `tool-detail.html` | One tool — utilization, qual status, PM, lot history | SCM `vendor-detail.html` |
| `recipe.html` | Process flow editor — N3E die recipe, live lot tracker | Forge `canvas-build.html` |
| `lot-detail.html` | Single wafer lot's journey through the recipe | SCM `po-detail.html` |
| `bom.html` | Process BOM — masks, layers, chemistries for one product | SCM `bom-detail.html` |

## Running

Every page is self-contained HTML — open directly:

```
open dashboard.html
```

## Design system

- Tailwind via Play CDN (`https://cdn.tailwindcss.com`), no build.
- Zinc palette, rounded-md/lg, shadcn-style focus rings, "K" monogram.
- Status colors: emerald (good), amber (warn), red (crit), zinc (neutral).
- Cmd/Ctrl+K command palette and skip-link a11y are repeated inline per page.
- This is a sibling-copy. Do NOT pull SCM's `design-system.css` / SF Pro / frosted-glass patterns into Kiln.

## Glossary tooltips

Every page references `glossary.js`, a shared script that turns any element with `class="gl"` into a hover-tooltip with a plain-English definition pulled from a built-in dictionary (~80 semi-industry terms).

Markup pattern:

```html
<span class="gl" data-term="EUV">EUV Litho</span>
<span class="gl">CMP</span>          <!-- term inferred from text -->
<span class="gl" data-term="lot">25 lots</span>  <!-- visible text differs from term -->
```

The dictionary lives at the top of `glossary.js` — add or edit terms there. For pages with dynamically rendered content (e.g. `bom.html`'s collapsible tree), call `window.glossaryRefresh()` after the render.
