# DRAFT: pull request for PostHog/posthog.com

> Draft only. Nothing is opened until you say so. Branch: `community/forum-refresh`
> on the fork (`ookpassant/posthog.com`), base `PostHog:master`.
> Body mirrors the repo's `.github/pull_request_template.md`.

---

**Title:** Community: soften /questions from support desk toward community (copy + nav)

---

## Changes

A small, frontend-only pass to make /questions read a bit more like a community
and less like a support queue. No backend, schema, or data changes. Copy and nav
order only. Two files, `src/components/Inbox/index.tsx` and
`src/navs/useTopicsNav.js`.

- **Reframe the ask CTA.** "Ask a question" becomes "Start a discussion": the
  sidebar button, the window title when the form opens, and the form's submit
  button (a local `buttonText` so the shared `QuestionForm` used on other
  surfaces is untouched).
- **Title the forum window "Community discussions."** The /questions index title
  (`'Forums'`) becomes "Community discussions." Topic and question pages keep
  their own titles.
- **Lead the sidebar with the community group.** Reorder the topic-group nav so
  the group holding #introductions, #where-in-the-world and #devrel comes first,
  shown as "Community." Sorting still keys off the raw Strapi label, so the CMS
  group is unchanged.
- **Add a support pointer.** A small sidebar footer: chatting through a bug is
  welcome here, but if you just need it fixed it links to /talk-to-a-human.
  Paired with a nudge that a lot of questions already have answers, so search may
  beat a new post. This keeps solved answers easy to find and stops the community
  and support intents from competing for the same frame.

Context: this comes with a clickable concept and a short write-up. [prototype
link]. Happy to split any of these out or drop them.

*Screenshots: the changes are copy and nav on the existing PostHog OS forum
layout. The prototype above shows the intended feel with a "highlight what
changed" toggle. I can add real screenshots from the Vercel preview once this is
open.*

## Checklist

- [x] I've read the [docs](https://posthog.com/handbook/wizard-and-docs/docs-style-guide) and/or [content](https://posthog.com/handbook/content/posthog-style-guide) style guides.
- [x] Words are spelled using American English
- [x] Use relative URLs for internal links
- [ ] I've checked the pages added or changed in the Vercel preview build (will do once the PR is open, since the preview builds on PR)
- [ ] If I moved a page, I added a redirect in `vercel.json` (N/A, no pages moved)
