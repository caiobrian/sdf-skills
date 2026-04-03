# SDF — Spec-Driven Flow

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![CI](https://github.com/caiobrian/sdf-skills/actions/workflows/ci.yml/badge.svg)](https://github.com/caiobrian/sdf-skills/actions/workflows/ci.yml)

A structured development framework for Claude Code. Organizes AI-assisted development into clear phases with human approval gates — preventing the context rot that degrades code quality in long sessions.

```
Discovery → Spec → Build → Verify → Document
```

Interactive phases (Discovery, Spec, Document) run in your main context so you can review and approve each step. Execution phases (Build, Verify) run as **subagents with fresh 200k context** — one per task, in parallel where possible.

## Why SDF

The core problem with long AI coding sessions: as the context fills up, Claude starts cutting corners. SDF solves this by:

- Locking the spec before any code is written — no improvisation during Build
- Running each task in a fresh subagent — full context for every implementation
- Tracing every test back to a requirement ID — Verify checks the spec, not intuition

## Installation

```bash
# Global (available in all projects)
npx skills add caiobrian/sdf-skills --global --agent claude-code --all -y

# Or project-scoped
npx skills add caiobrian/sdf-skills --agent claude-code --all -y
```

### Manual install

```bash
git clone https://github.com/caiobrian/sdf-skills.git /tmp/sdf-skills
cp -r /tmp/sdf-skills/skills/sdf ~/.claude/skills/sdf
cp -r /tmp/sdf-skills/skills/sdf-setup ~/.claude/skills/sdf-setup
rm -rf /tmp/sdf-skills
```

### Uninstall

```bash
npx skills remove --global sdf sdf-setup
```

## Skills

### `sdf-setup`

One-time project initialization. Analyzes your codebase and generates:

- **`.claude/CLAUDE.md`** — project constitution: stack, conventions, prohibited patterns
- **`LessonsLearned.md`** — running log of mistakes to avoid in future tasks

**Triggers:** `/sdf-setup`, `setup sdf`

### `sdf`

The main workflow. Smart router that detects the current phase and acts accordingly:

| Phase | When | Runs in |
|-------|------|---------|
| **Quick Track** | Bug fix, UI tweak, config change | Main context |
| **Discovery** | New problem, no spec yet | Main context |
| **Spec** | Problem defined, needs specification | Main context |
| **Build** | Spec approved, tasks pending | Subagent per task |
| **Verify** | Code done, needs validation | Subagent |
| **Document** | Everything done, close cycle | Main context |

**Triggers:** `/sdf`, `sdf`, or any development request (feature, bug, refactor, implement, validate, document)

## Generated artifacts

SDF creates a `specs/` folder per feature:

```
specs/
└── dark-mode/
    ├── requirements.md    # RF-xx, RNF-xx, EC-xx, CA-xx
    ├── plan.md            # Types, interfaces, technical strategy
    └── tasks.md           # T-xx ordered by dependency wave
```

See [`docs/examples/dark-mode/`](docs/examples/dark-mode/) for a complete example.

## Full flow

```
/sdf-setup              → Project constitution (run once per project)
  ↓
/sdf <problem>
  ↓
Discovery               → Problem statement with success criteria
  ↓ (approve)
Spec                    → requirements.md → plan.md → tasks.md
  ↓ (approve)
Build                   → Wave 1: T-01, T-02 (parallel subagents)
                          Wave 2: T-03       (depends on Wave 1)
  ↓
Verify                  → Subagent validates against spec IDs
  ↓
Document                → PR description + LessonsLearned.md update
```

## Quick Track

For small, isolated changes:

```
/sdf fix the typo in the error message on the login page
```

If scope grows, SDF auto-escalates to the full flow.

## Key principles

- **Spec is the contract** — Build and Verify follow the spec, no improvisation
- **Subagents prevent context rot** — each task gets a fresh 200k context window
- **Progressive disclosure** — routing logic in SKILL.md, details in phase files
- **Traceability** — every test references a requirement ID (RF-xx, CA-xx, EC-xx)
- **Language-adaptive** — SDF communicates in whatever language you use

## Documentation

- [Getting Started](docs/getting-started.md) — step-by-step first cycle
- [Example: Dark Mode](docs/examples/dark-mode/) — complete spec output

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT
