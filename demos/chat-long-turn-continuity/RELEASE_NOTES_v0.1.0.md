# Chat Long-Turn Continuity Demo v0.1.0

First scoped release of the public demo that most directly represents AgentLink's root mission: turning an ordinary chat slot into a durable AI-agent execution slot that can continue useful work beyond one physical model turn.

## Scope

This release applies **only** to `demos/chat-long-turn-continuity/`, which is independently published under the MIT License in that directory.

It is not a release of AgentLink's unpublished production core and does not expose private runtime source, endpoints, topology, credentials, user data, or internal runbooks.

## What the demo shows

- a chat-originated bounded job persists durable state outside one process
- separate `chat-turn-*` workers continue the same job across fresh Python processes
- already-completed steps are not restarted from zero
- an external-effect receipt is written before a deliberately simulated turn/process loss
- the next continuation sees the durable receipt and completes without replaying the effect
- an inspectable timeline records job creation, worker claims, completed steps, the effect receipt, reconciliation, and final completion

## Run

```bash
cd demos/chat-long-turn-continuity
python3 run_demo.py
```

No credentials, external services, or third-party Python packages are required.

## Test

```bash
python3 -m unittest -v test_continuity_demo.py
```

The implementation PR also passed the repository-wide Full Python suite before merge.

## Why this matters

The demo isolates one core AgentLink contract: conversational process state may disappear while durable operational truth survives. A later physical turn or worker should be able to continue from that state rather than reconstructing the job from scratch.

Reliability primitives such as receipts and idempotent recovery support this larger goal of chat-native long-running agent execution.
