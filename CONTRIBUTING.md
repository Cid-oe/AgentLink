# Contributing to AgentLink public surfaces

Thanks for taking the time to inspect or improve the public AgentLink repository.

AgentLink uses a deliberately mixed publication model: the production execution core remains private, while selected demos, tools, tests, architecture notes, and reproducible proofs are published here so reliability ideas can be inspected and improved safely.

## What is currently open for code contributions

The clearest independently licensed contribution surface is:

- `demos/receipt-replay-simulator/` — MIT licensed in that directory

Its local `CONTRIBUTING.md` contains run/test instructions and contribution guidance.

Other public directories may have their own license or scope statement. Do not assume that the repository root or unpublished AgentLink production core is licensed merely because a public file is visible.

If an issue explicitly invites a contribution, follow the license and scope stated for the affected public surface. When the licensing boundary is unclear, ask before copying, redistributing, or submitting a substantial code change.

## Good contributions

Useful contributions include:

- deterministic failure/recovery scenarios
- stronger idempotency and reconciliation tests
- portability improvements to independently licensed public demos
- reproducible bug reports
- narrow documentation corrections
- tests that make reliability invariants harder to regress

Prefer one focused change with a clear verification path over a large speculative rewrite.

## Before opening a pull request

1. Start from current `main`, especially after any repository-history maintenance.
2. Keep the change inside a clearly public/licensed surface unless an issue explicitly says otherwise.
3. Run the relevant local tests.
4. Do not add credentials, personal data, private endpoints, customer material, production logs, internal topology, contracts, private links, or unpublished AgentLink source.
5. Explain what changed, why it is useful, and how it was verified.
6. If AI assistance was materially used, it is fine to say so; the contributor remains responsible for the submitted code and test claims.

## Reliability rules to preserve

Several public examples intentionally model conservative execution behavior. Contributions should not weaken these rules without a strong, explicit reason and regression evidence:

- an interruption or timeout is not automatically proof of failure
- an uncertain external effect is reconciled rather than blindly replayed
- a recorded completed effect is not repeated
- a positive authentication boundary is not bypassed by credential guessing
- cooldowns and other positive abstention boundaries are respected

## Pull-request review

Maintainer review focuses on:

- reproducibility
- correctness of the reliability contract
- tests and failure cases
- privacy/security boundaries
- license/scope clarity
- whether claims are supported by executable evidence

A passing test suite is evidence for the behavior it exercises, not a claim that a toy demo has production-grade reliability.

## Security-sensitive findings

Do not put secrets, exploit-enabling private infrastructure details, or confidential material in a public issue or pull request. Use the repository's security guidance in `SECURITY.md` and keep public reports sanitized.

## Production core

The unpublished AgentLink production core is not part of the public contribution surface. Public examples may illustrate related concepts, but contributors should not infer private implementation details or attempt to reconstruct them from confidential information.
