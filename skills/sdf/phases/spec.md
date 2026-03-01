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

### Artifact 2: plan.md

Only after requirements.md is approved. Read `templates/plan.md` for structure.

**No executable code — only types/interfaces.**

Present and ask for approval before generating tasks.

### Optional: Design Validation

After plan.md, if the change is structural or high-risk, offer:

> "Essa mudança é estrutural. Quer que eu valide o plan.md contra o codebase real antes de seguir?"

If accepted:
1. **Feasibility** — Types compatible with existing codebase?
2. **Integration** — Touchpoints mapped? Backward compatibility?
3. **Risks** — Conflicts, unmapped dependencies, performance?
4. **Verdict** — Specific adjustments to plan.md or "Design validado."

### Artifact 3: tasks.md

Only after plan.md is approved. Read `templates/tasks.md` for structure.

## Rules
- Every requirement MUST have an ID
- Tasks reference requirement IDs
- Max ~50 lines per task, ordered by dependency
- Consult LessonsLearned.md before defining strategy
- Respect CLAUDE.md constitution
- Do NOT generate next artifact without approval of previous
- Requirements/plan in Portuguese, types in English
