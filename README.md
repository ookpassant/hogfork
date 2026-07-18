# hogfork

A little workspace for reimagining the PostHog community forum ([posthog.com/questions](https://posthog.com/questions)).

The idea is simple. Move it from feeling like a support desk toward feeling like a community, and turn that into a real contribution back to [PostHog/posthog.com](https://github.com/PostHog/posthog.com).

I kept this separate from my other work on purpose. It holds the design concept, the thinking behind it, and the draft changes. The actual pull request will come from a proper fork of posthog.com, since GitHub only lets you open one between a fork and its upstream.

## The idea

Right now the forum is framed like a helpdesk. You "Ask a question," threads carry statuses like needs-response, and product topics lead. That works for triage. But the communities that really stick feel like a place you belong to, and that's the part I want to bring forward. Two small moves do most of the work, and neither one needs a backend change.

### Bet 1: grow the conversation

Soften the voice from triage to talk, and make it clear this is a community, not a support queue.

- "Ask a question" becomes "Start a discussion." The window title "Questions" becomes "Community discussions."
- Community boards come first: #introductions, #build-in-public, #war-stories, #where-in-the-world, #the-pub. Product topics sit just below, under "Product talk."
- Support gets its own clear door. A gentle line saying that chatting through a bug is welcome, but if you just need it fixed, support lives over there. So the two intents stop competing for the same frame.

### Bet 2: spotlight the people

PostHog already ships a contributor level ladder. It's just hidden. Hoglet, Hogthusiast, PowerHog, TopHog, ElderHog, Hogfather (see `src/components/Squeak/util/getLevel.ts`). The badge shows up inside a thread, but nowhere you'd really notice.

- Rank stays out of the topic list, the way the old forums did it. Your rank lived under your avatar in a post, never in the index. Names stay clean.
- A "Top hogs this week" spotlight brings the ladder into view (name, rank, points) so the people who help actually get seen. It leans on points that already exist in the code.

### The look

I leaned on what made the early-2000s boards feel like a place, rebuilt in PostHog's current look (the PostHog OS window, the cream and orange, the real level colours). Coloured category bars, folder icons, a "last post" jump arrow, and a "who's browsing" footer.

## The prototype

[`prototype/community-redesign.html`](prototype/community-redesign.html) is a self-contained concept. Open it in a browser. There's a "highlight what changed" toggle so you can see exactly what's touched against the live page. Everything in it (names, posts, points) is made-up sample data.

## Status

- [x] Explore the real forum and its Squeak components
- [x] Concept prototype on the real PostHog OS layout
- [ ] Lock the scope (see [`docs/PLAN.md`](docs/PLAN.md))
- [ ] Fork posthog.com, build the diff, keep `npm run build` green
- [ ] Open the PR

See [`docs/PLAN.md`](docs/PLAN.md) for how each change maps to the real posthog.com code, and the order I'd ship them in.
