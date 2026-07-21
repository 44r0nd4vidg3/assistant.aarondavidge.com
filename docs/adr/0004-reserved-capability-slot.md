# ADR-0004: Reserved capability slot and extension contracts

**Status:** Accepted · 2026-07-21

## Context

The roadmap intentionally holds space for functionality not yet publicly specified. Past phases (blog, store) showed that late additions are cheap when interfaces anticipated growth and expensive when they didn't. The reserved work should slot in without renegotiating the architecture.

## Decision

The roadmap carries an explicitly reserved phase (Phase R). Three extension contracts are maintained from phase 1 onward so Phase R can rely on them: the gateway accepts additional routes without front-end changes; sub-agent registration under the triage agent is additive; the context pack and eval harness are versioned together so new capability ships with its own grading. Any reserved functionality is threat-modeled and receives its own ADR before implementation begins.

## Consequences

- Undisclosed features have a documented landing zone instead of arriving as architecture breaks.
- The contracts impose mild discipline on phases 1–5 (nothing may assume it is the last consumer of the gateway or triage agent).
- Security review is structurally guaranteed for whatever Phase R becomes — the ADR-before-build rule is on the record.
