# Plan: from concept to PR

This maps each change to the real posthog.com code, so the diff stays small, honest, and easy to review. Paths are from PostHog/posthog.com (Gatsby, React, Tailwind). The forum runs on their "Squeak" Q&A engine, with data from a Strapi backend.

## Where things live

| Area | Real file(s) |
| --- | --- |
| "Ask a question" copy | `src/components/Squeak/components/QuestionForm.tsx` (~L323), `src/components/Questions/QuestionForm.tsx` (label default ~L33) |
| Question list rows | `src/components/Questions/QuestionsTable.tsx` (the `Row`), `src/components/Squeak/components/Questions.tsx` |
| Level ladder and badge | `src/components/Squeak/util/getLevel.ts`, `src/components/Squeak/components/LevelBadge.tsx` |
| Community sidebar and topic order | `src/components/Community/Sidebar` and `src/navs` (`communityMenu`) |
| Buttons | `src/components/CallToAction` (orange, pressable) |

## How I'd ship it

Small first, so it can merge. The rest follows if there's appetite. (Rank badges are kept out of the topic list on purpose, see Bet 2 in the README.)

### PR 1: voice and framing (smallest, safest, pure copy and nav)

- "Ask a question" becomes "Start a discussion." "Questions" becomes "Community discussions."
- Reorder `communityMenu` so community boards lead and product topics group under "Product talk."
- Add the gentle "this is a community, not a support queue, support's over there" pointer.
- No backend, no new data, no schema. Copy and nav order only. Keep `npm run build` green.

### PR 2: category grouping

- Group the question list under category bars (community and product) instead of one flat list, in PostHog's current look.
- Presentational only. It reads from the topics that already exist.

### PR 3: contributor spotlight ("Top hogs")

- A small module surfacing top contributors by their existing points and levels (`getLevel.ts`): name, rank, points. It uses data that's already there, no new fields.

## PostHog-native touches (worth doing, and a good sign of fit)

- Gate it behind a PostHog feature flag, so it can be rolled out or turned off remotely.
- Instrument the key events (a discussion started, a spotlight clicked). Using PostHog's own product to measure community work feels right for this.

## Open questions for the maintainers

- Appetite for the voice shift from support desk to community. Worth confirming before the copy PR.
- Where "Top hogs" should live: on /questions, on a /community surface, or tied to profiles.
