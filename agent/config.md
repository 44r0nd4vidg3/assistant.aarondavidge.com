# Gateway, screening & runtime configuration spec (phase 1)

Values finalized at deploy; the *existence* of each control is non-negotiable (ADR-0003, ADR-0005). The gateway pipeline runs in strict order, fail-closed at every stage:

```
request → CORS → IP rate limit → input token cap → window truncation
        → Model Armor PRE-screen → ADK agent → Model Armor POST-screen
        → output cap → response
```

## Cost & abuse controls

| Control | Spec |
|---------|------|
| Per-IP rate limit | 10 requests/min, 60/day |
| Input token cap | 1k tokens/turn — over-length prompts rejected pre-model |
| Conversation window | Last 6 turns retained; older context truncated (bounds cost + context-manipulation) |
| Output cap | 400 tokens/turn |
| Session budget | 8k output tokens, then in-theme cutoff |
| Monthly spend | Alarm at 50%, hard cutoff at 100% |
| CORS | aarondavidge.com + assistant.aarondavidge.com only |

## Model Armor policy (both directions, max strictness, fail-closed)

| Direction | Screens for | Action on hit |
|-----------|-------------|---------------|
| PRE (prompt) | Prompt injection / jailbreak | Block → `REQUEST DEFLECTED · SENTINEL ARMED` |
| PRE (prompt) | Malicious URLs | Block |
| PRE (prompt) | PII in visitor input | Do not process → redirect to /contact |
| POST (response) | Outbound PII | De-identify before send |
| POST (response) | Leak patterns / policy violation | Drop, regenerate once, then fail closed |
| POST (response) | Harmful content | Drop, fail closed |
| Service outage | Any screening call fails | Degrade to offline state — never bypass |

## Data & model

| Control | Spec |
|---------|------|
| Transcript retention | 7 days, then purged |
| Screening logs | Verdict + category only, no transcript content beyond retention |
| PII policy | None solicited; contact routing bypasses the model |
| Session state | In-memory per session; no cross-session memory in phase 1 |
| Model config | Behind the ADR-0001 boundary; changes pass the eval set (phase 2+) |
| Screening config | Versioned in-repo; changes pass the same eval gate |
