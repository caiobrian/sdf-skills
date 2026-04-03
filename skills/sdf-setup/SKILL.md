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

Keep under 100 lines. Do NOT include what linters already enforce.

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
- Never expose secrets or credentials in logs, comments, or output
- Never use path traversal patterns (`../`) in file operations
- Never commit with --no-verify

## Folder Structure
- [mapped from project]

## Commands
- Build: [cmd]
- Test: [cmd]
- Test (watch): [cmd]
- Lint: [cmd]
- Coverage: [cmd]

## SDF Config
- research_phase: enabled
- milestone_tracking: disabled
- hooks: enabled
```

### Step 3: Generate `.claude/hooks-guide.md`

Generate a reference file with ready-to-use Claude Code hook configurations for this project.

Detect the project's formatter/linter from Step 1 and fill in the actual commands:

```markdown
# Claude Code Hooks — Project Setup Guide

Configure hooks in `.claude/settings.json` (project) or `~/.claude/settings.json` (global).

## Recommended Hooks for This Project

### Auto-format on file write
Runs the formatter automatically after Claude writes or edits a file.

\`\`\`json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit|MultiEdit",
        "hooks": [
          {
            "type": "command",
            "command": "[detected format command, e.g.: npx prettier --write $CLAUDE_TOOL_INPUT_PATH]"
          }
        ]
      }
    ]
  }
}
\`\`\`

### Guard against dangerous Bash commands
Blocks destructive commands from running without explicit confirmation.

\`\`\`json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$CLAUDE_TOOL_INPUT_COMMAND\" | grep -qE '(rm -rf|git push --force|git reset --hard|DROP TABLE|truncate)' && echo 'BLOCKED: destructive command requires manual confirmation' && exit 1 || exit 0"
          }
        ]
      }
    ]
  }
}
\`\`\`

### Reinforce context after compaction
Re-reads CLAUDE.md after Claude Code compacts the context, so conventions are never lost.

\`\`\`json
{
  "hooks": {
    "PostCompact": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "cat .claude/CLAUDE.md"
          }
        ]
      }
    ]
  }
}
\`\`\`

## How to Apply

1. Open or create `.claude/settings.json`
2. Merge the hook blocks above into the `"hooks"` key
3. Adjust commands to match your project's actual tooling
4. Test: run Claude Code and trigger a file write — formatter should run automatically

## Reference

Full hook event list: PreToolUse, PostToolUse, PreCompact, PostCompact, Notification, Stop, SubagentStop
Full docs: https://docs.anthropic.com/en/docs/claude-code/hooks
```

### Step 4: Generate `LessonsLearned.md`

```markdown
# Lessons Learned
<!-- Format: LL-XXX: Title | Context | Rule | Date -->
<!-- Max 50 entries. Remove oldest when full to keep token cost constant. -->
```

### Step 5: Confirm

Present output and ask (in the user's preferred language):
- If any important convention is missing
- If there are any specific prohibitions
- If the testing section accurately reflects the project's test strategy
- If the SDF Config toggles match their preferred workflow
- If hooks are relevant for this project (or if they already have hooks configured)

## Rules
- Detect patterns from REAL codebase, never assume defaults
- Always communicate in the user's preferred language
