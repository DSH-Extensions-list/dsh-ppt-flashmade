# Design language reference (phases 3 and 4)

The active design profile and measured source-template geometry take precedence over these defaults. See `docs/contracts.md`, sections 19–21, and decisions ADR-061/066/067. Preserve profile fields for `typeScale`, `roles`, `palette`, `chrome`, and `background`.

## 1. Typography

| Element | Size | Color role | Font role |
|---|---|---|---|
| Cover title | 44 pt bold | title | heading |
| Cover metadata | 16 pt | body | body |
| Contents numbering | 40 pt | title | number |
| Contents entries | 20 pt | muted | body |
| Section watermark number | 85 pt | watermark | number |
| Section title | 34 pt | title | heading |
| Content title | 36 pt | title | heading |
| Card heading | 20 pt | accent | heading |
| Card body | 14 pt | body | body |
| Emphasized number | 32 pt | onAccent | number |
| Closing title | 54 pt | title | heading |
| Closing subtitle | 32 pt | accent | heading |
| Footer metadata | 16 pt | body | body |

Use at most four size levels on a page. Keep body text at least 14 pt, and strengthen hierarchy through weight and color before shrinking text. Use fonts declared in the profile. The font pass assigns heading to runs at least 28 pt, number to numeric runs at least 32 pt, and body otherwise. Preserve a clear title-to-body contrast; avoid introducing unrelated font families. Select installed fonts with coverage for the requested slide language.

## 2. Palette roles

| Role | Default | Purpose |
|---|---|---|
| `bg` | #FFFFFF | Page and flat background |
| `title` | #0D0D0D | Main headings |
| `accent` | #577FD2 | Section numbers, card headings, emphasis |
| `body` | #262626 | Body text |
| `muted` | #595959 | Secondary explanations and contents entries |
| `watermark` | #F2F7FA | Watermarks and large pale surfaces |
| `onAccent` | #FFFFFF | Text over accent fills |

Use no more than three principal text colors per page. Reserve muted text for supporting explanations. Text over photos or generated backgrounds needs an overlay and a body-text contrast ratio of at least 4.5:1. `audit --profile` checks this. Use `tokens.json` and `chartPalette` for charts and tables rather than inventing unrelated colors.

## 3. Role geometry

| Role | Title anchor (inches) | Columns | Card gap (inches) | Composition |
|---|---|---|---|---|
| cover | (0.69, 3.08) | 1 | — | Title at left; visual or negative space at right |
| toc | Theme-authored anchor | 3 | 1.04 | Number blocks and secondary labels; keep title above panels |
| section | (0.64, 3.43) | 1 | — | Watermark number and section heading |
| content | (0.59, 0.58) | 2–3 | 0.43 | Group related evidence without crowding |
| ending | (0.69, 3.79) | 1 | — | Conclusion or next action with negative space |

Honor the chosen theme's layout menu and a supplied template's geometry. The old measured contents anchor `(5.19, 1.79)` came from a number box; do not move the contents title there or place it under panels. For card layouts, column width is `(available width - gap * (columns - 1)) / columns`, bounded by `columnsMax`. Use cards when the content calls for them; vary the page rhythm with full-width visuals, timelines, charts, comparisons, quotations, and section breaks where supported.

Every storyboard page declares its role. `toc` is a storyboard role mapped to IR content; `data` and `quote` refine content. Keep measured geometry within 0.05 inches unless a deliberate redesign is recorded. Update both storyboard and IR when changing layout.

## 4. Backgrounds and assets

Prefer `svg`, then user assets, local Office assets, flat backgrounds, stock photos, and optional image generation. If a source is unavailable, choose a valid alternative and report it. Never invent sources or licenses.

| Mode | Source | Overlay | Attribution |
|---|---|---|---|
| `svg` | Programmatic artwork | `overlayOpacity` | No third-party asset attribution |
| `user` | `assets list/copy --source user` | At least 10% where text needs it | Each external asset declares its license in `asset-manifest.json` |
| `office` | `assets discover/list/copy --source office` | At least 10% where needed | Local resources; do not redistribute the resource library |
| `flat` | Profile `palette.bg` | None | None |
| `photo` | `images search` | 10–20% where needed | License and credit in `assets/image_sources.json` |
| `image-gen` | Optional `DSH_PPT_ENABLE_IMAGE_GEN=1` | 10–20% where needed | Record source and review generated content |

Declare the background mode in the storyboard/profile. Rendering applies overlays and enforces 4.5:1 body contrast. SVG backgrounds need a PNG fallback for older Office versions. Copy selected assets into the deck's `assets/` directory and preserve their source records. Openverse/Wikimedia search needs no API key; Pexels/Pixabay require configured keys. Generated artwork is optional and must not block ordinary deck creation.

Avoid filling the canvas with text or repeated cards. Reserve meaningful visual space where the content benefits from a visual; use valid local artwork, charts, or shapes rather than leaving unexplained placeholders. Keep private deck assets out of the extension's source repository and distribution package.

## 5. Page furniture

Declare page numbering, footer, and section markers once in `deck.fusion.json` under `chrome`. Do not hand-draw competing copies on every page. The profile controls whether numbering, section watermarks, and metadata footers appear. Rendering owns `chrome-` shapes and their geometry. The manifest wins a storyboard conflict; rerun `validate` and `audit` after changing chrome.

## 6. Review checklist

1. Each page has a role and a layout available for that role in the selected theme.
2. Typography, palette, and hierarchy remain consistent; text fits without excessive shrinking.
3. Page composition fits its purpose and preserves title clearance, alignment, and spacing.
4. Backgrounds and overlays are declared, contrast passes, and SVG artwork has its fallback.
5. Asset licenses and credits are complete; image generation remains optional.
6. Page furniture is declared once and remains consistent.
7. Render the exported PPTX, inspect contact sheets and detailed problem slides, and correct crowding, clipping, or overlap before delivery.
