# Plan: from concept to contribution

This maps the concept to real posthog.com code and lays out the order to ship
it. Paths are from PostHog/posthog.com (Gatsby, React, Tailwind), verified
against the fork at `master` (commit `5084134`). The forum runs on their
"Squeak" Q&A engine, with data from a Strapi backend.

## The flow

PostHog bias is to ship, so the work is built and verified first, then talked
about next to it, not before it.

1. **One "forum refresh" PR.** The voice-and-framing changes below are small,
   frontend-only, and cohesive, so they ship together as a single reviewable PR
   from the fork (branch `community/forum-refresh`), not four separate ones. Each
   change is its own commit so the history still reads as clear steps. Draft body
   in [`pr-forum-refresh.md`](pr-forum-refresh.md). Link the prototype in it.
2. **Discussion (Ideas category), alongside it.** Carry the bigger direction: the
   spotlight, the new boards, the category grouping. Point at the PR as the
   concrete first step. Draft in [`discussion-draft.md`](discussion-draft.md).
3. **Tracking issue.** Open the issue in [`ISSUE.md`](ISSUE.md) so the agreed
   scope lives in one place.
4. **The bigger pieces follow as their own PRs** (category grouping, Top hogs),
   only if wanted. `pnpm build:minimal` stays green throughout.

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
| Forum window title | Comes from the page's SEO title via `setWindowTitle` (`AppWindow` strips `- PostHog`, ~L775). The `/questions` index has no "Questions" string: Inbox's `<SEO>` resolves it to the `'Forums'` fallback (`src/components/Inbox/index.tsx:563`), so swapping that literal for "Community discussions" retitles the index window, browser tab, and OG title. Topic and question pages keep their own titles. (Earlier the plan guessed "Questions" / page metadata; the real source is this one line.) |
| Sidebar topic order | `src/navs/useTopicsNav.js`: the `navSorted` array (L7) sets group order; "Latest" is L27. NOT `communityMenu` (that is the site's Community nav). Group labels and topic membership come from Strapi (`allSqueakTopicGroup`) |
| Question list rows | `src/components/Questions/QuestionsTable.tsx`, `src/components/Questions/TopicsTable.tsx` |
| Level ladder and badge | `src/components/Squeak/util/getLevel.ts` (Hoglet 10 to Hogfather 750, confirmed), `src/components/Squeak/components/LevelBadge.tsx` |
| Buttons | `OSButton` (used in Inbox); `src/components/CallToAction` for the orange pressable style |

## The forum-refresh PR (branch `community/forum-refresh`)

Four small changes, two files (`Inbox/index.tsx`, `useTopicsNav.js`), shipped as
one PR. Each is its own commit, so the history still reads as clear steps. Built
and verified on the fork; not opened yet. Draft body in
[`pr-forum-refresh.md`](pr-forum-refresh.md).

- **Ask CTA.** "Ask a question" becomes "Start a discussion": the sidebar button,
  the ask-window title, and the form's submit button (a local `buttonText` on
  `QuestionForm` so the shared default, used on other surfaces, is untouched).
- **Forum window title.** The `/questions` index title `'Forums'` becomes
  "Community discussions" (`Inbox/index.tsx:563`). Topic and question pages keep
  their own titles.
- **Sidebar order + label.** Reorder `navSorted` in `useTopicsNav.js` so the
  group holding the community boards (`#introductions`, `#where-in-the-world`,
  `#devrel`) leads, shown as "Community" via a frontend display override. Sorting
  still keys off the raw Strapi label, so the CMS group is unchanged.
- **Support pointer.** A small sidebar footer: chatting through a bug is welcome,
  but if you just need it fixed it links to `/talk-to-a-human`, plus a nudge that
  many questions already have answers so search may beat a new post.

## The bigger PRs (later, if wanted)

### Category grouping in the list

- Group the question list under category bars (community and product) instead of
  one flat list, in PostHog's current look. Presentational only.

### Contributor spotlight ("Top hogs")

- A small module surfacing top contributors by their existing points and levels
  (`getLevel.ts`): name, rank, points. Data that is already there, no new fields.

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
  data, not frontend. The frontend can only reorder them and relabel the display
  name (both in the forum-refresh PR). Renaming the group in the CMS is on their
  side. Grouping product topics under a single "Product talk" heading also needs
  Strapi, since it merges several existing groups.
- **Feature-flag gating.** Roll the change out or turn it off remotely with
  PostHog's own flags. Worth doing, needs a flag set up on their side.
- **Event instrumentation.** Track a discussion started, a spotlight clicked.
  Using PostHog to measure community work fits, but it is added scope.

## Prototype vs what is actually proposed

The prototype leans into old-forum nostalgia to sell the feeling. Not all of it
is on the table for merge. This keeps that honest.

| In the prototype | Maps to | Status |
| --- | --- | --- |
| "Start a discussion" ask CTA | forum-refresh PR | Built on branch |
| "Community discussions" window title | forum-refresh PR | Built on branch |
| Community-first sidebar order + "Community" label | forum-refresh PR | Built on branch |
| Support pointer + search note | forum-refresh PR | Built on branch |
| Category bars in the list | later PR | Proposed |
| "Top hogs this week" | later PR | Proposed |
| `#build-in-public`, `#war-stories`, `#the-pub` | Needs input | Illustrative until agreed |
| "Last post" jump arrow, "who's browsing" footer | none yet | Illustrative flavour, not proposed |

## Before anything goes public

- **Verify the referenced threads.** The draft cites prior forum issues
  (`#7960`, `#7961`). posthog.com is outside this workspace, so confirm on
  GitHub that those numbers exist and say what the draft claims before posting.
  A proposal that misquotes the maintainers' own threads loses trust fast.
