# Phase: Build

Implement tasks from the spec. **Each task runs as a subagent with fresh context.** Independent tasks in the same wave run in parallel.

## Required Files

- `specs/<feature>/tasks.md`
- `specs/<feature>/plan.md`
- `specs/<feature>/requirements.md`
- `.claude/CLAUDE.md`
- `LessonsLearned.md`

## Process

### Step 1: Map tasks and waves

Read `specs/<feature>/tasks.md`. Group tasks by wave — tasks with no dependency on each other belong to the same wave. Show the execution plan before starting:

```
Wave 1 (parallel): T-01, T-02
Wave 2 (parallel): T-03, T-04  ← depends on Wave 1
Wave 3:            T-05         ← depends on T-04 specifically
```

If tasks.md has no explicit Wave field, infer waves from the dependency order. Ask to confirm before proceeding.

### Step 2: Execute wave

Spawn **one subagent per task in the current wave simultaneously** using Task(). Provide this prompt per task:

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
- Complexity: [low | medium | high — read from tasks.md]

Model hint: if Complexity is 'low' (scaffolding, renaming, config), prefer a faster/cheaper
model. If 'medium' or 'high', use the default capable model.

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

Report back using this compact JSON (keep it short — main context accumulates all reports):
{
  "task_id": "T-XX",
  "files": ["path/to/file"],
  "requirements_covered": ["RF-xx", "EC-xx"],
  "self_review_pass": true,
  "issues": []
}
If self_review_pass is false or issues is non-empty, add a brief "notes" field explaining why.
```

### Step 3: Review wave output

After **all subagents in the wave** complete, review each output in the main context:
- Does it match the spec?
- Any conflicts between tasks that ran in parallel?

Resolve conflicts before proceeding. Mark `[x]` on completed tasks in `specs/<feature>/tasks.md`.

### Step 4: Next wave or transition

If more waves pending: "Wave N complete. Next: T-xx, T-yy — proceed?" (in the user's preferred language)
If all waves done: "Build complete. Want to validate?" (in the user's preferred language)

## Rules

- Tasks in the same wave → spawn simultaneously in parallel
- Tasks in different waves → wait for previous wave to complete before starting next
- 1 task per subagent — never batch multiple tasks in one subagent
- If spec is ambiguous, ASK the user before spawning subagents
- If a subagent output has issues, fix in a new subagent (never accumulate fixes in main context)
- If a mistake is worth recording, suggest adding to LessonsLearned.md
