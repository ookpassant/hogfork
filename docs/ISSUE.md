# DRAFT: tracking issue for PostHog/posthog.com

> Open this once the direction has a nod (or alongside PR 1 if you'd rather just
> ship and talk). It keeps the scope in one place and lets each PR close a box.

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

### Ships now (frontend only, each its own PR)

- [ ] **Copy:** "Ask a question" to "Start a discussion"; window title
  "Questions" to "Community discussions". (`QuestionForm.tsx` x2) [PR link]
- [ ] **Grouping:** existing topics grouped, community boards
  (#introductions, #where-in-the-world, #devrel) lead under "Community",
  product topics under "Product talk". Reorder only. (`communityMenu` / `Sidebar`)
- [ ] **Support pointer:** a "chat a bug here, but for a fix support's over
  there" line, plus a nudge to search existing discussions first. (copy)
- [ ] **Category grouping** in the question list, presentational. (`QuestionsTable.tsx`)
- [ ] **"Top hogs" spotlight:** top contributors by existing points and levels.
  (`getLevel.ts`)

### Needs a maintainer call first (not frontend only)

- [ ] **New community boards** (#build-in-public, #war-stories, #the-pub): new
  Squeak topics to create and moderate. No schema change, but your call on
  names and whether you want them at all.
- [ ] **Feature-flag gate** so it can be rolled out or turned off remotely.
- [ ] **Event instrumentation** (discussion started, spotlight clicked).

### Notes

- Each "ships now" box is a standalone PR. Merge or close them independently.
- `npm run build` stays green on every PR.
