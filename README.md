# hogfork

A workspace for reimagining the **PostHog community forum** ([posthog.com/questions](https://posthog.com/questions)) — moving it from *support desk* toward *community*, and turning that into a real contribution to [PostHog/posthog.com](https://github.com/PostHog/posthog.com).

This repo is deliberately separate from other projects. It holds the design concept, the rationale, and the draft changes. The actual pull request will be opened from a proper fork of `posthog.com` (GitHub only allows PRs between a fork and its upstream).

---

## The idea

The forum today is framed like a helpdesk: you **"Ask a question,"** posts carry statuses like *needs-response*, and product topics lead. But the thing that makes a community a *place* — people recognising each other, wandering in to talk, belonging — is underplayed. Two moves fix most of that, and neither needs a backend change.

### Bet 1 — grow the conversation
Shift the voice from triage to talk, and put the community first.
- **"Ask a question" → "Start a discussion."**
- Window title **"Questions" → "Community discussions."**
- **Off-topic first:** lift `#introductions`, `#where-in-the-world`, `#devrel` above the product boards in the sidebar. Community is the front door; product help is one glance down.
- Support keeps a quiet, dedicated door instead of framing everything.

### Bet 2 — spotlight the people
PostHog **already ships** a gamified contributor ladder — it's just buried.
`Hoglet → Hogthusiast → PowerHog → TopHog → ElderHog → Hogfather`
(see `src/components/Squeak/util/getLevel.ts`). The level badge renders *inside a thread* (`PowerHog · 142`) but **not in the question list**.
- **Surface the level badge in the list**, next to each author.
- Add lightweight **signatures** — a scrap of identity under a post, the old-forum way.
- A **"Top hogs this week"** spotlight so contributors get seen — which is literally the community role's second bet.

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
