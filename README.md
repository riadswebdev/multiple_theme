# Audit 4 — Exhaustive Client Color Usage and Migration Readiness

Generated inventory artifacts for the Whatstrend client. The scan covers application-owned source beneath `app/`, `components/`, `hooks/`, `lib/`, `src/`, `types/`, `utils/`, and `scripts/`, plus `tailwind.config.js`, `postcss.config.mjs`, and `next.config.mjs`; it excludes dependency/build/test/generated trees and static images.

## Artifacts

- [01-source-file-coverage.csv](01-source-file-coverage.csv): scanned source ledger, route and occurrence count.
- [02-color-occurrences.csv](02-color-occurrences.csv): line-level recognized color utilities, literals, token definitions/references, and inline style property occurrences.
- [03-color-definitions-and-token-catalog.csv](03-color-definitions-and-token-catalog.csv): deduplicated values/tokens and examples.
- [04-component-and-route-migration-map.csv](04-component-and-route-migration-map.csv): file-level migration review guide.
- [05-dynamic-styling-and-theme-dataflow.md](05-dynamic-styling-and-theme-dataflow.md): verified theme dataflow and dynamic style areas.
- [06-migration-classification-and-open-questions.md](06-migration-classification-and-open-questions.md): migration classification and decisions.
- [07-audit-validation-and-limitations.md](07-audit-validation-and-limitations.md): scan method, validation, exclusions, and limits.

## Coverage counts

- Source files scanned: 244
- Line-level occurrence records: 5461
- Unique kind/value catalog rows: 474
- App Router page/layout files: 65

## Route ledger

| Route | Source file | Occurrence records |
|---|---|---:|
| /add-friend/:userId | app/(app)/add-friend/[userId]/page.tsx | 11 |
| /calls/event/:id | app/(app)/calls/event/[id]/page.tsx | 95 |
| /calls/favourites | app/(app)/calls/favourites/page.tsx | 60 |
| /calls/keypad | app/(app)/calls/keypad/page.tsx | 34 |
| /calls | app/(app)/calls/page.tsx | 23 |
| /calls/schedule/new | app/(app)/calls/schedule/new/page.tsx | 88 |
| /calls/schedule | app/(app)/calls/schedule/page.tsx | 38 |
| /calls/select-contact | app/(app)/calls/select-contact/page.tsx | 0 |
| /calls/start | app/(app)/calls/start/page.tsx | 0 |
| /chats/archived | app/(app)/chats/archived/page.tsx | 0 |
| /chats/locked | app/(app)/chats/locked/page.tsx | 0 |
| /contact-picker/:purpose | app/(app)/contact-picker/[purpose]/page.tsx | 0 |
| /contacts | app/(app)/contacts/page.tsx | 0 |
| /conversations/:id/disappearing | app/(app)/conversations/[id]/disappearing/page.tsx | 19 |
| /conversations/:id/encryption | app/(app)/conversations/[id]/encryption/page.tsx | 14 |
| /conversations/:id/info | app/(app)/conversations/[id]/info/page.tsx | 8 |
| /conversations/:id/members | app/(app)/conversations/[id]/members/page.tsx | 1 |
| /conversations/:id | app/(app)/conversations/[id]/page.tsx | 87 |
| /conversations/:id/permissions | app/(app)/conversations/[id]/permissions/page.tsx | 28 |
| /conversations/:id/pinned | app/(app)/conversations/[id]/pinned/page.tsx | 11 |
| /conversations/:id/shared | app/(app)/conversations/[id]/shared/page.tsx | 32 |
| /conversations/:id/starred | app/(app)/conversations/[id]/starred/page.tsx | 11 |
| /conversations/:id/theme | app/(app)/conversations/[id]/theme/page.tsx | 78 |
| /diagnostics | app/(app)/diagnostics/page.tsx | 45 |
| /groups/:id | app/(app)/groups/[id]/page.tsx | 3 |
| /groups/invite/:token | app/(app)/groups/invite/[token]/page.tsx | 6 |
| /groups | app/(app)/groups/page.tsx | 27 |
| /inbox | app/(app)/inbox/page.tsx | 19 |
| / | app/(app)/layout.tsx | 0 |
| /notifications | app/(app)/notifications/page.tsx | 100 |
| /privacy | app/(app)/privacy/page.tsx | 147 |
| /profile/:userId | app/(app)/profile/[userId]/page.tsx | 48 |
| /profile | app/(app)/profile/layout.tsx | 0 |
| /profile | app/(app)/profile/page.tsx | 0 |
| /profile/qr | app/(app)/profile/qr/page.tsx | 0 |
| /profile/settings/:settingsPath* | app/(app)/profile/settings/[[...settingsPath]]/page.tsx | 0 |
| /reports | app/(app)/reports/page.tsx | 65 |
| /scan-profile | app/(app)/scan-profile/page.tsx | 18 |
| /settings/linked-dev | app/(app)/settings/linked-dev/page.tsx | 0 |
| /settings/linked-devices | app/(app)/settings/linked-devices/page.tsx | 63 |
| /settings | app/(app)/settings/page.tsx | 165 |
| /settings/security | app/(app)/settings/security/page.tsx | 57 |
| /status/:statusId/activity | app/(app)/status/[statusId]/activity/page.tsx | 61 |
| /stories | app/(app)/stories/page.tsx | 0 |
| /updates/channels/:channelId/info | app/(app)/updates/channels/[channelId]/info/page.tsx | 3 |
| /updates/channels/:channelId/invite | app/(app)/updates/channels/[channelId]/invite/page.tsx | 10 |
| /updates/channels/:channelId/notifications | app/(app)/updates/channels/[channelId]/notifications/page.tsx | 24 |
| /updates/channels/:channelId | app/(app)/updates/channels/[channelId]/page.tsx | 82 |
| /updates/channels/:channelId/share | app/(app)/updates/channels/[channelId]/share/page.tsx | 13 |
| /updates/channels/:channelId/storage | app/(app)/updates/channels/[channelId]/storage/page.tsx | 20 |
| /updates/channels/create | app/(app)/updates/channels/create/page.tsx | 40 |
| /updates/channels/explore | app/(app)/updates/channels/explore/page.tsx | 0 |
| /updates/channels | app/(app)/updates/channels/page.tsx | 38 |
| /updates/explore | app/(app)/updates/explore/page.tsx | 0 |
| /updates | app/(app)/updates/page.tsx | 43 |
| /auth/callback | app/auth/callback/page.tsx | 3 |
| / | app/error.tsx | 7 |
| / | app/global-error.tsx | 18 |
| / | app/globals.css | 11 |
| / | app/layout.tsx | 2 |
| /login | app/login/page.tsx | 0 |
| / | app/not-found.tsx | 19 |
| / | app/page.tsx | 1 |
| /profile/complete | app/profile/complete/page.tsx | 1 |
| /unauthorized | app/unauthorized/page.tsx | 9 |

## Important interpretation

This is a static source scan, not a rendered visual audit. Occurrence classifications are heuristic and should be reviewed before migration. The migration map does not authorize a bulk replacement. Conversation themes, user-generated story colors, media/video colors, and other feature-specific color domains must remain separate from app semantic colors unless a product decision explicitly changes that boundary.
