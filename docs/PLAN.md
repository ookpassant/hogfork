# Plan: from concept to contribution

This maps the concept to real posthog.com code and lays out the order to ship
it. Paths are from PostHog/posthog.com (Gatsby, React, Tailwind). The forum
runs on their "Squeak" Q&A engine, with data from a Strapi backend.

## The flow

PostHog bias is to ship, so lead with something shipped, not with a request for
permission. The smallest change is a copy edit that reverts in one line, so it
goes out as a real PR on day one. The talking happens next to it, not before it.

1. **Ship PR 1 first.** Open the copy PR (below) straight away. It is trivial,
   reversible, and shows the intent better than any paragraph. Link the
   prototype in the PR description.
2. **Discussion (Ideas category), in parallel.** Carry the bigger direction:
   the grouping, the spotlight, the new boards. Point at the already-open PR 1
   as the concrete first step. Draft in [`discussion-draft.md`](discussion-draft.md).
3. **Tracking issue for the rest.** Open the issue in [`ISSUE.md`](ISSUE.md) so
   the agreed scope lives in one place. Each PR below closes one checkbox.
4. **Ship the rest as small PRs from a fork.** Atomic, independently
   reviewable, `npm run build` stays green. Merge what lands, drop what doesn't.

## Where things live

| Area | Real file(s) |
| --- | --- |
| "Ask a question" copy | `src/components/Squeak/components/QuestionForm.tsx` (~L323), `src/components/Questions/QuestionForm.tsx` (label default ~L33) |
| Question list rows | `src/components/Questions/QuestionsTable.tsx` (the `Row`), `src/components/Squeak/components/Questions.tsx` |
| Level ladder and badge | `src/components/Squeak/util/getLevel.ts`, `src/components/Squeak/components/LevelBadge.tsx` |
| Community sidebar and topic order | `src/components/Community/Sidebar` and `src/navs` (`communityMenu`) |
| Buttons | `src/components/CallToAction` (orange, pressable) |

## The PRs

Each one stands alone. A maintainer can take the copy change without the nav
change, or stop after PR2. That is the point of splitting them.

### PR 1: copy only (smallest, safest)

- "Ask a question" becomes "Start a discussion."
- The window title "Questions" becomes "Community discussions."
- Nothing else. Pure string changes in the two form files above.

### PR 2: group the existing topics

- Under the sidebar, group the topics that already exist: the three community
  boards (`#introductions`, `#where-in-the-world`, `#devrel`) lead under a
  "Community" heading, product topics group under "Product talk."
- Reorder and heading only, in `communityMenu` / `Sidebar`. No new boards, no
  data, no schema.

### PR 3: the support pointer

- A gentle line: chatting through a bug is welcome here, but if you just need
  it fixed, support lives over there.
- Paired with the honest other half: the forum also surfaces solved bugs and
  answered questions, so search is worth a look before starting a new thread.
  This keeps the forum's real job (public, searchable answers) front and
  centre instead of hiding it. Copy plus a link to the topic search that is
  already in the sidebar.

### PR 4: category grouping in the list

- Group the question list under category bars (community and product) instead
  of one flat list, in PostHog's current look.
- Presentational only. Reads from the topics that already exist.

### PR 5: contributor spotlight ("Top hogs")

- A small module surfacing top contributors by their existing points and
  levels (`getLevel.ts`): name, rank, points. Data that is already there, no
  new fields.

## Needs your input first (not in the PRs above)

These are in the vision and the prototype, but they are not frontend-only, so
they do not ride along in a "just copy and nav" PR. They need a maintainer
decision before any code.

- **New community boards** (`#build-in-public`, `#war-stories`, `#the-pub`).
  No schema change, but they are new Squeak topics that someone has to create
  in the CMS, name, and agree to moderate. That is a product call, not a diff.
  Proposed in the Discussion, built only if wanted.
- **Feature-flag gating.** Roll the change out or turn it off remotely with
  PostHog's own flags. Worth doing, needs a flag set up on their side.
- **Event instrumentation.** Track a discussion started, a spotlight clicked.
  Using PostHog to measure community work fits, but it is added scope.

## Prototype vs what is actually proposed

The prototype leans into old-forum nostalgia to sell the feeling. Not all of it
is on the table for merge. This keeps that honest.

| In the prototype | Maps to | Status |
| --- | --- | --- |
| "Start a discussion", "Community discussions" | PR 1 | Proposed |
| Community-first sidebar grouping | PR 2 | Proposed (existing boards only) |
| Support pointer + search note | PR 3 | Proposed |
| Category bars in the list | PR 4 | Proposed |
| "Top hogs this week" | PR 5 | Proposed |
| `#build-in-public`, `#war-stories`, `#the-pub` | Needs input | Illustrative until agreed |
| "Last post" jump arrow, "who's browsing" footer | none yet | Illustrative flavour, not proposed |

## Before anything goes public

- **Verify the referenced threads.** The draft cites prior forum issues
  (`#7960`, `#7961`). posthog.com is outside this workspace, so confirm on
  GitHub that those numbers exist and say what the draft claims before posting.
  A proposal that misquotes the maintainers' own threads loses trust fast.
