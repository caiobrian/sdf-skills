# Requirements Template

```markdown
# Requirements: [name]

## Context
[current state + problem + metrics]

## Objective
[1-2 sentences]

## Functional Requirements
- **RF-01:** [the system must...]
- **RF-02:** [the system must...]

## Non-Functional Requirements
- **RNF-01 (Performance):** [specific metric, e.g., p95 < 200ms]
- **RNF-02 (Reliability):** [e.g., retry with exponential backoff, max 3 attempts]
- **RNF-03 (Compatibility):** [targets, e.g., Chrome 120+, Node 20+]
- **RNF-04 (Observability):** [what must be logged/traced and at which level]

## Edge Cases
- **EC-01:** [scenario → expected behavior]
- **EC-02:** [scenario → expected behavior]

## Out of Scope
- [explicit exclusions — mandatory, at least one]

## Acceptance Criteria
- **CA-01:** [verifiable with a number or binary outcome, e.g., "loads in < 2s on 3G" or "user can complete X without Y"]
- **CA-02:** [avoid subjective language — "fast", "good", "clean" are not criteria]
```

Every requirement has a unique ID. Acceptance criteria must be **measurable** — include thresholds, counts, or binary outcomes. Edge cases define scenario AND expected behavior. Out of Scope is mandatory.
