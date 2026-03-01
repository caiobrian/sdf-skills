# SDF — Spec-Driven Flow

A structured development framework for Claude Code. Organizes AI-assisted development into phases: **Discovery → Spec → Build → Verify → Document**.

Prevents context rot by running execution phases (Build/Verify) as subagents with fresh context. Interactive phases (Discovery/Spec/Document) run in main context for human approval at each step.

## Installation

### Via `npx skills` (recommended)

```bash
# Install globally (available across all projects)
npx skills add caiobrian/sdf-skills --global --agent claude-code --all -y

# Or install in current project only
npx skills add caiobrian/sdf-skills --agent claude-code --all -y
```

### Manual

```bash
git clone https://github.com/caiobrian/sdf-skills.git /tmp/sdf-skills
cp -r /tmp/sdf-skills/skills/sdf ~/.claude/skills/sdf
cp -r /tmp/sdf-skills/skills/sdf-setup ~/.claude/skills/sdf-setup
rm -rf /tmp/sdf-skills
```

## Skills

### `sdf-setup`

One-time project initialization. Analyzes your codebase and generates a project constitution (`.claude/CLAUDE.md`) and `LessonsLearned.md`.

**Triggers:** `setup sdf`, `/sdf-setup`

### `sdf`

Main workflow. Smart router that detects the current phase and acts accordingly:

| Phase | When | Execution |
|-------|------|-----------|
| **Quick Track** | Bug fix, UI tweak, config change | Main context |
| **Discovery** | New problem, no spec yet | Main context |
| **Spec** | Problem defined, needs specification | Main context |
| **Build** | Spec approved, tasks pending | Subagent per task |
| **Verify** | Code done, needs validation | Subagent |
| **Document** | Everything done, close cycle | Main context |

**Triggers:** `sdf`, `/sdf`, or any development request (new feature, bug, refactor, implement, validate, document)

## Full Flow

```
/sdf-setup          → Project constitution (once)
  ↓
Discovery           → Understand the problem
  ↓
Spec                → requirements.md → plan.md → tasks.md
  ↓
Build               → Implement (1 subagent per task)
  ↓
Verify              → Test against spec (subagent)
  ↓
Document            → Close cycle + PR description
```

## Generated Artifacts

```
specs/
└── <feature-name>/
    ├── requirements.md    # RF-xx, RNF-xx, EC-xx, CA-xx
    ├── plan.md            # Types, interfaces, strategy
    └── tasks.md           # T-xx ordered by dependency
```

## Key Principles

- **Spec is the contract** — Build and Verify follow the spec, no improvisation
- **Subagents prevent context rot** — each task gets fresh 200k context
- **Progressive disclosure** — SKILL.md routes, phase files have the details
- **Quick Track** — shortcut for small tasks, auto-escalates if scope grows
- **Traceability** — every test references a requirement ID (RF-xx, CA-xx, EC-xx)

## License

MIT