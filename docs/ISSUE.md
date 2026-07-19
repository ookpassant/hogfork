# DRAFT: tracking issue for PostHog/posthog.com

> Open this once the direction has a nod (or alongside the forum-refresh PR if
> you'd rather just ship and talk). It keeps the scope in one place.

---

**Title:** Community-first pass on /questions: copy, grouping, contributor spotlight

**Labels (suggest):** community, enhancement, good first issue candidate

---

Making /questions feel more like a community and less like a support desk, in
small reviewable steps. Background and the "why" are in the Discussion: [link].
Clickable concept: [prototype link]. All of this is frontend unless flagged.

The forum's job of surfacing solved bugs and answered questions stays intact.
None of this hides existing answers or touches the support flow; the topic
search stays put so people can find what already exists.

### The forum-refresh PR (branch `community/forum-refresh`, one PR) [PR link]

Frontend only, two files (`Inbox/index.tsx`, `useTopicsNav.js`), four commits:

- [ ] **Ask CTA:** "Ask a question" to "Start a discussion" (button, ask-window
  title, and the form submit via a local `buttonText` override).
- [ ] **Forum window title:** the /questions index title "Forums" to "Community
  discussions" (`Inbox/index.tsx:563`).
- [ ] **Sidebar order + label:** the community group (#introductions,
  #where-in-the-world, #devrel) leads, shown as "Community" via a frontend
  display override. Reorder + relabel only; the Strapi group is unchanged.
- [ ] **Support pointer:** a "chat a bug here, but for a fix talk to a human"
  footer, plus a nudge to search first.

### Bigger, as their own PRs later

- [ ] **Category grouping** in the question list, presentational. (`QuestionsTable.tsx`)
- [ ] **"Top hogs" spotlight:** top contributors by existing points and levels.
  (`getLevel.ts`)

### Needs a maintainer call first (not frontend only)

- [ ] **New community boards** (#build-in-public, #war-stories, #the-lounge): new
  Squeak topics to create and moderate. No schema change, but your call on
  names and whether you want them at all.
- [ ] **Retire #devrel** (or fold it in). It is a real board, so the reorder PR
  still shows it under "Community"; removing or merging it is a Strapi action.
- [ ] **Feature-flag gate** so it can be rolled out or turned off remotely.
- [ ] **Event instrumentation** (discussion started, spotlight clicked).

### Notes

- The four boxes above ship as one PR (`community/forum-refresh`); the bigger two
  are separate PRs later.
- `pnpm build:minimal` stays green on every PR.
