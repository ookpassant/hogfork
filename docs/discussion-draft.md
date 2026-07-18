# DRAFT: GitHub Discussion post for PostHog/posthog.com

> A draft for review. Nothing gets posted until you say so. Edit it freely, it's your voice.
> Suggested category: Ideas or Meta (or wherever the maintainers like proposals to go).
> Before posting: verify the issue references in the "did some reading" paragraph (see docs/PLAN.md).

---

**Title:** Could /questions feel more like a community and less like a support desk?

---

Hi. I'm an active PostHog user and I spend a fair bit of time in the forum. I want to float an idea about /questions, and I've built a clickable concept so it's something you can look at rather than just read about.

The thing I keep noticing is that the forum is framed like a support queue. You "Ask a question," threads carry statuses like needs-response, and product topics lead. That's great for triage. But the dev communities that really stick, the old phpBB and ProBoards boards, some of today's Discords, feel like a place. You recognise people, you wander in to talk, you belong. Right now the community side of /questions is doing a lot of quiet work under a support-desk frame.

Two small bets could shift that:

1. Grow the conversation. Soften the voice from triage to talk ("Ask a question" becomes "Start a discussion"), and put community boards up top with product topics grouped under "Product talk." Nothing gets hidden. The ordering just says this is a place to talk, and product help is one glance down. The boards you already have (#introductions, #where-in-the-world, #devrel) can lead as-is. A few more community-flavoured boards (#build-in-public, #war-stories, #the-pub) would give people more reasons to hang around, though those would be new topics to set up on your side, so they are a suggestion, not something I'd just open a PR for.

2. Spotlight the people. Here's the fun part. PostHog already ships a contributor level ladder: Hoglet, Hogthusiast, PowerHog, TopHog, ElderHog, Hogfather (`src/components/Squeak/util/getLevel.ts`). It renders inside a thread, but you'd never really notice it. A small "Top hogs" spotlight would bring that ladder into view so the people who help actually get seen, using data that already exists.

I did some reading first. From the existing threads (#7961 on surfacing solved support questions into the forum, #7960 on a points incentive) it's clear the forum was built to surface solved answers publicly, and that a reputation idea has already been on your minds. This builds on that, not against it. The level ladder in bet 2 is exactly the kind of incentive #7960 was reaching for, just made visible.

One thing I want to be upfront about. /questions is also a real support channel, and surfacing solved bugs and answered questions publicly is a big part of what it's for. I'm not proposing to touch that. If anything the concept leans into it: the topic search stays right where it is, so before someone starts a new thread they can find the discussion or the solved answer that already covers it. And support gets a clearer door, with a "chatting through a bug is welcome here, but if you just need it fixed, support's over there" pointer, so the community and support intents stop competing for the same frame.

See it: [prototype link]. It's a clickable concept built on PostHog's real design (the PostHog OS window, your palette, the actual level colours). There's a "highlight what changed" toggle so you can see exactly what's touched against the live page. It leans into a bit of old-forum nostalgia (category bars, a "last post" jump arrow, a "who's browsing" footer), kept in the current look. Some of that is just flavour to show the feeling, not all of it is something I'd ask you to merge. All names, posts, and points in it are made-up sample data.

In the spirit of shipping rather than asking permission, I've gone ahead and opened the smallest piece already: [PR link], the copy change (the rename). It's a one-line-to-revert edit, so it felt sillier to write a paragraph about it than to just do it. Everything else stays tiny and separate: the community-first grouping of your existing topics, then the support pointer, each easy to review and easy to say no to. The bolder pieces (the category grouping, the Top hogs spotlight) follow only if you want them. I'll open a tracking issue so it's all in one place.

So really this is two things: a PR you can merge or close today, and a question. Is this a direction you'd welcome, and what am I missing about how you think about /questions? Happy to keep shipping the small stuff and shape the bigger stuff with you.

---

### Hosting the prototype link

The prototype is a single self-contained HTML file (`prototype/community-redesign.html`). To give it a public URL for the post, the easiest options are:

- Enable GitHub Pages on this repo and link the file, or
- Drop it on any static host (Netlify drop, Cloudflare Pages, and so on).

Replace `[prototype link]` above once it's live.
