# /create-brand-kit - Create Brand Kit

Build a complete brand kit from a short brief or from the assets already in the project, and write it to `brand/` as human-readable guidelines plus machine-readable design tokens.

## Steps

1. Collect the brief: brand name, one-line description, primary audience, 3-5 personality traits, and any fixed inputs (existing logo, mandated colors, required fonts). Ask only for what is missing
2. Scan the project for existing brand signals: logo files (`*.svg`, `*.png` named logo, brand, or mark), color definitions in CSS custom properties, Tailwind or theme configs, font imports, and any existing style guide or README branding
3. Decide the mode: **extract** (formalize what exists and fix inconsistencies) or **create** (design from the brief). Mixed is fine: keep a mandated logo and design everything else around it
4. Write the brand foundation: mission, positioning statement, values, personality traits with a short "we are / we are not" list, and the primary audience
5. Define the color system:
   - Pick primary, secondary, and accent hues; derive a 50-900 ramp for each by adjusting lightness in HSL or OKLCH while holding hue and chroma
   - Add a neutral ramp tinted toward the primary hue and semantic colors for success, warning, error, and info
   - Verify every text/background pair meets WCAG 2.1 AA (4.5:1 for normal text, 3:1 for large text and UI components); adjust lightness until it passes
   - Provide a dark-mode mapping for every role: background, surface, text, border, primary, accent
   - Record hex, RGB, and HSL for every swatch
6. Define typography: heading family, body family, monospace family if the brand ships code, web-safe fallback stacks, a modular type scale (for example a 1.25 ratio from a 16px base), weights in use, and line heights for headings and body
7. Write logo guidelines: primary lockup, horizontal and stacked variants, icon-only mark, monochrome and reversed versions, minimum size in px and mm, clear space expressed as a fraction of the mark height, and an explicit misuse list (no stretching, recoloring, drop shadows, or placement on busy backgrounds)
8. Specify supporting elements: spacing scale, border radius, elevation and shadows, iconography style (stroke weight, corner style, grid size), and imagery or illustration direction
9. Write voice and tone: 3-4 voice principles each with a do/don't example, tone shifts by context (marketing, product UI, error messages, support), vocabulary to use and avoid, and formatting conventions (capitalization, Oxford comma, numerals)
10. Generate the deliverables:
    - `brand/BRAND.md` with every section above and rendered swatch tables
    - `brand/tokens.json` in W3C Design Tokens format with color, typography, spacing, radius, and shadow groups
    - `brand/tokens.css` exposing the same tokens as CSS custom properties with a `[data-theme="dark"]` override block
    - `brand/assets/README.md` listing every required logo export (SVG, PNG at 1x/2x/3x, favicon sizes, social avatar sizes) and marking which exist versus which are still needed
11. Cross-check the kit: every color referenced in BRAND.md exists in tokens.json, every color token has a dark-mode value, every font has a fallback stack, and every AA pair is listed with its ratio
12. Present a summary: palette swatches with contrast results, a type specimen, the logo asset checklist, and the open decisions that need a human sign-off

## Format

```
Brand: <name>
Mode: <extract|create|mixed>
Primary: <hex> (<name>)  Secondary: <hex>  Accent: <hex>
Typography: <heading> / <body> / <mono>
AA Pairs: <passed>/<total>
Files: brand/BRAND.md, brand/tokens.json, brand/tokens.css, brand/assets/README.md
Needs Decision: <list>
```

## Rules

- Never invent logo artwork; describe the mark and its rules and list the files a designer must supply
- Keep the core palette small: one primary, one secondary, one accent, one neutral ramp, four semantic colors
- Every color pair intended for text must have a recorded WCAG ratio; do not ship a pair that fails AA
- Prefer open-license fonts (Google Fonts, Fontsource) unless the brief mandates a licensed family; note licensing for every family
- Use the brand's own words from the brief in voice examples, not generic marketing copy
- Write token values once and derive every format from them; hand-edited duplicates drift
- Do not overwrite an existing `brand/` directory without showing the diff first
