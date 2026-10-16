# /export-brand-tokens - Export Brand Tokens

Convert the brand kit's tokens into the formats a codebase consumes: CSS variables, Tailwind, SCSS, iOS, Android, and Figma.

## Steps

1. Locate the source of truth in `brand/tokens.json` (W3C Design Tokens format); if only `brand/BRAND.md` exists, parse its swatch and typography tables into tokens first
2. Validate the token file: every token has `$type` and `$value`, every alias such as `{color.primary.500}` resolves, and no two tokens share a name under different casing
3. Determine the target platforms from the argument or from the project (`tailwind.config.*`, `*.scss`, `Package.swift`, `build.gradle`, `.storybook/`)
4. Generate each requested output:
   - **CSS**: `:root` custom properties in kebab-case (`--color-primary-500`), a `[data-theme="dark"]` block for dark-mode overrides, and a `prefers-color-scheme` fallback
   - **Tailwind**: a preset extending `theme.colors`, `fontFamily`, `fontSize`, `spacing`, `borderRadius`, and `boxShadow` that references the CSS variables so runtime theming keeps working
   - **SCSS**: `$` variables and maps mirroring the token groups
   - **iOS**: a Swift enum with `UIColor` and `Color` extensions plus a `Font` helper
   - **Android**: `colors.xml`, `dimens.xml`, and a Compose `Theme.kt` color scheme
   - **Figma**: a Tokens Studio compatible JSON set with light and dark themes
5. Write outputs under `brand/dist/<platform>/` and leave the source tokens untouched
6. Add a short usage snippet at the top of each generated file showing how to import it
7. Diff the new output against any previous export and list added, removed, and changed tokens
8. If the project already has a token pipeline (Style Dictionary, Tokens Studio, Theo), generate a config for it instead of ad hoc files and explain how to run it

## Format

```
Source: brand/tokens.json (<N> tokens)
Platforms: <css|tailwind|scss|ios|android|figma>
Output: brand/dist/<platform>/...
Changes: +<added> -<removed> ~<changed>
```

## Rules

- Generated files must state that they are generated and name the source file
- Keep token names identical across platforms apart from the casing convention each target requires
- Export colors as hex for web, RGBA floats for iOS, and ARGB hex for Android
- Do not hardcode the dark theme into components; export it as an override layer
- Keep `brand/tokens.json` as the only hand-edited file
