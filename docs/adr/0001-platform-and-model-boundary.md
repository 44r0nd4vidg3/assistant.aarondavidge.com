# ADR-0001: Gemini Enterprise Agent Platform + ADK, with a model-agnostic boundary

**Status:** Accepted · 2026-07-21

## Context

The assistant needs a managed agent runtime (deployment, scaling, state), a code-first framework for precise control of behavior and future multi-agent orchestration, and room to grow into tools and voice. Google's Gemini Enterprise Agent Platform (the 2026 successor to Vertex AI) provides all three via the Agent Development Kit and Agent Runtime, and its model catalog includes both Gemini and Claude — meaning platform choice does not lock model choice.

## Decision

Build on the Gemini Enterprise Agent Platform with the ADK (Python). Keep the model selection behind a single configuration boundary: the agent definition, prompts, context pack, and evals are written model-agnostically, and the site's public claim ("Claude API" on the project card) remains satisfiable by pointing the same agent at Claude through the platform's catalog.

## Consequences

- Managed runtime removes self-hosted inference surface from the threat model entirely.
- Multi-agent phase 4 uses first-class ADK patterns rather than hand-rolled orchestration.
- The eval harness (phase 2) doubles as the model-swap safety net: any model change must pass the same graded set.
- Platform lock-in is accepted at the orchestration layer, deliberately not at the model layer.
