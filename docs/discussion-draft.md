# DRAFT: GitHub Discussion post for PostHog/posthog.com

> A draft for review. Nothing gets posted until you say so. Edit it freely, it's your voice.
> Suggested category: Ideas or Meta (or wherever the maintainers like proposals to go).

---

**Title:** Could /questions feel more like a community and less like a support desk?

---

Hi. I'm an active PostHog user and I spend a fair bit of time in the forum. I want to float an idea about /questions, and I've built a clickable concept so it's something you can look at rather than just read about.

The thing I keep noticing is that the forum is framed like a support queue. You "Ask a question," threads carry statuses like needs-response, and product topics lead. That's great for triage. But the dev communities that really stick, the old phpBB and ProBoards boards, some of today's Discords, feel like a place. You recognise people, you wander in to talk, you belong. Right now the community side of /questions is doing a lot of quiet work under a support-desk frame.

Two small bets could shift that, and both are frontend only, no schema changes:

1. Grow the conversation. Soften the voice from triage to talk ("Ask a question" becomes "Start a discussion"), and put community boards up top with product topics grouped under "Product talk." Nothing gets hidden. The ordering just says this is a place to talk, and product help is one glance down.

2. Spotlight the people. Here's the fun part. PostHog already ships a contributor level ladder: Hoglet, Hogthusiast, PowerHog, TopHog, ElderHog, Hogfather (`src/components/Squeak/util/getLevel.ts`). It renders inside a thread, but you'd never really notice it. A small "Top hogs" spotlight would bring that ladder into view so the people who help actually get seen, using data that already exists.

I did some reading first. From the existing threads (#7961 on surfacing solved support questions into the forum, #7960 on a points incentive) it's clear the forum was built to surface solved answers publicly, and that a reputation idea has already been on your minds. This builds on that, not against it. The level ladder in bet 2 is exactly the kind of incentive #7960 was reaching for, just made visible.

One thing I want to be upfront about. /questions is also a real support channel, and I'm not proposing to break that. Surfacing solved answers stays the point. If anything, the concept makes support's door clearer, with a "chatting through a bug is welcome here, but if you just need it fixed, support's over there" pointer, so the community and support intents stop competing for the same frame.

See it: [prototype link]. It's a clickable concept built on PostHog's real design (the PostHog OS window, your palette, the actual level colours). There's a "highlight what changed" toggle so you can see exactly what's touched against the live page. It leans into a bit of old-forum nostalgia (category bars, a "last post" jump arrow, a "who's browsing" footer), kept in the current look. All names, posts, and points in it are made-up sample data.

If there's appetite, I'd start tiny: a copy and nav PR (the rename, the community-first ordering, the support pointer). Pure frontend, easy to review. The bolder pieces (the category grouping, the Top hogs spotlight) could follow as separate PRs, only if you want them.

Mostly I want to ask: is this a direction you'd welcome? And what am I missing about how you think about /questions today? I'm happy to do the work. I'd just rather build the right thing with you than lob a big PR over the wall.

---

### Hosting the prototype link

The prototype is a single self-contained HTML file (`prototype/community-redesign.html`). To give it a public URL for the post, the easiest options are:

- Enable GitHub Pages on this repo and link the file, or
- Drop it on any static host (Netlify drop, Cloudflare Pages, and so on).

Replace `[prototype link]` above once it's live.
