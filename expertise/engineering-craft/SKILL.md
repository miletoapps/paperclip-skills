# Engineering Craft

The engineer turns a plan into code that is correct, clean, safe, and coherent with the system it lives in. Excellence here means handling the cases that break, writing code the next person can maintain, never shipping a hack disguised as a solution, and respecting the existing architecture. This skill is for the agents that write and change code.

## When to use

- When implementing any task that produces or modifies code
- When deciding how to structure a change
- When choosing between a quick hack and a proper implementation

## What great engineering looks like

### Start from a fresh base (sync with the remote first)
- Before starting ANY code work, `git fetch` the remote and base your branch on the current tip of the target branch — humans and other agents also push to these repos outside your view, so a local clone or worktree is never assumed to be current
- Verify against the remote tip before writing anything; never plan or code on top of a stale base
- If the target branch advanced while you worked, rebase onto the new tip (or merge it in) and re-verify your change before opening the PR
- If you find unexpected changes in the same files you are about to touch, STOP and investigate before proceeding — someone may be working in the same area

### Correctness beyond the happy path
- Handle edge cases, empty states, and error conditions — not just the obvious flow
- Validate inputs at boundaries
- Consider concurrency, retries, and partial-failure where relevant
- Never assume external calls succeed — handle their failure

### Clean and maintainable
- Clear names, small focused units, no needless cleverness
- Match the style and conventions already in the codebase
- Correct types — do not silence the type system with escape hatches just to make it compile
- Leave no dead code, no stray debug logging, no commented-out blocks

### Coherent with the architecture
- Follow the project's established patterns (read the context document and look at neighboring code first)
- Put logic where the architecture expects it, not where it is fastest to drop in
- Do not introduce a new dependency, pattern, or paradigm without good reason and (for anything significant) human/plan approval

### No gambiarra (no hacks)
- Do not paper over a deeper problem with a workaround and call it done
- If a proper fix is out of scope, implement the safe minimum AND flag the real fix as tracked debt — explicitly, never silently
- A temporary workaround is always labeled as such, with a path to the real solution

### Self-verification
- Read your own diff before opening the PR — as if reviewing someone else
- Run whatever checks exist (typecheck, lint, build, tests) and confirm green
- Trace the change through the system to confirm it does what was intended and breaks nothing adjacent
- Verify against the plan's acceptance criteria

## PR readiness

Before opening the PR: correct category prefix, complete description (context, changes, validation, category, risks), branch from the right base, no secrets in the diff, checks passing. (See the PR-conventions and secrets-handling disciplines.)

## Invariants you must preserve

1. Edge cases and failure modes handled — not just the happy path.
2. Code matches existing conventions and architecture.
3. No hack shipped as a solution; temporary workarounds are labeled and tracked.
4. Types respected, not bypassed; no debug cruft left behind.
5. Self-review the diff and run all available checks before the PR.
6. Out-of-scope problems are surfaced, never silently buried.
7. Work starts from the current remote tip: fetch before you begin, and rebase before opening the PR if the base advanced.

## The standard

Great engineering leaves the codebase better than you found it: the change is correct under stress, the next maintainer understands it immediately, and it fits the system as if it had always been there. You write code you would be comfortable defending in a rigorous review — because it will get one.
