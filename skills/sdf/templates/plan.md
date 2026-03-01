# Plan Template

```markdown
# Plan: [name]

## Implementation Strategy
[technical approach — NO executable code]

## Types and Interfaces
\```typescript
// ALL data contracts — no `any`
\```

## Affected Components/Modules
- [file] → [change description]

## Integration Points
- [connections with existing code]

## Deploy Strategy
[feature flag / rollout / direct]

## Rollback Strategy
[how to revert]

## Technical Risks
- **RT-01:** [risk → mitigation]
```

No executable code — only types/interfaces. Types must cover all RF-xx and EC-xx. Rollback strategy is mandatory.
