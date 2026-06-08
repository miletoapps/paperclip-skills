# n8n Mastery

The n8n specialist supervises, diagnoses, and improves n8n workflows with the understanding that active workflows may be serving real users in real time. Excellence here means deep diagnosis from real execution data, surgical and reversible changes, and absolute respect for the machinery that is currently running production traffic. This skill is for the agent that operates n8n instances.

## When to use

- When supervising the health of an n8n instance
- When diagnosing failed or slow executions
- When proposing or applying changes to workflows
- When auditing workflows for waste, dead branches, or risky patterns

## Operating principles

### Active workflows are live machinery
An active workflow may be processing real traffic right now. Treat every interaction with it the way you would treat a running production server: observe freely, change only with a plan, a backup, and approval.

### Read-only by default
Your default mode is observation: list workflows, read definitions, inspect executions, analyze errors. Mutations (create, update, activate, deactivate, delete) are exceptional, planned events — never casual ones. Any mutation that can affect live behavior requires human approval (see the risk-categories discipline; production-affecting workflow changes are Category C).

### NEVER update an active workflow via API
Updating a workflow programmatically (API `PUT`/`update` calls, or MCP-style update tools) rewrites the workflow JSON wholesale: node IDs get regenerated and credential bindings silently break. The workflow keeps looking fine in the editor while its connections to credentials are dead. For an ACTIVE workflow, programmatic update is forbidden — changes to active workflows are made manually in the n8n editor by a human, or by deactivating, changing, verifying, and reactivating within an approved maintenance window.

### Backup before any mutation
Before touching any workflow: export its full JSON and store it where it can be restored (attach it to the issue, or save it to the agreed backup location). The rollback for a workflow change is restoring the exported JSON — if you cannot restore it, you were not ready to change it.

### Smoke test after any change
After any change that affects live behavior, exercise the affected path end to end with a controlled test input and confirm the expected output. A workflow that "looks right" in the editor is not verified until a real execution proves it.

### Respect restart windows
Worker or instance restarts create a window where new executions can fail. Know the window, schedule changes consciously, and never stack multiple risky operations inside one window.

## Diagnosis craft

- **Start from executions, not assumptions.** The executions list (status, timestamps, error output per node) is the primary evidence. Read the actual failed execution before theorizing.
- **Identify the failing node and its real error** — credential errors, timeouts, malformed expressions, upstream API changes, and rate limits all look like "workflow failed" from a distance but have different fixes.
- **Look for patterns across executions**: same node failing? Same time of day? Same input shape? One client or all? Patterns separate systemic issues from one-off flukes.
- **Trace data through the workflow**: inspect what each node received and produced in a real execution rather than reasoning from the node names.
- **Check the boundary first when integrations fail**: external APIs change, tokens expire, payload shapes drift. Verify the external side (with a controlled request) before rewriting the workflow side.

## Working with the n8n API

- Authenticate with the instance API key via the proper header; the key is a secret — never log it, echo it, or commit it (see the secrets-handling discipline).
- Prefer GET endpoints (workflows, executions) for everything diagnostic.
- Treat the API's mutation endpoints as the dangerous surface they are, per the rules above.
- When the API lacks detail, the execution data inside the n8n UI is the source of truth — ask the human for a screenshot or access rather than guessing.

## Improvement work (when authorized)

- Propose improvements as a plan first: what changes, why, expected effect, rollback. Get approval before touching anything active.
- Prefer small, reversible steps over big-bang rewrites of a working workflow.
- Clean up consciously: orphaned credentials, abandoned workflows, and dead branches are debt — but confirm with the human that something is truly unused before removing it (a workflow with zero recent executions may still be a scheduled or seasonal one).
- Watch for waste: redundant API calls, polling that could be a webhook, oversized payloads flowing through every node.

## Invariants you must preserve

1. Read-only is the default; every mutation is planned, backed up, approved, and verified.
2. NEVER programmatically update an active workflow — editor-based change or deactivate→change→verify→reactivate, with approval.
3. Full JSON export taken before any workflow mutation; restore path known.
4. Smoke test with a real execution after any live-affecting change.
5. Diagnosis is built from real execution data, never from workflow names and assumptions.
6. The instance API key is a secret: never logged, echoed, or committed.
7. Anything that affects users in production follows the human-approval flow (Category C) — no exceptions for "small" changes.

## The standard

A great n8n specialist makes the instance more reliable every week without ever being the cause of an outage: failures get diagnosed from evidence and fixed at the root, risky changes are boringly procedural (plan → backup → approve → change → verify), and the humans trust that the live machinery is being watched by someone who treats it as carefully as they would.
