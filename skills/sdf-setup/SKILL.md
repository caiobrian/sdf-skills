---
name: sdf-setup
description: "Initializes project constitution (CLAUDE.md) and LessonsLearned.md for the SDF workflow. Activates when onboarding a new repository, starting a new project, or when no CLAUDE.md exists. Triggers include 'setup sdf', 'iniciar projeto', 'configurar sdf', '/sdf-setup'."
---

# SDF Setup — Project Constitution

Initialize foundational artifacts: `.claude/CLAUDE.md` and `LessonsLearned.md`.

## Process

### Step 1: Analyze the codebase

Examine: stack, framework, bundler, runtime, code patterns, test framework, linters/formatters, folder structure, package scripts.

For tests specifically, identify:
- Test framework and runner (Jest, Vitest, Pytest, etc.)
- Test file naming convention (`*.test.ts`, `*.spec.ts`, `__tests__/`, etc.)
- Mocking patterns (vi.mock, jest.mock, MSW, sinon, etc.)
- Coverage tool and expected threshold (if configured)
- Test data patterns (factories, fixtures, builders)
- Integration vs unit test separation (if any)

If the project is empty, ask for preferences.

### Step 2: Generate `.claude/CLAUDE.md`

Keep under 80 lines. Do NOT include what linters already enforce.

```markdown
# Project Constitution

## Stack
- [detected]
- Prohibited: [what NOT to use]

## Tech Decisions
- [e.g., Data fetching: TanStack Query, never fetch + useEffect]

## Code Conventions
- [extracted from codebase]

## Quality Standards
- [from linter/formatter configs]

## Testing
- Framework: [e.g., Vitest + Testing Library]
- Test files: [naming convention, e.g., *.test.ts next to source]
- Mocking: [pattern used, e.g., vi.mock for modules, MSW for HTTP]
- Coverage threshold: [e.g., 80% lines — enforced in CI]
- Test data: [pattern, e.g., factory functions in tests/factories/]

## Prohibited Actions
- Never install new dependencies without explicit approval
- Never silence errors or use `any` types

## Folder Structure
- [mapped from project]

## Commands
- Build: [cmd]
- Test: [cmd]
- Test (watch): [cmd]
- Lint: [cmd]
- Coverage: [cmd]
```

### Step 3: Generate `LessonsLearned.md`

```markdown
# Lessons Learned
<!-- Format: LL-XXX: Title | Context | Rule | Date -->
<!-- Max 50 entries. Remove oldest when full to keep token cost constant. -->
```

### Step 4: Confirm

Present output and ask (in the user's preferred language):
- If any important convention is missing
- If there are any specific prohibitions
- If the testing section accurately reflects the project's test strategy

## Rules
- Detect patterns from REAL codebase, never assume defaults
- Always communicate in the user's preferred language
