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
- CA-01: ✅/❌ [measured value vs threshold]

### Types
- [ ] Interfaces from plan.md implemented correctly
- [ ] Zero unauthorized `any`
- [ ] Return types match contracts

## Step B: Generate Tests

Derive tests from REQUIREMENTS (not from code):
- Every test MUST reference at least one ID (RF-xx, CA-xx, EC-xx)
- Mandatory categories: happy path (CA-xx), edge cases (EC-xx), error states, loading states (if async), empty states (if renders data)
- `describe` in English, test names in the user's preferred language
- Use the test framework specified in CLAUDE.md

## Step C: Run and Diagnose

Execute the test suite. For each failure, follow this cycle:

1. **Diagnose** — Is the failure caused by:
   - A test issue (wrong assertion, bad mock, setup error)?
   - An implementation issue (logic bug, missing edge case, type mismatch)?

2. **Fix** — Apply the fix:
   - Test issue → fix the test directly
   - Implementation issue → flag it; do NOT fix implementation inside the verify subagent

3. **Re-run** — Execute again after fix.

4. **Escalate** — If the same test fails after one fix attempt, stop and include it in the report as a confirmed implementation gap.

## Step D: Report

Status: ✅ Approved | ⚠️ With caveats | ❌ Failed
Coverage: X/Y requirements covered
Tests generated: N
Tests passing: N/N

Issues (if any):
- [ID] [description] — [test issue fixed | implementation gap requiring reopen of T-xx]
```

### Step 2: Review report

In main context, review the verification report.

If ❌ Failed: reopen the affected tasks and spawn new build subagents for each implementation gap.
If ✅ or ⚠️: "Verification complete. Want to document and close the cycle?" (in the user's preferred language)

## Rules

- Tests without requirement references = noise — don't generate
- If implementation diverges from spec, FLAG clearly — do not silently adapt the test to match wrong behavior
- Never fix implementation issues inside the verify subagent — reopen the build phase for that
- No trivial tests without context
