# Phase: Spec

Generate 3 sequential artifacts inside `specs/<feature-name>/`. The spec is the contract.

## Output Location

```
specs/<feature-name>/
├── requirements.md
├── plan.md
└── tasks.md
```

Derive `<feature-name>` from the problem statement using kebab-case. Confirm folder name before creating.

## Required Input

- Problem Statement (from Discovery)
- CLAUDE.md (project constitution)
- LessonsLearned.md

If anything is missing, ask before starting.

## Process

### Artifact 1: requirements.md

Read `templates/requirements.md` for structure. Generate with ALL traceable IDs (RF-xx, RNF-xx, EC-xx, CA-xx).

Present and ask for review before proceeding.

### Optional: Technical Research

After requirements.md is approved, if the implementation involves non-trivial technical decisions (library selection, architectural approach, unfamiliar domain), offer:

> "Before planning, do you want me to research the technical options?" (in the user's preferred language)

If accepted, spawn a **research subagent** via Task():

```
Research task for <feature-name>:

Read specs/<feature>/requirements.md for context.

Investigate and report on:
1. Library/tool options that fit the requirements — for each: pros, cons, maintenance status, bundle size (if frontend), community adoption
2. Known pitfalls or gotchas for the chosen approach
3. Compatibility with the stack in .claude/CLAUDE.md
4. Recommended approach with justification

Format each decision as:
DEC-01: [topic] — Recommendation: [option] — Reason: [1-2 sentences] — Alternatives considered: [options]

Keep it concise. This feeds directly into plan.md.
```

Review the research output in the main context and document each decision as **DEC-xx** (Decision IDs). plan.md must reference DEC-xx for any non-obvious technical choices.

### Artifact 2: plan.md

Only after requirements.md is approved (and research complete, if run). Read `templates/plan.md` for structure.

**No executable code — only types/interfaces.**

If research was performed, include a `## Technical Decisions` section at the top of plan.md listing each DEC-xx with its recommendation.

Present and ask for approval before generating tasks.

### Optional: Design Validation

After plan.md, if the change is structural or high-risk, offer:

> "This change is structural. Do you want me to validate plan.md against the actual codebase before proceeding?" (in the user's preferred language)

If accepted:
1. **Feasibility** — Types compatible with existing codebase?
2. **Integration** — Touchpoints mapped? Backward compatibility?
3. **Risks** — Conflicts, unmapped dependencies, performance?
4. **Verdict** — Specific adjustments to plan.md or "Design validated."

### Artifact 3: tasks.md

Only after plan.md is approved. Read `templates/tasks.md` for structure.

## Rules
- Every requirement MUST have an ID
- Tasks reference requirement IDs
- Max ~50 lines per task, ordered by dependency
- Consult LessonsLearned.md before defining strategy
- Respect CLAUDE.md constitution
- Do NOT generate next artifact without approval of previous
- Requirements/plan in the user's preferred language, types in English
- Always communicate in the user's preferred language
