# Phase: Build

Implement tasks from the spec. **Each task runs as a subagent with fresh context.**

## Required Files

- `specs/<feature>/tasks.md`
- `specs/<feature>/plan.md`
- `specs/<feature>/requirements.md`
- `.claude/CLAUDE.md`
- `LessonsLearned.md`

## Process

### Step 1: List pending tasks

Read `specs/<feature>/tasks.md` and show which tasks are pending. Ask which to implement next (or suggest the next by dependency order).

### Step 2: Spawn subagent for the task

Use Task() to spawn a fresh context for each task. Provide this prompt:

```
Implement task T-[XX] for the <feature-name> feature.

Read these files first:
1. specs/<feature>/requirements.md — requirements with traceable IDs
2. specs/<feature>/plan.md — types, interfaces, and technical strategy
3. specs/<feature>/tasks.md — full task details for T-[XX]
4. .claude/CLAUDE.md — project constitution (conventions, stack, prohibitions)
5. LessonsLearned.md — past mistakes to avoid

Task details:
- Requirements: [RF-xx, RNF-xx, EC-xx from the task]
- Affected files: [from the task]

Implementation rules:
- Use EXACTLY the types from plan.md
- Handle all edge cases referenced in the task
- Follow CLAUDE.md conventions strictly
- No `any` types
- No silenced errors
- No improvements outside task scope
- No new dependencies without explicit list in plan.md
- Code in English

After implementation, complete this self-review:
- [ ] Types match plan.md
- [ ] Requirements RF-xx covered
- [ ] Edge cases EC-xx handled
- [ ] Zero `any` types
- [ ] Errors handled explicitly
- [ ] LessonsLearned.md respected
- [ ] CLAUDE.md conventions followed

Report back:
1. Files created/modified
2. Self-review result
3. Trade-offs or decisions made
4. Any risks or fragile points
```

### Step 3: Review subagent output

In the main context, review what the subagent produced:
- Does it match the spec?
- Any concerns?

Mark `[x]` on the completed task in `specs/<feature>/tasks.md`.

### Step 4: Next task or transition

If more tasks pending: "Task T-xx complete. Next is T-yy — want to proceed?" (in the user's preferred language)
If all done: "Build complete. Want to validate?" (in the user's preferred language)

## Rules
- 1 task per subagent — never batch multiple tasks
- If spec is ambiguous, ASK the user before spawning the subagent
- If subagent output has issues, fix in a new subagent (don't accumulate in main context)
- If a mistake is worth recording, suggest adding to LessonsLearned.md
