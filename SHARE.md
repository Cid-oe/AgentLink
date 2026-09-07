# Share AgentLink

AgentLink is an execution-layer project aimed at turning ordinary chat sessions into persistent, long-running AI-agent control surfaces. The production core remains private, while selected demos and proofs are published so the underlying continuity and reliability ideas can be inspected, tested, and improved safely.

## One-line description

**AgentLink aims to let a normal chat thread become a long-running AI agent that can keep working across physical turns, interruptions, devices, and tools.**

## What the project is really about

The root goal is not merely retry safety. AgentLink is trying to bridge the gap between short-lived chat turns and real work that may take hours or days.

The intended experience is simple:

> I ask in chat, and the agent keeps working until the job is actually done.

That requires durable job/thread state, resume across model-turn boundaries, real tool and device execution, bounded authority, receipts, worker coordination, and idempotent recovery.

## 30-second public demo

The current MIT-licensed public demo shows one small primitive needed for that larger goal: how an agent should recover when an external side effect may already have happened before a disconnect.

```bash
git clone https://github.com/paper-daemon/AgentLink.git
cd AgentLink/demos/receipt-replay-simulator
python3 demo.py
python3 -m unittest -v
```

No credentials, external services, or third-party Python packages are required.

## Useful links

- Repository: https://github.com/paper-daemon/AgentLink
- First scoped release: https://github.com/paper-daemon/AgentLink/releases/tag/receipt-replay-simulator-v0.1.0
- Receipt Replay Simulator: https://github.com/paper-daemon/AgentLink/tree/main/demos/receipt-replay-simulator
- Good first issues: https://github.com/paper-daemon/AgentLink/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22
- External contributor example: https://github.com/paper-daemon/AgentLink/pull/20

## Suggested technical framing

A broader question behind AgentLink is:

> Can an ordinary chat thread become a durable agent execution slot instead of ending at each model response?

One concrete reliability question inside that is:

> What should the agent do when a network interruption happens after an external side effect may already have occurred?

The public demo treats **unknown as different from failed**. A completed effect is skipped, a definitely-not-started action may retry, and an uncertain effect stops for reconciliation rather than being blindly replayed.

## Community-post version

I’m building AgentLink around a simple idea: a normal chat thread should be able to become a real long-running AI-agent control surface.

Today, chat models are good at reasoning and tool use, but operational work often outlives a single response. AgentLink is aimed at keeping that work moving across physical turns, interruptions, devices, browser loss, worker handoffs, and external services while preserving durable state outside any one conversation response.

The first public MIT-licensed demo focuses on one reliability primitive required for that: timeout does not automatically mean an external action failed. Completed effects are skipped, definitely-not-started work may retry, and uncertain outcomes stop for reconciliation instead of blind replay.

The project has already received and merged an external contributor PR, and the first scoped demo release is public.

I’d especially value feedback from people working on agent runtimes, tool orchestration, long-horizon automation, or chat-native agents.

Repo: https://github.com/paper-daemon/AgentLink

## Short social version

Building AgentLink to turn an ordinary chat thread into a **long-running AI-agent execution slot**.

The goal: work should survive model-turn limits, disconnects, browser loss, device changes, and worker handoffs instead of dying with one response.

First public MIT demo covers one key primitive: **timeout ≠ proof of failure**, so external effects are not blindly replayed after interruption.

v0.1.0 is live, and an external contributor PR has already landed.

https://github.com/paper-daemon/AgentLink

Feedback, failure cases, and stars are welcome if this is a problem you care about.

## Sharing boundary

Please do not describe the unpublished production AgentLink core as open source. The independently licensed public contribution surface is explicitly identified in the repository, including `demos/receipt-replay-simulator/` under MIT.

Do not coordinate votes, fake engagement, or ask people to manipulate ranking systems. Share the project because the technical problem is relevant, and let readers decide whether it deserves a star.