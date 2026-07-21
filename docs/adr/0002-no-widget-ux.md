# ADR-0002: The panel is the interface — no chat widget

**Status:** Accepted · 2026-07-21

## Context

Assistant widgets have earned their bad reputation: floating bubbles occlude content, modals hijack the page, empty chat panes put the burden of a cold start on the visitor, and vendor styling breaks the site's design language. The site already has a designed A4RON.AI panel in the hero — a native surface with status, visualizer, and brand voice.

## Decision

The assistant renders inside the existing panel. The INITIALIZE CHAT button is replaced by an always-ready terminal input line; responses stream as console output in the site's own vocabulary; quick-intent chips provide one-tap value; assistant.html is the same conversation at full-screen, not a separate experience. No bubble, no modal, no third-party chat chrome, in any phase.

## Consequences

- Zero-click start; the first interaction costs the visitor nothing but a glance.
- The front end is custom (no drop-in widget library), accepted as the price of native feel.
- The panel's conversational contract becomes a cross-phase invariant — voice and tools must render into the same stream.
- Honesty affordances (AI disclaimer, human escape hatch) are part of the interface spec, not an afterthought.
