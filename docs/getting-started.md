# Getting Started with SDF

This guide walks you through your first complete SDF cycle — from project setup to a shipped feature.

## Prerequisites

- [Claude Code](https://claude.ai/code) installed
- A project repository (any language/framework)

## Step 1: Install SDF

```bash
npx skills add caiobrian/sdf-skills --global --agent claude-code --all -y
```

This installs two skills globally:
- **`sdf`** — the main workflow
- **`sdf-setup`** — one-time project initialization

## Step 2: Initialize your project

In a Claude Code session inside your project, run:

```
/sdf-setup
```

Claude will analyze your codebase and generate two files:

| File | Purpose |
|------|---------|
| `.claude/CLAUDE.md` | Project constitution — stack, conventions, prohibitions |
| `LessonsLearned.md` | Running log of mistakes to avoid |

Review both files and adjust anything that's wrong or missing. These are the source of truth for all future SDF cycles.

## Step 3: Start a development cycle

Trigger SDF on any development request:

```
/sdf implement dark mode for the settings page
```

or simply describe what you want:

```
users are reporting that the login form doesn't work on mobile
```

Claude will detect the right phase and begin there.

## Step 4: Follow the flow

A full cycle goes through these phases:

```
Discovery → Spec → Build → Verify → Document
```

You interact at each transition point. Claude will ask for approval before moving to the next phase.

### Discovery

Claude restates the problem, asks targeted questions (max 3 per message), and produces a **Problem Statement** with measurable success criteria.

### Spec

Three artifacts are generated in `specs/<feature>/`:

- `requirements.md` — functional (RF), non-functional (RNF), edge cases (EC), acceptance criteria (CA)
- `plan.md` — types, interfaces, technical strategy
- `tasks.md` — ordered implementation tasks with dependency waves

You review and approve each artifact before proceeding.

### Build

Each task runs in a **fresh subagent** (separate context window). Independent tasks in the same wave run in parallel.

This prevents context rot — the #1 reason AI-generated code degrades in quality mid-session.

### Verify

A dedicated subagent validates the implementation against the spec. Every test is traced back to a requirement ID (RF-xx, CA-xx, EC-xx).

### Document

Claude writes a PR description and closes the cycle. `LessonsLearned.md` is updated with anything notable.

## Quick Track

For small, isolated tasks (bug fix, rename, config change), SDF shortcuts the full flow:

```
/sdf fix the typo in the error message on line 42 of auth.ts
```

If scope grows during Quick Track, Claude escalates automatically to the full flow.

## Tips

- **Trust the spec** — if Build doesn't match what you wanted, the spec was wrong. Fix the spec, not the code.
- **Keep CLAUDE.md short** — under 80 lines. Detailed rules belong in the spec, not the constitution.
- **Add to LessonsLearned.md** — whenever Claude makes a mistake worth remembering, add it. Future tasks will avoid repeating it.
- **Run sdf-setup once per project** — re-run it only when the stack changes significantly.
