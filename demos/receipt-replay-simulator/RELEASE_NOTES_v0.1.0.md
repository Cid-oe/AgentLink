# Receipt Replay Simulator v0.1.0

> Release-notes draft for the first scoped release of the public Receipt Replay Simulator.

## Scope

This release applies **only** to `demos/receipt-replay-simulator/`, which is independently published under the MIT License in that directory.

It is **not** a release of AgentLink's unpublished production core, and it does not grant a license to private AgentLink implementation code or infrastructure.

## Included reliability behavior

The simulator makes two small contracts executable and inspectable:

### Recovery after interruption

- `COMPLETED` → `SKIP_ALREADY_COMPLETED`
- `NOT_STARTED` → `RETRY`
- `UNCERTAIN` → `RECONCILE_MANUALLY`

An interruption, timeout, or lost connection is therefore not treated as proof that an external effect failed. When completion cannot be established, the demo stops at reconciliation instead of blindly replaying the action.

### Guarding a new external effect

- `CLEAR` → execution may proceed when no completed effect is recorded
- `POSITIVE_AUTH_GATE` → `STOP_FOR_AUTH`
- `COOLDOWN` → `DEFER_COOLDOWN`
- a previously recorded completed effect always wins and returns `SKIP_ALREADY_COMPLETED`, across every current `AttemptBoundary`

## Verification

From this directory:

```bash
python3 demo.py
python3 -m unittest -v
```

The implementation is dependency-free and uses Python's standard-library `unittest` suite.

The repository also runs the Receipt reliability tests and the full Python suite in GitHub Actions. The release tag should only be cut from a privacy-safe commit for which both workflows are green.

## Contribution surface

External bug reports, reproducibility cases, documentation fixes, and narrowly scoped code changes are welcome for this MIT-licensed demo. See `CONTRIBUTING.md` before opening a contribution.

Useful follow-up work includes:

- enum-complete table-driven recovery tests
- deterministic interrupted-effect failure-injection scenarios
- stronger reconciliation examples that remain offline and dependency-free

## Security and privacy boundary

Do not include credentials, private endpoints, customer data, production logs, internal topology, private AgentLink source, or confidential material in issues, pull requests, fixtures, screenshots, or examples.

## Release checklist

Before publishing `receipt-replay-simulator-v0.1.0`:

- confirm the tag points to rewritten privacy-safe history
- confirm Receipt reliability tests are green
- confirm the full Python suite is green
- re-run the demo locally or in an equivalent isolated environment
- verify the release description preserves the demo-only MIT license scope
- verify no secrets, personal data, private endpoints, or production implementation details were added
