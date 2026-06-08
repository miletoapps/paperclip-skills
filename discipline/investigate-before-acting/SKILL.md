# Investigate Before Acting

Before proposing a plan, writing code, or executing any change, ALWAYS inspect the real current state of the system. Never assume, guess, or infer when you can verify. Wrong assumptions cost far more than the minutes spent checking — especially when live systems and real users are involved.

This is a foundational discipline for every agent on every task. It is never optional.

## When to use

- At the start of ANY task, before planning
- Before stating "the code does X" or "the config is Y"
- Before proposing a fix for a bug
- Whenever you catch yourself about to write "should be", "probably", "I assume", "likely", "I think it's"
- Before answering any question about how something currently works

## When NOT to use

- For stable general knowledge (language syntax, framework concepts) that does not depend on the specific repo or environment state
- When the operator explicitly says "don't investigate, draft something quick" — but even then, flag every assumption you make

## The core rule

If a claim is testable against the actual system, test it. Do not state it as fact until verified.

Claims you must verify, never assume:
- "This column is named X" → query the schema / `information_schema`
- "This enum has values A, B, C" → query `pg_enum` / read the type definition
- "This function does X" → read the source
- "This env var is set" → check the actual environment
- "This file imports Y" → read/grep the file
- "The branch is up to date" → `git status`, `git log`
- "The change worked" → check health/status; never assume success

## How to investigate (toolkit)

- **Read files in full** before editing — not just a snippet around the change
- **grep / search** for every usage, definition, and reference
- **Query the database** for real schema and real row counts
- **Check git state** before pushing or deploying
- **Inspect runtime** (logs, process status, health) before claiming something works
- **Read the project context documents** as a map for the non-discoverable (history, people, business decisions, known traps) — then verify anything technical they claim
- **Trace the full pipeline** end to end when a change might ripple (UI → API → DB → jobs → external services)

## Hierarchy of evidence

1. **The live system is the only source of technical truth** — code in the repositories, the real database, configurations, logs, runtime behavior. Every technical fact is verified there.
2. **Project context documents are MAPS, not authority.** They exist for what cannot be discovered by investigating the system: project history, people, business decisions and their reasons, infrastructure topology, known sensitive zones, board conventions. Use them to orient yourself — never as proof of a technical fact.
3. **When a document conflicts with the live system, the system wins.** Report the divergence (comment on the issue) so the document gets corrected. Documents converge toward the truth; they never override it.

## When you cannot verify (ask → research → declare)

When you hit a question you cannot answer from the system:

1. **Is it technically discoverable?** Then investigate with real data: read the code, query the database, check logs, inspect git history, run a controlled test. Exhaust this before anything else.
2. **Is it about intent, business, or history** (not discoverable in any system)? Ask the human — a precise, specific question, before proceeding.
3. **Human doesn't know?** Go research it with data: deeper system archaeology, external documentation of the tools involved, reproducible experiments.
4. **Still unresolved?** State the uncertainty explicitly and proceed only with what is proven — scope the work to avoid depending on the unknown.

At no point is a gap filled with assumption. "Probably", "should be", and "I imagine" are not evidence.

## Depth expectation

Shallow investigation is the same as no investigation. Read the whole relevant file. Follow the call chain. Check the actual data. The goal is to understand the system as it truly is, not to confirm a guess you already made. When two explanations both fit the surface evidence, dig until the more specific evidence rules one out.

## Invariants you must preserve

1. **Distinguish fact from hypothesis explicitly.** Say "hypothesis:" when you must guess.
2. **Read before write.** Never edit a file you have not read in full.
3. **Verify after acting.** Confirm the change did what you intended.
4. **No guessing identifiers.** Names, paths, signatures, hostnames — look them up.
5. **One verified fact beats three plausible assumptions.**
6. **Documents are maps, not truth.** Technical facts come from the live system; document-vs-system divergences are reported, and the system always wins.
7. **Gaps are closed by asking and researching — never by assuming.** Discoverable → investigate with data. Intent/business → ask the human. Unknown after both → declare the uncertainty and scope around it.

## The failure mode this prevents

The most damaging failure: editing based on what you imagine the code does, shipping it, and discovering in production that the real code was different. This breaks trust and risks live systems. The remedy is always the same — investigate first, thoroughly.
