# Technical Proof Inventory

This page separates **publicly reproducible evidence** from broader evidence categories that exist only in the private AgentLink development environment. It deliberately avoids publishing internal code, private infrastructure details, credentials, sensitive operational state, or security-relevant topology.

AgentLink's root claim is about chat-native continuity: a job started from an ordinary chat control surface should be able to outlive one physical model turn and continue from durable operational state.

## Publicly reproducible proof

### 1. Chat Long-Turn Continuity Demo

Public surface:

`demos/chat-long-turn-continuity/`

What it demonstrates:

- one bounded job persists outside a single Python process
- several fresh `chat-turn-*` processes continue the same durable job
- completed steps remain completed across turns
- a deliberate interruption occurs after an external-effect receipt is recorded but before step completion is recorded
- a later continuation loads the same durable state
- the receipt is reconciled rather than replaying the external effect
- final `effect_count` remains `1`
- worker ownership and `lease_epoch` survive as inspectable state
- an execution timeline remains available after handoff

Run:

```bash
cd demos/chat-long-turn-continuity
python3 run_demo.py
python3 -m unittest -v test_continuity_demo.py
```

CI evidence:

- dedicated workflow: `.github/workflows/chat-long-turn-continuity.yml`
- the workflow executes the fresh-process story and its regression tests
- implementation PR #25 passed the repository-wide Full Python suite before merge

Release:

`chat-long-turn-continuity-v0.1.0`

Browser visualization:

https://paper-daemon.github.io/agentlink-continuity/

The browser version uses localStorage as a deliberately simple durable-state stand-in so a visitor can interrupt the flow, reload the page, and resume the same public contract without installing anything.

**Claim boundary:** this proves the public continuity contract in deterministic simulators. It does not claim that the public JSON/localStorage implementations are the private production AgentLink runtime or undocumented ChatGPT internals.

### 2. Receipt Replay Simulator

Public surface:

`demos/receipt-replay-simulator/`

What it demonstrates:

- `COMPLETED` effects are not repeated
- `NOT_STARTED` work may retry
- `UNCERTAIN` work stops for reconciliation
- positive authentication boundaries stop execution
- cooldown boundaries defer execution
- a recorded completed effect takes precedence across current attempt boundaries

This is a focused reliability primitive beneath the broader chat-continuity goal.

Release:

`receipt-replay-simulator-v0.1.0`

### 3. Worker Lease Recovery

Public surface:

`demos/worker-lease-recovery/`

This is a smaller proof surface around worker ownership / recovery concepts. It supports the larger question of how a later worker can continue durable work when a previous owner disappears or becomes stale.

## Private-development evidence categories

The following categories describe active private implementation / test directions. They should not be interpreted as public proof until a reproducible public surface is linked.

### Persistent execution

Private development includes mechanisms and tests around durable work state, long-running execution, checkpoints, and resume behavior across real chat / worker / device boundaries.

### Action receipts

Development includes append-oriented execution receipt concepts intended to make completed work auditable and reduce unsafe replay.

### Failure replay / recovery

Recovery work includes distinguishing interrupted work from already-completed actions and using receipts when reconstructing execution state.

### Capability leases

Worker capability and availability can be represented as time-bounded state so routing does not rely indefinitely on stale worker assumptions.

### Stale-owner recovery

Long-running execution needs a way to recover ownership when a worker or generation disappears without cleanly releasing a job.

### Cloud / remote worker activity

AgentLink development includes remote-worker paths and persistent availability / heartbeat concepts for extending execution beyond one local process or machine.

### Parallel coordination

The project is exploring lane ownership, locking, conflict reduction, and handoff behavior for multiple concurrent workers.

## Next stronger public proofs

Public evidence should prefer deterministic measurements over screenshots alone. Useful next steps include:

- longer physical-turn chains
- explicit worker-handoff regression coverage
- stale-owner recovery fixtures
- turn-budget exhaustion and later resume
- fault-injection matrices across checkpoint locations
- duplicate-action count under repeated interruption
- recovery / resume success rate
- authorization rejection / expiry tests
- multi-worker conflict scenarios
- p50 / p95 recovery time once a realistic public harness exists

## Publication policy

Technical proof should be published only when it can be shared without exposing:

- production endpoints
- private host information
- tokens or secrets
- sensitive authorization internals
- private customer / user data
- exploitable operational detail

The goal is to publish **credible, bounded evidence**. Every public claim should make clear what the proof actually demonstrates and where the private production boundary begins.
