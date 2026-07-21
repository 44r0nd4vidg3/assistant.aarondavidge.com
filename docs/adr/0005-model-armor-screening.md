# ADR-0005: Model Armor as the inline screening layer

**Status:** Accepted · 2026-07-21

## Context

The lockdown thesis (ADR-0003) requires screening of untrusted input and model output. Hand-rolled filters (regex PII scrubbing, keyword blocklists) are brittle and unmaintained; the platform provides Model Armor as a managed screening service purpose-built for this: prompt injection and jailbreak detection, PII/sensitive-data detection and de-identification, malicious URL screening, and harmful-content filtering, applied to both prompts and responses.

## Decision

Every turn passes through Model Armor twice, at maximum policy strictness, fail-closed:

1. **Pre-model:** visitor prompt screened before it reaches the agent. Injection/jailbreak attempts and malicious payloads are blocked with an in-theme response (`REQUEST DEFLECTED · SENTINEL ARMED`); detected PII in visitor input is flagged and the visitor is redirected to the contact page rather than having the model process it.
2. **Post-model:** agent response screened before it reaches the visitor. Outbound PII is de-identified; leak-pattern or policy-violating output is dropped and regenerated once, then failed closed with the themed error.

Fail-closed means a screening-service outage degrades the assistant to its offline state — it never bypasses to unscreened traffic.

## Consequences

- Injection defense is load-bearing from day one and already proven when phase 4 adds tools — the highest-risk phase inherits a hardened boundary, not a new one.
- Managed screening adds per-turn latency and cost; the UX budget (first token < 1.5s) is revised to < 2s and the spend model prices two screening calls per turn.
- Policy tuning is versioned in this repo alongside the context pack; screening config changes go through the same eval gate as model changes.
- Blocked-attempt metrics (counts and categories, not content) feed the phase-5 dashboard — the lockdown becomes demonstrable with numbers.
