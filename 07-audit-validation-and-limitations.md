# Audit Validation and Limitations

## Static coverage performed

- Scanned **244 client-owned source files** from `app/`, `components/`, `hooks/`, `lib/`, `src/`, `types/`, `utils/`, and `scripts/`, plus `tailwind.config.js`, `postcss.config.mjs`, and `next.config.mjs`.
- Excluded `node_modules`, `.next`, test directories/files, browser-test directories, coverage/test output directories, declaration files, and public binary assets from code occurrence scanning.
- Recorded **5,461 line-level recognized occurrences** across **474 unique kind/value entries**. These are scanner records, not 5,461 distinct rendered colors. A source line can yield multiple records (for example, a class utility and a variable reference).
- The coverage ledger contains **65 App Router route/layout entries** discovered from route source files. Each route is linked to its source page/layout file and line-level occurrence count.
- Kept visual assets separate from code scans. Image files found in the client public asset inventory are `assets/wallpapers/chat-theme-amoled.png`, `chat-theme-aurora.png`, `chat-theme-cyber.png`, `chat-theme-geometric.png`, `chat-theme-lavender.png`, `chat-theme-mint.png`, `chat-theme-nature.png`, `chat-theme-ocean.png`, `chat-theme-paper.png`, `chat-theme-sunset.png`, `desktop-default-theme.png`, `mobile-default-theme.png`, and `whatstrend-logo.png`. The ten `chat-theme-*` files are under `client/public/assets/wallpapers/`; the defaults and logo are directly under `client/public/`. Assets were listed by filename, not analyzed at pixel level.

## Recognition approach

The generated occurrence CSV recognizes:

- Hex literals.
- `rgb()`, `rgba()`, `hsl()`, `hsla()`, `oklch()`, `oklab()`, and `color()` functions.
- Common Tailwind named color utilities, including palette families and opacity suffixes.
- CSS custom property definitions and `var(--...)` references.
- Common inline-style property names associated with background, text, border, outline, fill, stroke, and shadow colors.

The component and route map joins occurrences to their source file, file basename/module, and App Router route (where applicable). Shared component consumers are not statically resolved to every route importing them; the component source is the ownership record.

## Validation status

- No application source, configuration, or assets were modified.
- The one-off inventory generator was executed with the available Node.js runtime and then removed from the artifact directory.
- The generated CSV files were checked for headers, file sizes, line totals, and aggregate counts.
- No build, lint, unit test, browser test, or screenshot test was run. This was a static inventory, and those commands were unnecessary to enumerate source occurrences.
- Visual assets were identified by filename but not inspected pixel-by-pixel.

## Limitations and interpretation cautions

1. **Heuristic classifications:** Meaning labels are inferred from value and line context. Similar colors can serve different roles; the CSV does not substitute for component-owner review.
2. **Static source only:** Runtime-generated class names, values loaded from remote data, browser-computed colors, CSS-in-JS inside dependencies, and dynamically constructed CSS not matching the recognizers may be missed.
3. **Tailwind arbitrary utilities:** The scanner recognizes common named palette utilities and some syntax patterns, but arbitrary utility forms can be missed or may be split into separate records. Review the source when assessing a component.
4. **Third-party CSS:** `@heroui/styles` and React Toastify styles are imported but dependency source and resolved computed styles were not exhaustively inventoried.
5. **Visual assets:** Asset pixels, gradients baked into images, and video content do not appear as code color occurrences.
6. **Route ownership:** Shared components can be used by multiple pages; the CSV maps them to their owning source file, not a complete import graph.
7. **Tests excluded:** Test fixtures are not production styling and were excluded. Tests may still document expected palette values and should be used as migration regression references.
8. **No runtime appearance verification:** Light/dark screenshots, contrast calculations, computed-style inspection, and generated Tailwind CSS inspection remain for implementation validation.
9. **Scope:** This audit is client-only. Admin and backend code were not part of the coverage ledger.
