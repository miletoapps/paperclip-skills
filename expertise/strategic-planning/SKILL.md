# Strategic Planning

The planner turns a fuzzy goal into a rigorous, complete plan that an executor can follow without surprises. Excellence here means questioning premises, investigating reality first, weighing trade-offs honestly, and producing a plan so thorough that the risky thinking is done before any code is written. This skill is for the agent that architects and plans before execution.

## When to use

- When a task needs design or planning before implementation (notably Category B)
- During Discovery — understanding the real state before proposing anything
- When choosing between architectural approaches
- When writing a Plan Issue for human approval

## What great planning looks like

### Discovery first
- Never plan against assumptions. Investigate the real code, schema, data, and constraints before proposing anything.
- Map the full surface the change touches — including indirect ripples through APIs, jobs, data, and external services.
- Read the project context document for known gotchas, fragilities, and history.

### Question the premise
- Ask whether the requested thing is the right thing. Sometimes the best plan reframes the problem.
- Surface hidden assumptions in the request and check them.
- If the goal conflicts with the project's long-term health, say so.

### Design with trade-offs
- Produce more than one viable approach when the choice is non-trivial
- For each: what it optimizes, what it costs, what it forecloses later
- Recommend one, with reasoning — thinking several moves ahead (scale, maintenance, future change)
- Prefer approaches coherent with the existing architecture over clever novelty

### Completeness of the plan
A Plan Issue should leave nothing important to chance:
- Context and origin (which goal/issue)
- Scope — explicitly in and explicitly out
- Files / components affected
- Technical decisions and why
- Risks and how they are mitigated
- Acceptance criteria (objective, checkable)
- Rollback consideration for anything risky

### Right-sized rigor
Thorough is not the same as bloated. Plan the appropriate depth for the risk — a small change gets a tight plan, a dangerous one gets an exhaustive one. Do not pad; do not under-specify.

## Invariants you must preserve

1. Discovery (real investigation) precedes every plan — no planning on assumptions.
2. The plan states scope in AND out, files, decisions, risks, and acceptance criteria.
3. Non-trivial choices present trade-offs and a justified recommendation.
4. The plan respects the project's long-term health over the quick path.
5. For Category B, the plan is complete enough to approve without seeing code.
6. Surface flaws in the request itself rather than planning around them silently.

## The standard

A great plan means the hard thinking is finished before code starts: the executor implements with confidence, the reviewer checks against a clear target, and the human approved with full understanding of scope, cost, and risk. The plan anticipates the problems instead of discovering them in production.
