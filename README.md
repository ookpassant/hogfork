# hogfork

A workspace for reimagining the **PostHog community forum** ([posthog.com/questions](https://posthog.com/questions)) — moving it from *support desk* toward *community*, and turning that into a real contribution to [PostHog/posthog.com](https://github.com/PostHog/posthog.com).

This repo is deliberately separate from other projects. It holds the design concept, the rationale, and the draft changes. The actual pull request will be opened from a proper fork of `posthog.com` (GitHub only allows PRs between a fork and its upstream).

---

## The idea

The forum today is framed like a helpdesk: you **"Ask a question,"** posts carry statuses like *needs-response*, and product topics lead. But the thing that makes a community a *place* — people recognising each other, wandering in to talk, belonging — is underplayed. Two moves fix most of that, and neither needs a backend change.

### Bet 1 — grow the conversation
Shift the voice from triage to talk, and make it unmistakable that this is a community, not a support queue.
- **"Ask a question" → "Start a discussion."** Window title **"Questions" → "Community discussions."**
- **Community-first boards:** real conversation topics up top — `#introductions`, `#show-and-tell`, `#war-stories`, `#build-in-public`, `#where-in-the-world`, `#the-pub` (the boring `#devrel` is gone). Product topics sit under a **"Product talk"** heading, one glance down.
- **Support has its own door, loudly:** a welcome banner ("This isn't a support queue — hit a wall? → Talk to a human"), a "need it fixed fast?" escape on the Product-talk bar, and a sidebar pointer. Nobody mistakes the vibe.

### Bet 2 — spotlight the people (the old-forum way)
PostHog **already ships** a gamified contributor ladder — it's just buried.
`Hoglet → Hogthusiast → PowerHog → TopHog → ElderHog → Hogfather`
(see `src/components/Squeak/util/getLevel.ts`). The level badge renders *inside a thread* (`PowerHog · 142`) but nowhere you'd notice.
- Rank does **not** clutter the topic list — just like an old ProBoards/phpBB board, where your rank lived under your avatar in a post, never in the index. Names stay clean.
- A **"Top hogs this week"** spotlight (its own little desktop window) surfaces the whole ladder, so contributors actually get *seen* — literally the community role's second bet.
- **Signatures** give everyone a scrap of identity under a post. (Note: needs a `signature` profile field — a small backend add, so it's a follow-up, not the first PR.)

### The look — ProBoards nostalgia, PostHog skin
The refit leans on what made early-2000s boards feel like a *place*, rebuilt in PostHog's current "PostHog OS" design (the draggable window on the illustrated desktop, cream + orange, real level colours): **coloured category bars**, folder/status icons, "Last post by… ↪" jump arrows, signature divider rules, and a "128 hogs browsing" footer.

---

## The prototype

[`prototype/community-redesign.html`](prototype/community-redesign.html) — a self-contained concept built on PostHog's real design language (the "PostHog OS" desktop, the window chrome, their palette, and the real `getLevel` badge colours). Open it in a browser. Toggle **"highlight what changed"** (bottom-left) to see every proposed change outlined against the real page, each tagged with the bet it serves.

It's a concept, not the live site — the hedgehog wallpaper is approximated, and dock icons are stand-ins.

---

## Status

- [x] Explore the real forum + Squeak components
- [x] Concept prototype on the real PostHog OS layout
- [ ] Lock PR scope (see [`docs/PLAN.md`](docs/PLAN.md))
- [ ] Fork `PostHog/posthog.com`, build the diff, keep `npm run build` green
- [ ] Open the PR

See [`docs/PLAN.md`](docs/PLAN.md) for the change-by-change mapping to real components and the proposed PR slices.
