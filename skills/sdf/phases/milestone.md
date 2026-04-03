# Phase: Milestone

Close a development milestone: consolidate learnings, generate a CHANGELOG entry, archive completed specs, and tag the release.

## When to Use

Trigger this phase when a meaningful set of features is complete and the team is ready to cut a version — not after every single feature. Typical triggers: "fechar milestone", "close milestone", "gerar CHANGELOG", "tagear versão".

## Required Input

- Milestone name or version (e.g., `v1.2.0` or `Q1-features`)
- List of features completed in this milestone (or the set of `specs/` folders to include)
- `.claude/CLAUDE.md` (project constitution)
- `LessonsLearned.md`

If anything is missing, ask before starting.

## Process

### Step 1: Consolidate LessonsLearned

Review `LessonsLearned.md`. For entries added during this milestone:
- Identify patterns or recurring themes
- Mark entries that are now "institutionalized" (absorbed into CLAUDE.md conventions) with `[archived]`
- Do NOT delete — only mark archived ones. Prune oldest entries if count exceeds 50.

If any lesson should become a permanent convention, suggest adding it to CLAUDE.md.

### Step 2: Generate CHANGELOG entry

Produce a CHANGELOG block for this milestone:

```markdown
## [<version>] — <date>

### Added
- <feature>: <1-line summary> (specs/<feature-name>/)

### Changed
- <what changed and why>

### Fixed
- <bug and root cause, if any>

### Technical Decisions
- DEC-xx: <decision summary> (see specs/<feature>/plan.md)

### Lessons Learned
- <key insight from this milestone worth highlighting>
```

Present and ask for review before proceeding.

### Step 3: Archive completed specs

For each feature in this milestone:
1. Move `specs/<feature>/` to `specs/archive/<version>/<feature>/`
2. Create a one-line index entry in `specs/archive/index.md`:

```
| <version> | <feature-name> | <date> | <1-line summary> |
```

If `specs/archive/index.md` does not exist, create it with the header:

```markdown
# Specs Archive

| Version | Feature | Date | Summary |
|---------|---------|------|---------|
```

### Step 4: Suggest git tag

Propose the release tag command for the user to run manually:

```
git tag -a <version> -m "Release <version>: <milestone name>"
git push origin <version>
```

Do NOT run this automatically — tagging is a manual decision.

### Step 5: Confirm and close

Present a summary:
- CHANGELOG entry added
- Specs archived
- LessonsLearned.md updated
- Git tag command provided

Ask if there is any remaining cleanup before the milestone is considered closed.

## Rules

- Never delete specs — only archive (move to `specs/archive/`)
- Never push or tag automatically — always propose commands for manual execution
- Always communicate in the user's preferred language
