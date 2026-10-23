# Dynamic Styling and Theme Dataflow

## Scope

This inventory is for the Next.js client only. The app-wide theme is not implemented in the inspected source. The code that is called “theme” today primarily controls conversation appearance.

## Conversation theme state

1. `client/hooks/useChatThemeStore.ts` defines `ChatThemeConfig`, `DEFAULT_CHAT_THEME`, a global theme and per-conversation `customThemes` map.
2. On the client, the store hydrates from `localStorage` under `whatstrend:chat-theme-store:v1` (`:50`, `:190-225`, `:300-302`). It normalizes legacy aliases such as `bubbleColor`, `outgoingBubbleBg`, and `outgoingBubbleColor` (`:79-134`). Numeric brightness, scale, and position are clamped or checked; color strings are passed through as strings.
3. `client/lib/themesConfig.ts` supplies ten preset wallpaper and bubble palettes.
4. `client/app/(app)/conversations/[id]/theme/page.tsx` constructs previews and drafts, then calls the store update methods for theme selection/customization.
5. `client/app/(app)/conversations/[id]/page.tsx` obtains the active theme through `useChatThemeForConversation` and applies wallpaper URL/color, brightness, scale, and position to the wallpaper layer (`:173-177`, `:896-909`).
6. `client/components/messaging/MessageList.tsx` receives active theme data and applies bubble background, text, and border colors through inline styles; its helper converts hex to RGBA for subtle quote backgrounds.

This flow affects conversation-specific UI and should not be conflated with application theme selection. No shared application-theme preference/controller was identified in the client source scan.

## Other dynamic styling domains

- **Story composer:** `client/components/stories/StoryComposer.tsx` keeps drawing brush and text colors in editor state. These represent user content and authoring controls, not necessarily app chrome.
- **Story rendering:** `client/components/stories/StoryTray.tsx` uses SVG `stopColor` and `stroke` values for a decorative progress ring.
- **Media and upload progress:** `client/components/media/MediaUploader.tsx` and channel upload UI set progress width dynamically while supplying fixed utility colors.
- **Calls:** calling components use color utilities and occasional inline `currentColor`/opacity for quality indicators and states.
- **Message state:** `MessageList.tsx` uses dynamic bubble colors and statuses, with selected/failed overlays and call-event cards.

## Application-wide theming seam

Potential seam, not yet implemented: root document theme selector → CSS custom-property theme values → Tailwind CSS 4 semantic utilities and direct CSS variable consumers. A small selection controller would manage a named preference. This would not need to alter the chat-theme store, story-editor content palette, or media overlays.

## Compatibility and open details

- Existing chat preferences are local to a browser profile and stored in a dedicated key. This scan does not establish cross-device synchronization or whether that preference is intended to be account-bound.
- The chat theme store color fields are free-form strings rather than a validated palette ID. A later app-theme implementation should not retroactively restrict existing conversation data without a migration/compatibility decision.
- App-level color use includes arbitrary utilities and direct literals; dynamic consumer audit must include inline styles and library props, not only class names.
