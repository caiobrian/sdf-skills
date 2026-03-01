# Phase: Document

Close the SDF cycle. Runs in main context (interactive).

**This phase only runs when explicitly invoked by the user.**

## Process

### Step 1: Technical record

```markdown
# Record: [feature/fix name]

## What changed
[summary with RF-xx references]

## Technical decisions
- [decision + justification + related RF/RNF]

## Trade-offs accepted
- [what was sacrificed + why acceptable]

## Spec deviations
- [changes during implementation + justification]
- If none: "No deviations"

## Technical debt created
- [if any + when to resolve]

## Post-deploy monitoring
- [what to monitor + alert thresholds]
```

### Step 2: Update artifacts

- [ ] `specs/<feature>/plan.md` — reflects what was ACTUALLY implemented
- [ ] `specs/<feature>/tasks.md` — all checkboxes marked [x]
- [ ] `LessonsLearned.md` — session errors documented

### Step 3: PR Description

```markdown
## What
[2-3 sentences]

## Why
[problem + impacted metric]

## How
[technical approach]

## Tests
[coverage + what was validated]

## Risks
[attention points for reviewer]

## Rollback
[how to revert]
```

### Step 4: Confirm

"Ciclo SDF completo. Artefatos atualizados. Algo mais antes de fechar?"

## Rules
- Only document decisions that actually happened
- If no deviations, say "Sem desvios"
- Always suggest additions to LessonsLearned.md if errors occurred
