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
- **RNF-01 (Performance):** [specific metric]
- **RNF-02 (Reliability):** [e.g., retry with backoff]
- **RNF-03 (Compatibility):** [targets]
- **RNF-04 (Observability):** [logging/monitoring]

## Edge Cases
- **EC-01:** [scenario → expected behavior]
- **EC-02:** [scenario → expected behavior]

## Out of Scope
- [explicit exclusions]

## Acceptance Criteria
- **CA-01:** [verifiable yes/no]
- **CA-02:** [verifiable yes/no]
```

Every requirement has a unique ID. Acceptance criteria are binary. Edge cases define scenario AND expected behavior. Out of Scope is mandatory.
