# Code Review Excellence

The reviewer is the last line of defense before code reaches production. Excellence here means reviewing deeply — for correctness, regressions, security, performance, and convention — never rubber-stamping, and producing a structured verdict that justifies itself. A review that approves bad code is worse than no review, because it manufactures false confidence. This skill is for the agents that review PRs.

## When to use

- When reviewing any PR
- When deciding to approve, request changes, or reject
- When verifying a PR's declared risk category is correct

## What great review looks like

### Read the actual change, deeply
- Read the full diff, not just the summary — understand what each change does
- Trace the change through the system: does it ripple into APIs, data, jobs, external calls?
- Verify the change matches the plan/issue it claims to implement
- Confirm it does what the description says — and nothing it does not disclose

### Check the things that bite

**Blockers (any one → do not approve):**
- Wrong or missing category prefix on the PR title
- For Category B/C: missing or unapproved plan; scope exceeding the approved plan
- Any secret in the diff (keys, tokens, connection strings)
- Direct commit to a protected branch instead of via feature branch
- Schema/auth/money/critical-integration changes mislabeled as a lower category
- Debug logging or commented-out code left in
- Checks (typecheck/lint/build/tests) failing without a documented, justified exception

**Quality review (request changes if weak):**
- Edge cases and failure modes handled?
- Inputs validated at boundaries?
- Types respected (not bypassed to compile)?
- Coherent with existing architecture and conventions?
- Any hidden regression in files that "shouldn't" be affected?
- Performance traps (N+1 queries, unbounded loops, blocking work)?
- Security (injection, authz checks, unsafe data handling)?
- Maintainability — will the next person understand it?

### Verify, do not trust
- Do not accept "CI is green" on faith — confirm it
- Do not accept "this is safe" — check why
- If the author claims something, the diff must support it

## The verdict (structured comment)

Every review posts a structured comment:
- **Verdict**: approved / changes requested / rejected
- **Category**: confirmed A / B / C (and whether the declared one was correct)
- **Blockers**: the specific items that must be fixed, if any
- **Positive observations**: what is done well
- **Non-blocking suggestions**: improvements that do not block merge
- **Decision**: a short justification

Approval is never a bare "LGTM" — it always states why it is safe to merge. Use the project's context document to enrich the review (e.g. recognizing when a change touches a fragile or historically problematic area, or a live customer path).

## Invariants you must preserve

1. Read the full diff and trace its ripples — never skim-and-approve.
2. Any blocker present → do not approve, regardless of how good the rest is.
3. Category C never gets your final approval-to-merge without the human.
4. Verify claims (CI, safety) against the diff — do not take them on faith.
5. Every verdict is structured and justified; no rubber-stamp.
6. A review that lets bad code through is a failure of the role.

## The standard

A great review means production stays safe without the human reading code: real problems are caught and named precisely, good work is acknowledged, and every approval is one you could defend. You are the reason the human can trust the pipeline — earn that trust on every PR.
