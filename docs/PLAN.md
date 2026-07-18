# Plan — from concept to PR

Mapping each proposed change to the real `posthog.com` code, so the diff stays small, honest, and reviewable. File paths are from `PostHog/posthog.com` (Gatsby + React + Tailwind; the forum is powered by their "Squeak" Q&A engine, data from a Strapi backend).

## What lives where

| Area | Real file(s) |
| --- | --- |
| "Ask a question" CTA copy | `src/components/Squeak/components/QuestionForm.tsx` (~L323), `src/components/Questions/QuestionForm.tsx` (label default ~L33) |
| Question list rows | `src/components/Questions/QuestionsTable.tsx` (the `Row`), `src/components/Squeak/components/Questions.tsx` |
| Level ladder + badge | `src/components/Squeak/util/getLevel.ts`, `src/components/Squeak/components/LevelBadge.tsx` |
| Community sidebar / topic order | `src/components/Community/Sidebar` + `src/navs` (`communityMenu`) |
| Buttons | `src/components/CallToAction` (orange, pressable; `bg-orange` + shadow) |

## Proposed PR slices

Small first, so it merges; the rest as fast follow-ups.

### PR 1 — surface the level badge in the question list *(smallest, safest, fully real)*
- Render `<LevelBadge points={...} />` beside the author in `QuestionsTable`'s `Row`. The component and points already exist; this only *shows* them where they're currently hidden.
- Ship the copy change with it: `"Ask a question" → "Start a discussion"`.
- No backend/Strapi change. No new data. Pure frontend.
- Keep `npm run build` green (lint + types run in build).

### PR 2 — community-first sidebar
- Reorder `communityMenu` so off-topic/community boards lead.
- Copy pass on section labels toward community voice.

### PR 3 — contributor spotlight ("Top hogs")
- A small module surfacing top contributors by points for a window (uses existing profile/points data).

## PostHog-native touches (worth doing, signals fit)
- **Gate behind a PostHog feature flag** so it can be rolled out / killed remotely.
- **Instrument the events** (e.g. discussion started, level badge seen/clicked) — using PostHog's own product to measure community work is the strongest possible fit signal for the role.

## Open questions for maintainers
- Appetite for the language shift (support desk → community) — confirm before the copy PR.
- Whether "Top hogs" should live on `/questions`, a `/community` surface, or as a profile-linked widget.
