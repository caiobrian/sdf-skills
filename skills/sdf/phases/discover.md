# Phase: Discovery

Understand the problem before any specification or code.

## Process

### Step 1: Classify

- **Type:** bug | feature | refactor | infra
- **Symptom or root cause?** If symptom, investigate cause.

### Step 2: Restate

Rewrite the problem. Ask: "É isso mesmo?"

### Step 3: Fill gaps

Max 3 questions per message. Only ask what's missing:
- Who is affected?
- Which metric is impacted?
- Current vs expected behavior?
- Frequency / quantitative impact?
- Constraints (stack, deadline, dependencies)?
- Measurable success criteria?

If sufficient context was already provided, skip to Step 4.

### Step 4: Problem Statement

```markdown
## Problem Statement

**Problem:** [2-3 sentences]
**Type:** [bug | feature | refactor | infra]
**Affected metric:** [which one]
**Impact:** [quantitative]
**Root cause hypothesis:** [if applicable]
**Success criteria:** [measurable]
**Constraints:** [stack, deadline, deps]
```

### Step 5: Transition

"Problem statement pronto. Quer seguir pra spec?"

For small, well-defined problems, suggest quick track instead.

## Rules
- NEVER suggest solutions or code in this phase
- Focus on separating symptom from cause
