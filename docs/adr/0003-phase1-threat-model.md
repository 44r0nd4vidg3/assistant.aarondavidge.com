# ADR-0003: Phase-1 threat model — lockdown is the product

**Status:** Accepted · 2026-07-21 (supersedes the original draft, which deferred injection screening to phase 4)

## Context

A public LLM endpoint on a security researcher's site will be probed for sport. The original draft reasoned that a tool-less agent has nothing to lose but a screenshot and deferred injection hardening to phase 4. That reasoning missed the project's actual thesis: **demonstrating that a native, public-facing agent can be fully locked down** — PII containment, leak prevention, tool-misuse prevention, and spend control. The security stack is not overhead on the demo; it *is* the demo.

## Decision

Phase 1 ships the full defensive gateway even though the agent holds no secrets and no tools:

- **Cost controls:** per-IP rate limits, input *and* output token caps per turn, session budgets, conversation-window truncation, monthly spend alarm with hard cutoff.
- **Model Armor at full capacity, both directions, every turn** (ADR-0005): pre-model screening of prompts (injection/jailbreak, PII, malicious URLs) and post-model screening of responses (PII de-identification, leak patterns, harmful content). Fail-closed.
- **Data minimization:** no PII solicited, 7-day transcript retention, contact flows routed to the site's contact page rather than through the model.

The system prompt is still written assuming it will be extracted and published — screening reduces exposure, it does not create secrecy.

## Consequences

- Worst-case financial exposure is capped by configuration; worst-case content exposure is bounded by symmetric screening.
- The gateway's full stack exists *before* anything valuable sits behind it — phase 4's tools inherit a battle-tested boundary instead of a rushed one.
- Latency and cost of per-turn screening are accepted as the price of the thesis.
- Screening verdicts are logged (without transcript content beyond retention policy) to make the lockdown measurable — blocked-attempt counts become portfolio data.
