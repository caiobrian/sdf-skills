# Phase: Quick Track

Compressed workflow for small, well-defined tasks. Runs in main context.

## When to use

- Bug fixes with clear reproduction
- Small UI adjustments
- Simple refactors (rename, extract, move)
- Config changes
- Small, isolated features

## When NOT to use → escalate to full flow

- New features affecting multiple modules
- Architectural changes
- Unclear requirements
- Public API changes

## Process

### Step 1: Scope

```markdown
**Problem:** [what's wrong or needed]
**Fix:** [proposed approach]
**Files:** [affected]
**Won't touch:** [boundaries]
```

Ask for confirmation.

### Step 2: Implement

Follow CLAUDE.md conventions. No `any` types. No scope creep.

### Step 3: Quick verify

```markdown
## Quick Check
- [ ] Fix addresses the stated problem
- [ ] No regressions in affected area
- [ ] Types correct
- [ ] CLAUDE.md conventions followed
- [ ] Existing tests pass
```

### Step 4: Done

Present: what changed, quick check results, any risks.

If scope grows:
> "This is more complex than it seemed. I suggest escalating to the full flow. Want to continue with discovery?" (in the user's preferred language)

## Rules
- If scope grows, STOP and escalate
- Respect CLAUDE.md and LessonsLearned.md
- If mistake worth recording, suggest adding to LessonsLearned.md
- Code in English
- Always communicate in the user's preferred language
