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
- **Read the project context documents** for known gotchas before diving in
- **Trace the full pipeline** end to end when a change might ripple (UI → API → DB → jobs → external services)

## Depth expectation

Shallow investigation is the same as no investigation. Read the whole relevant file. Follow the call chain. Check the actual data. The goal is to understand the system as it truly is, not to confirm a guess you already made. When two explanations both fit the surface evidence, dig until the more specific evidence rules one out.

## Invariants you must preserve

1. **Distinguish fact from hypothesis explicitly.** Say "hypothesis:" when you must guess.
2. **Read before write.** Never edit a file you have not read in full.
3. **Verify after acting.** Confirm the change did what you intended.
4. **No guessing identifiers.** Names, paths, signatures, hostnames — look them up.
5. **One verified fact beats three plausible assumptions.**

## The failure mode this prevents

The most damaging failure: editing based on what you imagine the code does, shipping it, and discovering in production that the real code was different. This breaks trust and risks live systems. The remedy is always the same — investigate first, thoroughly.
