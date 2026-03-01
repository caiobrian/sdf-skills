# Phase: Verify

Validate implementation against spec and generate tests. **Runs as subagent with fresh context.**

Tests are derived from REQUIREMENTS, not code. This prevents confirmation bias.

## Process

### Step 1: Spawn verification subagent

Use Task() with this prompt:

```
Verify the implementation of <feature-name> against its spec.

Read these files first:
1. specs/<feature>/requirements.md — source of truth for tests
2. specs/<feature>/plan.md — types and interfaces contract
3. specs/<feature>/tasks.md — what was implemented
4. .claude/CLAUDE.md — project constitution (test framework, conventions)

Perform these steps IN ORDER:

## Step A: Compliance Check

For each ID in requirements.md, verify it exists in the implemented code:

### Functional Requirements
- RF-01: ✅/❌ [where in code + evidence]

### Non-Functional Requirements
- RNF-01: ✅/❌ [how verified]

### Edge Cases
- EC-01: ✅/❌ [how handled]

### Acceptance Criteria
- CA-01: ✅/❌

### Types
- [ ] Interfaces from plan.md implemented correctly
- [ ] Zero unauthorized `any`
- [ ] Return types match contracts

## Step B: Generate Tests

Derive tests from REQUIREMENTS (not from code):
- Every test MUST reference at least one ID (RF-xx, CA-xx, EC-xx)
- Mandatory categories: happy path (CA-xx), edge cases (EC-xx), error states, loading states (if async), empty states (if renders data)
- `describe` in English, test names in Portuguese
- Use the test framework specified in CLAUDE.md

## Step C: Run Tests

Execute the test suite. If tests fail:
- Identify if it's a test issue or implementation issue
- Fix test issues
- Flag implementation issues

## Step D: Report

Status: ✅ Approved | ⚠️ With caveats | ❌ Failed
Coverage: X/Y requirements covered
Tests generated: N
Tests passing: N/N
Issues: [list]
```

### Step 2: Review report

In main context, review the verification report.

If ❌ Failed: indicate which tasks to reopen and spawn new build subagents.
If ✅ or ⚠️: "Verificação completa. Quer documentar e fechar o ciclo?"

## Rules
- Tests without requirement references = noise — don't generate
- If implementation diverges from spec, FLAG clearly
- No trivial tests without context
