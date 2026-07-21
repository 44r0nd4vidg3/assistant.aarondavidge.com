# assistant.aarondavidge.com

A4RON.AI — the resident assistant of [aarondavidge.com](https://aarondavidge.com). Built on the Gemini Enterprise Agent Platform with the Agent Development Kit (ADK), phased like its siblings ([blog](https://github.com/44r0nd4vidg3/blog.aarondavidge.com), [store](https://github.com/44r0nd4vidg3/store.aarondavidge.com)): capability only when it pays rent, security budget landing exactly where the attack surface grows.

## Phases

| Phase | Capability | New attack surface | Security response | Status |
|-------|-----------|--------------------|-------------------|--------|
| 1 — Concierge | Scoped Q&A about Aaron, no tools | Public LLM endpoint · **the lockdown demo itself** | Full defensive gateway: Model Armor (both directions), IP + token + spend caps, data minimization | 🔨 In build |
| 2 — Grounded RAG | Answers cited from the curated corpus + eval harness in CI | Corpus poisoning (low — curated only) | Owner-only indexing, eval regression gate | Planned |
| 3 — Voice | Realtime voice via the SPEAK path | Audio session abuse | Push-to-talk, session caps | Planned |
| 4 — Agentic actions | Allowlisted tools: schedule, message, GitHub activity | **Prompt injection becomes real** (input + tools) | Tool allowlist, confirmation UI, action caps, audit log | Planned |
| 5 — Ops | Review dashboard, feedback → evals, pinned models | Admin session | Isolated origin, managed auth | Planned |
| R — Reserved | Undisclosed expansion | TBD | Threat-modeled at design time, ADR'd before build | Held |

The project thesis: a native, public-facing agent can be **fully locked down** — PII contained, leaks screened, tool misuse prevented, spend capped — and phase 1 ships that entire gateway before anything valuable sits behind it. See [ADR-0003](docs/adr/0003-phase1-threat-model.md) and [ADR-0005](docs/adr/0005-model-armor-screening.md).

Phase R is deliberate: the roadmap holds numbered space and interface headroom for functionality not yet public. Extension points are documented in [docs/architecture.md](docs/architecture.md).

## UX doctrine

No floating bubble. No modal. No empty-chat cold start. The assistant lives *inside* the site's existing A4RON.AI panel as a terminal-native input line; responses stream like console output. Full rationale and interaction spec: [docs/ux.md](docs/ux.md) and [ADR-0002](docs/adr/0002-no-widget-ux.md).

## Decision records

| ADR | Decision |
|-----|----------|
| [0001](docs/adr/0001-platform-and-model-boundary.md) | Gemini Enterprise Agent Platform + ADK, with a model-agnostic boundary |
| [0002](docs/adr/0002-no-widget-ux.md) | The panel is the interface — no chat widget |
| [0003](docs/adr/0003-phase1-threat-model.md) | Phase-1 threat model: denial-of-wallet, not prompt injection |
| [0004](docs/adr/0004-reserved-capability-slot.md) | Reserved capability slot and extension contracts |
| [0005](docs/adr/0005-model-armor-screening.md) | Model Armor as the inline screening layer, both directions, fail-closed |

## Repo layout

- `agent/` — system prompt, grounding context pack, and runtime config spec consumed by the ADK agent
- `docs/` — architecture, UX spec, ADRs

## Author

Aaron Davidge — AI engineer & security researcher · [aarondavidge.com](https://aarondavidge.com) · [@44r0nd4vidg3](https://github.com/44r0nd4vidg3)
