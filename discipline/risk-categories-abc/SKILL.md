# Risk Categories (A / B / C)

Every development task must be classified into one of three risk categories BEFORE any code is written. The category determines who approves the work and how it flows from idea to production. This skill teaches the METHOD of classification — the universal rules, defaults, and flows. The concrete list of what is critical in a given project lives in that project's context document, not here.

Applies to every agent: those who plan, those who execute, and those who review.

## When to use

- When receiving any new development task
- When decomposing a backlog into sub-tasks
- When reviewing a PR (verify the declared category is correct)
- When deciding whether a change needs human approval

## The three categories

### Category A — Fully automated
Low-risk, mechanical, or cosmetic changes. Examples (general): linting, formatting, documentation edits, a refactor confined to a single file, patch/minor dependency bumps, new tests that do not change production behavior, purely cosmetic UI tweaks.

Flow:
1. Engineer opens a PR titled with the `[A]` prefix
2. A reviewer reviews and, if it passes, approves and merges
3. Human sees it afterward (daily summary / at deploy)

No human in the loop before merge, by design.

### Category B — Human approves the PLAN before execution
Medium-risk changes: a new feature, a multi-file refactor, a new route/endpoint, a major dependency bump, significant (non-cosmetic) UI, new business logic.

Flow:
1. A Plan Issue is opened BEFORE any code, describing: context, scope, files affected, technical decisions, risks, acceptance criteria
2. A human approves the plan in text — without reading any code
3. The engineer implements
4. A reviewer approves the PR (titled `[B]`)
5. Merge; human sees it at deploy

Human approves the idea; agent executes; agent reviews.

### Category C — Human approves the PR before merge
High-risk or irreversible changes. The concrete, closed list of what counts as Category C is defined per project in its context document. Universally, treat as Category C anything involving: database schema/migrations, authentication/authorization, money/billing, critical external integrations, production environment variables, irreversible operations (mass delete, drop), and any change that directly affects live customers.

Flow:
1. Engineer opens a PR titled `[C]`
2. Reviewer reviews and marks "Category C — awaiting human"
3. A human approves the PR directly
4. Merge; human controls deploy

A human is ALWAYS in the loop before Category C reaches production — even if the reviewer considers the code flawless.

## Classification rule (conservative defaults)

- Unsure between A and B → choose B
- Unsure between B and C → choose C
- Cannot decide alone → escalate to the human and ask
- NEVER underestimate risk. Asking for an unnecessary approval is cheap; breaking production is not.

## When scope changes mid-task

If a task that started as one category crosses into a higher one during execution (e.g. an "A" cosmetic change turns out to require a schema tweak), STOP, re-classify to the higher category, and follow its flow. Do not continue under the old, lower category.

## Invariants you must preserve

1. Category prefix (`[A]`/`[B]`/`[C]`) in every PR title. No prefix → rejected.
2. Category C never merges without a human — no exceptions.
3. Category B's plan is approved BEFORE code exists, not after.
4. Conservative default always wins under uncertainty.
5. Re-classify when scope grows; never smuggle higher-risk work under a lower category.

## Where the project-specific list lives

To know exactly which files, tables, workflows, or integrations are critical (Category C) in the project you are working on, read that project's context document. This skill gives you the method; the document gives you the specifics.
