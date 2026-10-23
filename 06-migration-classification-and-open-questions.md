# Migration Classification and Open Questions

## Classification guidance

| Classification | Source area / examples | Migration treatment |
|---|---|---|
| App semantic colors | Global page/surface/text styles, shared app-shell surfaces, navigation, common controls and dialogs | Candidate for app theme tokens after role assignment and visual validation |
| Shared component state | Focus, hover, selected, disabled, loading, warning, success and destructive states | Candidate for semantic tokens; keep state meaning distinct from palette hue |
| Conversation-specific appearance | `client/hooks/useChatThemeStore.ts`, `client/lib/themesConfig.ts`, conversation theme route and message bubbles | Preserve as a separate user customization domain; do not mass-replace with app tokens |
| User-authored/content color | Story brush/text colors and other authoring data | Keep content data independent unless product policy explicitly says otherwise |
| Media/call/decorative | Video black backgrounds, screen share, SVG gradients, chart-like indicators, shadows and decorative gradients | Review case by case; many are feature-specific or technical display requirements |
| Third-party library styling | HeroUI and Toastify styles | Check the installed library’s supported theming hooks and overrides before migration |
| Unclear/legacy | Colors in unusual dynamic branches, aliases or seldom-used routes | Inspect owning component and rendered state; do not infer meaning from hue alone |

`02-color-occurrences.csv` records a heuristic role classification. It is a triage aid; the source line and owning component remain the evidence of record.

## Priority order for a later implementation

1. Confirm which preferences are needed: system, light, dark, or named branded variants; decide the initial default.
2. Confirm persistence scope (device-local versus account-level) and first-render behavior.
3. Verify Tailwind CSS 4 token/config behavior and the supported HeroUI styling contract.
4. Tokenize root page/surface/text/border/focus roles, then shared shell/components.
5. Migrate route feature families in reviewable batches, following the source coverage and route maps.
6. Review all dynamic styles and semantics before touching conversation themes or user content colors.
7. Remove obsolete literals only after static search and visual regression checks confirm no consumer remains.

## Decisions and investigation still needed

- Should system preference be supported, and should an explicit user choice override it?
- Should the app theme preference be local to a device or synchronized with the account? No app-level storage model was found.
- What should remain the default for existing users? Current root layout explicitly forces dark styling.
- Which roles and variants are actually necessary? The taxonomy should be informed by components and states rather than every Tailwind color shade.
- Which HeroUI CSS variables/roles are supported by installed `@heroui/styles` 3.2.4?
- Is the JavaScript Tailwind config loaded under the current Tailwind 4 CSS-first setup? It defines custom login animations, but generated CSS was not built/verified.
- Which direct colors are intentionally brand/content colors, as opposed to app chrome?
- Should chat theme values remain per-conversation and browser-local? This inventory observed current local persistence but cannot determine intended product policy.
- Are there visual requirements for high contrast, custom brand themes, or color-blind-safe state indicators beyond standard light/dark themes?

## Explicitly out of scope

This migration classification does not include admin or backend styling changes and does not prescribe redesigning the chat theme UI or data model.
