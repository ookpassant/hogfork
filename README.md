# hogfork

A little workspace for reimagining the PostHog community forum ([posthog.com/questions](https://posthog.com/questions)).

The idea is simple. Move it from feeling like a support desk toward feeling like a community, and turn that into a real contribution back to [PostHog/posthog.com](https://github.com/PostHog/posthog.com).

I kept this separate from my other work on purpose. It holds the design concept, the thinking, and the previews. The actual code change lives on a fork and is now an open pull request.

## The PR (open)

A small, frontend-only pass on `/questions`. Two files (`src/components/Inbox/index.tsx`, `src/navs/useTopicsNav.js`). No backend, schema, or data changes.

**[PostHog/posthog.com#18683](https://github.com/PostHog/posthog.com/pull/18683)** (draft)

- "Ask a question" becomes "Start a discussion": the sidebar button, the ask-window title, and the form's submit button (a local `buttonText` so the shared form on other pages is untouched).
- The forum index title "Forums" becomes "Community discussions." Topic and question pages keep their own titles.
- Community topics lead the sidebar: the group holding #introductions, #where-in-the-world and #devrel is reordered to the top and shown as "Community." Sorting still keys off the raw Strapi label, so the CMS is unchanged.
- A support pointer in the sidebar footer: chatting through a bug is welcome, but if you just need it fixed it links to /talk-to-a-human, with a nudge that a quick search may beat a new post.

## The bigger vision (not in the PR)

The prototype and previews gesture at where this could go. These need a maintainer's call, so they are deliberately out of the copy PR:

- **New community boards** (#build-in-public, #war-stories, #the-lounge). New Squeak topics that someone has to create in the CMS. (#devrel is a real board too, but reads a bit niche up front, so retiring or folding it in is worth a look.)
- **Spotlight the people.** PostHog already ships a hidden contributor level ladder: Hoglet, Hogthusiast, PowerHog, TopHog, ElderHog, Hogfather (`src/components/Squeak/util/getLevel.ts`). A "Top hogs" spotlight would bring it into view, using points that already exist.

## See it

Live preview site: **https://ookpassant.github.io/hogfork/**

- **The PR, on the real design** — the shipping change applied to posthog.com's actual forum page.
- **The bigger wishlist** — the same, plus the proposed new boards.
- **A ProBoards wildcard** — the whole forum reskinned as a navigable 2004-era board, just for fun.

Everything on the preview site is a prototype with made-up sample content, clearly flagged as not the real posthog.com.

## Building the real change

The fork builds with pnpm (Node 22): `pnpm install && pnpm start` for dev, `pnpm build:minimal` for a quick build check. The copy and nav change typechecks clean (`tsc`) and lints clean (`eslint`) on the two files, and the branch is rebased on current upstream master so it merges without conflicts.

## Status

- [x] Explore the real forum and its Squeak components
- [x] Concept prototype and previews on the real PostHog OS layout
- [x] Build the copy and nav change on a fork, verify it typechecks and lints
- [x] Open the PR (draft): [#18683](https://github.com/PostHog/posthog.com/pull/18683)
- [ ] A maintainer approves the workflows so CI and the Vercel preview run
- [ ] Add before/after screenshots, then flip the PR from draft to ready for review

The plan, the PR draft, and the discussion notes live under [`docs/`](docs/) on the `community-redesign` branch.
