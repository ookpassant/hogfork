# DRAFT: pull request for PostHog/posthog.com

> Draft only. Nothing is opened until you say so. Branch: `community/forum-refresh`
> on the fork (`ookpassant/posthog.com`), base `PostHog:master`.
> Body mirrors the repo's `.github/pull_request_template.md`.

---

**Title:** Make /questions read more like a community, less like a support desk

---

## Changes

Small frontend-only pass. Copy and nav order, two files (`src/components/Inbox/index.tsx`, `src/navs/useTopicsNav.js`). No backend, schema, or data changes.

- "Ask a question" → "Start a discussion" – sidebar button, window title on the form, and the submit button. Uses a local `buttonText` so the shared `QuestionForm` on docs pages is untouched.
- Forum window title "Forums" → "Community discussions" – index only. Topic and question pages keep their own titles.
- Community topics first – reordered the topic-group nav so the group holding #introductions, #where-in-the-world, and #devrel leads, shown as "Community." Sorting still keys off the raw Strapi label, so nothing changes in the CMS.
- Support pointer in the sidebar footer – chatting through a bug is welcome here, but if you just need it fixed → /talk-to-a-human. Plus a nudge that search might beat a new post, since a lot of questions already have answers.

Why: the handbook says community ≠ support, but /questions currently asks people to... ask a question. This smells like support. This is the smallest move toward shifting that – see a clickable (kinda) concept of where it could go, see new boards! See moved topics! Note the support topic at the bottom of the board list! https://ookpassant.github.io/hogfork/

(There's also a wildcard in there where I reskinned the whole forum as an old-school ProBoards board – 2004 forum energy, folder icons, fully clickable through boards and threads. Purely for fun... but honestly, kind of on theme? Have a click.)

Happy to split any of these four out, or drop them.

## Screenshots

Copy + nav on the existing layout – will add before/after from the Vercel preview once it builds.

## Checklist

- [x] I've read the [docs](https://posthog.com/handbook/wizard-and-docs/docs-style-guide) / [content](https://posthog.com/handbook/content/posthog-style-guide) style guides
- [x] Words are spelled using American English
- [x] Relative URLs for internal links
- [ ] Checked the changed pages in the Vercel preview build (will do once it builds on open)
- [ ] N/A – no pages moved, no redirects needed
