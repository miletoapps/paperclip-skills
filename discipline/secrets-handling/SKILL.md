# Secrets Handling

Secrets — API keys, tokens, passwords, connection strings — must never be exposed in code, logs, commits, or PR diffs. A single leaked secret can compromise production systems and user data. This skill defines the non-negotiable rules for keeping secrets out of artifacts.

Applies to every agent on every task.

## When to use

- Whenever code touches an API key, token, password, or connection string
- Before committing any file
- When writing logs or debug output
- When configuring environment variables
- When reviewing a PR (scan the diff for leaked secrets)

## Hard rules (never break)

1. **NEVER commit** any file containing real secrets (`.env`, `.env.local`, `.env.production`, etc). These belong in `.gitignore`.
2. **NEVER hardcode** a secret in source. Read it from the environment or a secret store.
3. **NEVER log** a secret — not even partially, not even "just for debugging".
4. **NEVER place** a secret in a PR description, issue comment, or commit message.
5. **NEVER echo** a full secret back in plaintext when one appears in context.

## Where secrets belong

- Environment variables loaded at runtime (not committed)
- A secrets manager / vault when available
- A platform-managed environment config
- An `.env.example` may exist in the repo, but with PLACEHOLDER values only — never real ones

## Reviewing for leaked secrets

When reviewing, scan the diff for:
- Strings matching key patterns (`sk-`, `sk_`, `ghp_`, `github_pat_`, JWT `eyJ...`, long hex/base64 blobs)
- New `.env*` files being added
- Connection strings with embedded passwords
- Tokens left in test fixtures or comments

If found: reject, require removal, and require rotation of the exposed secret.

## If a secret leaks

1. Treat it as compromised immediately
2. Rotate it — generate new, revoke old
3. Update the secret store / env config
4. Restart whatever consumes it
5. If it was committed, it is in git history — rotation is mandatory, not optional

## Important boundary — do not police the operator

This skill is about keeping secrets out of committed artifacts (code, logs, commits, PRs). It is NOT about lecturing the human operator on their own credential hygiene in conversation. If an operator shares a credential with you directly and states they manage rotation themselves, respect that and move on — do not repeat security warnings they have already dismissed. Your responsibility is the artifacts you produce, not policing the human.

## Invariants you must preserve

1. No real secret in any committed file.
2. No secret in any log output.
3. `.env*` always gitignored; `.env.example` placeholder-only.
4. Leaked secret → rotate, never just delete-and-forget.
5. Keep secrets out of artifacts; do not lecture the operator.
