# DRAFT — GitHub Discussion post for PostHog/posthog.com

> Draft for review. Nothing is posted until you say so. Edit freely — it's in your voice.
> Suggested category: **Ideas / Meta** (or wherever the maintainers steer proposals).

---

**Title:** Could `/questions` feel more like a community and less like a support desk?

---

Hi 👋 — I'm an active PostHog user and I spend a fair bit of time in the forum. I want to float an idea about `/questions`, and I've built a clickable concept to make it concrete rather than just talk.

**The thing I keep noticing:** the forum is framed like a support queue. You **"Ask a question,"** threads carry statuses like *needs-response*, and product topics lead. That's great for triage — but the dev communities that really stick (the old phpBB/ProBoards boards, some of today's Discords) feel like a *place*: you recognise people, you wander in to talk, you belong. Right now the community side of `/questions` is doing a lot of quiet work under a support-desk frame.

**Two small bets to shift that — both frontend-only, no schema changes:**

1. **Grow the conversation.** Soften the voice from triage to talk (`"Ask a question" → "Start a discussion"`), and put community boards up top with product topics grouped under "Product talk." Nothing gets hidden — the ordering just says "this is a place to talk," and product help is one glance down.

2. **Spotlight the people.** Here's the fun part: PostHog *already ships* a contributor level ladder — `Hoglet → Hogthusiast → PowerHog → TopHog → ElderHog → Hogfather` (`src/components/Squeak/util/getLevel.ts`). It renders inside a thread as e.g. `PowerHog · 142`, but you'd never notice it. A small **"Top hogs"** spotlight would surface that ladder so contributors actually get *seen* — using data that already exists.

**I did some reading first.** From existing threads (#7961 on surfacing solved support Qs into the forum, #7960 on a points incentive) it's clear the forum was created to *surface solved answers publicly*, and that a reputation/points idea has already been on your minds. This proposal builds on that, not against it — the level ladder in bet 2 is exactly the kind of incentive #7960 gestured at, just made visible.

**The part I want to be upfront about:** `/questions` is also a real support channel, and I'm not proposing to break that — surfacing solved answers stays the point. If anything, the concept makes support's door *clearer* — a "chatting through a bug is welcome here, but if you just need it fixed, support's over there →" pointer — so the community and support intents stop competing for the same frame.

**See it:** [prototype link] — a clickable concept built on PostHog's *real* design (the PostHog OS window, your palette, the actual level colours). There's a "highlight what changed" toggle so you can see exactly what's touched vs. the live page. It leans into a bit of old-forum nostalgia (category bars, "last post ↪", a "who's browsing" footer), kept in the current skin. *(All names, posts, and points in it are fictional sample data.)*

**If there's appetite, I'd start tiny:** a copy + nav PR (the rename + community-first ordering + the support pointer). Pure frontend, easy to review. The bolder pieces (board grouping, the Top Hogs spotlight) could follow as separate PRs, only if you want them.

Mostly I want to ask: **is this a direction you'd welcome?** And what am I missing about how you think about `/questions` today? Happy to do the work — just want to build the right thing *with* you rather than lob a big PR over the wall.

---

### Hosting the prototype link
The prototype is a single self-contained HTML file (`prototype/community-redesign.html`). To give it a public URL for the post, easiest options:
- Enable **GitHub Pages** on this repo and link the file, or
- Drop it on any static host (Netlify drop, Cloudflare Pages, etc.).
Replace `[prototype link]` above once it's live.
