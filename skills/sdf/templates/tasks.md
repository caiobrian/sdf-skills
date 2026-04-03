# Tasks Template

```markdown
# Tasks: [name]

## T-01: [descriptive name]
- **Wave:** 1
- **Type:** component | hook | util | service | test | config
- **Complexity:** low | medium | high
- **Requirements:** RF-01, RNF-02
- **Input:** [precondition]
- **Output:** [deliverable]
- **Done:** [objective criteria]
- **~Lines:** [estimate]
- [ ] Pending

## T-02: [descriptive name]
- **Wave:** 1
- **Type:** component | hook | util | service | test | config
- **Complexity:** low | medium | high
- **Requirements:** RF-02, EC-01
- **Input:** [precondition]
- **Output:** [deliverable]
- **Done:** [objective criteria]
- **~Lines:** [estimate]
- [ ] Pending

## T-03: [descriptive name]
- **Wave:** 2
- **Type:** component | hook | util | service | test | config
- **Complexity:** low | medium | high
- **Requirements:** RF-03
- **Input:** [depends on T-01, T-02]
- **Output:** [deliverable]
- **Done:** [objective criteria]
- **~Lines:** [estimate]
- [ ] Pending
```

Each task references requirement IDs. Max ~50 lines per task. One responsibility per task — split if it does two things.

**Wave rules:**
- Tasks in the same wave have no dependencies on each other and run in parallel.
- A task that depends on another task must be in a later wave.
- If all tasks are sequential, use Wave 1, 2, 3... with one task each.
