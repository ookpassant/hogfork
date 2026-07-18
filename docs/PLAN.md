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

Small first, so it merges; the rest as fast follow-ups. (Rank badges are deliberately **not** added to the topic list — see Bet 2 in the README.)

### PR 1 — voice + framing *(smallest, safest, pure copy/nav)*
- `"Ask a question" → "Start a discussion"`; `"Questions" → "Community discussions"`.
- Reorder `communityMenu` so community boards lead and product topics group under "Product talk".
- Add the "this is a community, not a support queue → talk to a human" pointer.
- No backend, no new data, no schema. Copy + nav order only. Keep `npm run build` green.

### PR 2 — ProBoards-style board grouping
- Group the question list under category bars (community vs product) instead of one flat list, in PostHog's skin.
- Presentational; reads from the topics that already exist.

### PR 3 — contributor spotlight ("Top hogs")
- A small module surfacing top contributors by their existing points/levels (`getLevel.ts`). Uses data that's already there — no new fields.

### Later — signatures
- A per-profile `signature` line under posts. Needs a **profile field on the Strapi backend**, so it's a bigger, separate change — worth doing, not the opening move.

## PostHog-native touches (worth doing, signals fit)
- **Gate behind a PostHog feature flag** so it can be rolled out / killed remotely.
- **Instrument the events** (e.g. discussion started, level badge seen/clicked) — using PostHog's own product to measure community work is the strongest possible fit signal for the role.

## Open questions for maintainers
- Appetite for the language shift (support desk → community) — confirm before the copy PR.
- Whether "Top hogs" should live on `/questions`, a `/community` surface, or as a profile-linked widget.
