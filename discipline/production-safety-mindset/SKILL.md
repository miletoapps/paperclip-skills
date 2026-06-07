# Production Safety Mindset

Production is sacred. Real users depend on it in real time. Every change that can reach production must be made with the assumption that a mistake will hurt someone — and therefore with backups, a rollback plan, verification, and conscious awareness of risk windows. This skill is the universal safety discipline; the specific critical resources of each project live in that project's context document.

Applies to every agent that touches, reviews, or deploys anything that can affect a running system.

## When to use

- Before ANY change to infrastructure, databases, live services, or integrations
- Before any deploy
- When assessing the risk of a task (alongside the risk-categories skill)
- When reviewing a PR that touches sensitive areas

## Core principles

### 1. Never assume success
After any change, verify it actually worked. "It should be fine" is not verification. Check health, status, logs, real behavior. Assume nothing.

### 2. Always have a rollback
Before making a risky change, know exactly how to undo it. If you cannot describe the rollback, you are not ready to make the change.

### 3. Back up before mutating
Before altering anything that holds state (a workflow definition, a config, data), capture its current form so it can be restored.

### 4. Respect risk windows
Some operations have a window where the system is degraded (a service restart, a migration, a cache rebuild). Know the window, minimize it, and avoid stacking risky operations.

### 5. Smoke test after changing live behavior
After a change that affects a live path, exercise that path end to end with a test input and confirm the expected result — do not wait for a real user to discover a break.

### 6. Confirm state before destructive or irreversible steps
Before a drop, a mass delete, or a deploy, confirm the precondition (e.g. the right code is pushed, the right rows are targeted). Irreversible operations get double-checked.

## Standard safe-change procedure

1. Understand the blast radius — what depends on this?
2. Back up the current state
3. Make the change in the smallest, most reversible way possible
4. Verify it did what you intended (do not assume)
5. Smoke test the affected path
6. Keep the rollback ready until you are confident
7. If anything looks wrong, roll back first, investigate second

## Invariants you must preserve

1. Rollback plan exists before any risky change.
2. Backup taken before mutating stateful things.
3. Verification after every change — never assume success.
4. Smoke test after touching live behavior.
5. Destructive/irreversible operations require confirmed preconditions and human approval (see risk-categories).
6. Under uncertainty about risk, stop and escalate rather than proceed.

## The mindset

Treat every production change as if a real person is on the other end right now — because they usually are. Caution here is not slowness for its own sake; it is respect for the people relying on the system. The specific list of what is most fragile in your current project is in its context document — read it before you act.
