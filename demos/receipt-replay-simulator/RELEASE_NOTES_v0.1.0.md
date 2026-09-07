# Receipt Replay Simulator v0.1.0

First scoped release of the public Receipt Replay Simulator.

## Scope

This release applies **only** to `demos/receipt-replay-simulator/`, which is independently published under the MIT License in that directory.

It is **not** a release of AgentLink's unpublished production core, and it does not grant a license to private AgentLink implementation code or infrastructure.

## Included reliability behavior

The simulator makes two small contracts executable and inspectable.

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

The latest code-changing commit for this demo passed both the Receipt reliability tests and the full Python suite. Subsequent release-preparation changes are documentation-only.

## Contribution surface

External bug reports, reproducibility cases, documentation fixes, and narrowly scoped code changes are welcome for this MIT-licensed demo. See `CONTRIBUTING.md` before opening a contribution.

Useful follow-up work includes:

- enum-complete table-driven recovery tests
- deterministic interrupted-effect failure-injection scenarios
- stronger reconciliation examples that remain offline and dependency-free

## Security and privacy boundary

Do not include credentials, private endpoints, customer data, production logs, internal topology, private AgentLink source, or confidential material in issues, pull requests, fixtures, screenshots, or examples.
