# Called — App Flow Map

A click-by-click map of the Called web app, captured by walking the product as a logged-in admin.

**Live site:** https://called-io.github.io/called-journey/ (enabled below)

## What's in here

| File | Purpose |
|---|---|
| [`index.html`](./index.html) | Screen-by-screen report — 53 cards across 7 phases. Click any screenshot to view full-size, expand "Actions" on each card to see what every button does. |
| [`tree.html`](./tree.html) | Interactive node-link graph of the whole flow. Switch between tree / levels / force layouts, toggle phases on and off, click a node for its screenshot. |
| [`flow.json`](./flow.json) | Machine-readable sidecar — every screen, every action, every transition target, plus a `ux_observations` array of friction points worth fixing. Feed it to an LLM to surface UX issues. |
| `screenshots/` | 53 captured PNGs at 1440×900, plus a handful of meta-previews of the report itself. |

## Coverage (7 phases, 53 screens)

1. **Auth & onboarding** — sign in, sign up, email forms, password reset, logout confirm
2. **Shell & navigation** — home, chat, groups, members, insights, pathway, events, news, profile menu, all settings pages, notifications panel, community detail
3. **Community lifecycle** — full 2-step create wizard → post-create state → QR modal → Edit Community page → name-confirmation delete
4. **Chat channels** — new message picker → create channel wizard → send message → message-options menu → channel-options menu → delete
5. **Groups** — create modal → detail → edit → delete-with-name confirmation
6. **Events, News & feature CRUD** — Event create form, News create form
7. **Modals & overlays** — captured throughout phases 3–5

## How it was made

Captured with Playwright MCP driving a browser through the running app on `localhost:5274`, on `2026-05-13`, under Jason Brown's admin account. The full report and tree are static HTML — no server required.

## Highlights from `ux_observations`

- Two destructive flows use different friction levels: community/group delete requires typing the name; channel/message delete is a single-click confirm. Consider standardizing.
- `/profile/notifications` exists as a route but is not linked anywhere in the Settings sidebar — discoverability gap.
- Creating a community auto-generates a "Women's Group" default group and a "Bible Study" upcoming event — this is surprising and not disclosed in the creation wizard.
- The Headway "What's New" iframe intercepts pointer events on cards near the top-right of the page when visible — real users may bump into hard-to-click affordances when the widget is open.
- Action buttons on the community/group hero are `role="button"` divs (not real `<button>`s) — complicates accessibility tooling.

(Full list in [`flow.json`](./flow.json) → `ux_observations`.)
