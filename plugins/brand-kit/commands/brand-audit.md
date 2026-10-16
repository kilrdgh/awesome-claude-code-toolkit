# /brand-audit - Audit Brand Consistency

Check a codebase, document set, or marketing copy against the brand kit and report every deviation.

## Steps

1. Load the brand kit from `brand/BRAND.md` and `brand/tokens.json`; stop and suggest `/create-brand-kit` if neither exists
2. Scope the audit from the argument: a directory, a file glob, or `all` for the whole project
3. Audit colors: find every hardcoded color literal in CSS, SCSS, styled-components, Tailwind arbitrary values, SVGs, and inline styles; match each against the palette with a small tolerance (Delta E under 3) and flag off-palette values
4. Audit typography: find font-family declarations, font imports, and weight or size values; flag families not in the kit and sizes that do not map to a type scale step
5. Audit logo usage: locate every logo asset reference; flag raster logos where an SVG exists, non-proportional sizing, logos below the minimum size, insufficient clear space in layout components, and recolored marks
6. Audit copy: sample headings, button labels, empty states, error messages, and marketing pages; check capitalization style, banned vocabulary, tone principles, and the brand name's spelling and casing
7. Audit dark mode: confirm every surface and text pairing has a dark-mode token and still meets WCAG AA in both themes
8. Audit spacing and radius: flag arbitrary pixel values where a spacing or radius token exists within 2px
9. Score each category (Color, Typography, Logo, Copy, Dark Mode, Spacing) as the percentage of checked instances that match the kit
10. Produce the report: a deviation table with file, line, current value, nearest kit value, and a suggested replacement
11. Offer an autofix for mechanical deviations (literal color to token, pixel spacing to token, raster logo to SVG) and apply it only when asked
12. List kit gaps found during the audit: colors or sizes used consistently in the project but absent from the kit, which may belong in it

## Format

```
Scope: <path>
Score: Color <N>%  Typography <N>%  Logo <N>%  Copy <N>%  Dark Mode <N>%  Spacing <N>%
Deviations: <count> (<autofixable> autofixable)
Top Issues:
  - <file>:<line> <current> -> <kit value>
Kit Gaps: <list>
```

## Rules

- Report each unique deviation once with an occurrence count, not every instance
- Treat third-party and vendored code as out of scope unless explicitly included
- Do not flag semantic colors (success, warning, error, info) as off-palette when they match the kit's semantic set
- Never apply autofixes without confirmation; the diff is the deliverable
- Copy findings are suggestions; wording decisions stay with the author
