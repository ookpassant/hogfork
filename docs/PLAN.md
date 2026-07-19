# Plan: from concept to contribution

This maps the concept to real posthog.com code and lays out the order to ship
it. Paths are from PostHog/posthog.com (Gatsby, React, Tailwind), verified
against the fork at `master` (commit `5084134`). The forum runs on their
"Squeak" Q&A engine, with data from a Strapi backend.

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
   reviewable, `pnpm build:minimal` stays green. Merge what lands, drop what
   doesn't.

## Local dev and verification

From the handbook (developing-the-website):

- **pnpm 10.x, Node 22.x.**
- Dev server: `pnpm install && pnpm start`. The first run is slow ("Building
  development bundle" takes a few minutes).
- Quick build check: `pnpm build:minimal`.
- **Runs without secrets.** Missing env vars (GitHub contributors, Ashby, and
  so on) throw errors that are "dismissible, and you can continue to edit the
  website." So a copy or nav change can be verified locally without their
  backend. What we cannot verify locally is the forum rendering with real data,
  since that comes from Strapi. For the look, the prototype stands in.
- Verification bar per PR: `pnpm start` renders the changed component, and
  `pnpm build:minimal` compiles clean. Ask in #posthogdotcom only if a change
  actually needs a real env var.

## Where things live

| Area | Real file(s) |
| --- | --- |
| `/questions` "Ask a question" CTA | `src/components/Inbox/index.tsx`: the sidebar button (L127), the ask-window title (L395), and the form's submit button via a local `buttonText` prop on `QuestionForm` (L400). Inbox renders the Squeak `QuestionForm` (import L8) with no override, so the shared default lives at `src/components/Squeak/components/QuestionForm.tsx:323` and is best left alone to avoid touching other surfaces |
| Window title "Questions" | Not a plain string. Comes from the page's meta/SEO title (`AppWindow` strips `- PostHog`, ~L775); `src/pages/questions/index.tsx` returns `null` and the OS layer injects the app. Changing it is a metadata change, so it is its own PR |
| Sidebar topic order | `src/navs/useTopicsNav.js`: the `navSorted` array (L7) sets group order; "Latest" is L27. NOT `communityMenu` (that is the site's Community nav). Group labels and topic membership come from Strapi (`allSqueakTopicGroup`) |
| Question list rows | `src/components/Questions/QuestionsTable.tsx`, `src/components/Questions/TopicsTable.tsx` |
| Level ladder and badge | `src/components/Squeak/util/getLevel.ts` (Hoglet 10 to Hogfather 750, confirmed), `src/components/Squeak/components/LevelBadge.tsx` |
| Buttons | `OSButton` (used in Inbox); `src/components/CallToAction` for the orange pressable style |

## The PRs

Each one stands alone. A maintainer can take the copy change without the nav
change, or stop after PR2. That is the point of splitting them.

### PR 1: the ask CTA copy (smallest, safest)

- "Ask a question" becomes "Start a discussion" on the `/questions` surface:
  the sidebar button, the ask-window title, and the form's submit button.
- All three live in `src/components/Inbox/index.tsx`, and the submit button is a
  local `buttonText` override so the shared `QuestionForm` default (used on other
  surfaces) is untouched. One file, zero ripple.
- The "Questions" to "Community discussions" window title is NOT in here. It is
  a page-metadata change (see the table), so it ships as its own small PR.

### PR 2: group the existing topics

- Under the sidebar, put the community group first: reorder the `navSorted`
  array in `src/navs/useTopicsNav.js` so the group holding the community boards
  (`#introductions`, `#where-in-the-world`, `#devrel`) leads.
- Reorder only, frontend, no schema. This is the part that is genuinely a diff.
- Renaming the group to "Community" and grouping product topics under "Product
  talk" is a **Strapi** change (group labels and membership are backend data),
  so it moves to "Needs your input first" below, not this PR.

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
- **Renaming topic groups** ("Off-topic" to "Community", product topics under
  "Product talk"). The group labels and which topics belong to them are Strapi
  data, not frontend. The frontend can only reorder them (PR 2). Renaming is a
  CMS edit on their side.
- **Feature-flag gating.** Roll the change out or turn it off remotely with
  PostHog's own flags. Worth doing, needs a flag set up on their side.
- **Event instrumentation.** Track a discussion started, a spotlight clicked.
  Using PostHog to measure community work fits, but it is added scope.

## Prototype vs what is actually proposed

The prototype leans into old-forum nostalgia to sell the feeling. Not all of it
is on the table for merge. This keeps that honest.

| In the prototype | Maps to | Status |
| --- | --- | --- |
| "Start a discussion" ask CTA | PR 1 | Proposed |
| "Community discussions" window title | own PR | Proposed (page metadata) |
| Community-first sidebar order | PR 2 | Proposed (reorder only; rename needs Strapi) |
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
