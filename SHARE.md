# Share AgentLink

AgentLink is an execution-layer project aimed at turning ordinary chat sessions into persistent, long-running AI-agent control surfaces. The production core remains private, while selected demos and proofs are published so the continuity and reliability ideas can be inspected, tested, and improved safely.

## One-line description

**AgentLink aims to let a normal chat thread become a long-running AI agent that can keep working across physical turns, interruptions, devices, and tools.**

## What the project is really about

The root problem is the mismatch between short-lived chat turns and real work that may take hours or days.

The intended experience is:

> I ask in chat, and the agent keeps working until the job is actually done.

That requires durable job/thread state, continuation across model-turn boundaries, real tool and device execution, bounded authority, receipts, worker coordination, and idempotent recovery.

## Flagship public demo

The MIT-licensed [Chat Long-Turn Continuity Demo](./demos/chat-long-turn-continuity/) shows the core continuity idea directly.

```bash
git clone https://github.com/paper-daemon/AgentLink.git
cd AgentLink/demos/chat-long-turn-continuity
python3 run_demo.py
```

The demo launches separate fresh Python processes for multiple `chat-turn-*` continuations. It deliberately interrupts the process after an external-effect receipt is written but before the step is marked complete. A later continuation loads the same durable state, finds the receipt, and completes the job without replaying the effect.

No credentials, external services, or third-party Python packages are required.

## Useful links

- Repository: https://github.com/paper-daemon/AgentLink
- Flagship demo: https://github.com/paper-daemon/AgentLink/tree/main/demos/chat-long-turn-continuity
- First scoped release: https://github.com/paper-daemon/AgentLink/releases/tag/receipt-replay-simulator-v0.1.0
- Reliability primitive: https://github.com/paper-daemon/AgentLink/tree/main/demos/receipt-replay-simulator
- Good first issues: https://github.com/paper-daemon/AgentLink/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22
- External contributor example: https://github.com/paper-daemon/AgentLink/pull/20

## Technical framing

A useful question behind AgentLink is:

> Can an ordinary chat thread become a durable agent execution slot instead of ending at each model response?

The flagship demo isolates that contract into something reproducible: conversational process state can disappear while durable operational state survives and later workers continue from the latest checkpoint.

A second question is what happens when continuity breaks around an external side effect. AgentLink treats **unknown as different from failed** so completed effects are not blindly replayed.

## Community-post version

I’m building AgentLink around a simple idea: a normal chat thread should be able to become a real long-running AI-agent execution slot.

Chat models are good at reasoning and tool use, but real operational work often outlives one response. AgentLink is aimed at keeping that work moving across physical turns, interruptions, browser loss, devices, worker handoffs, and external services while preserving durable operational state outside any one model response.

I just published a dependency-free MIT demo that shows the continuity contract directly. A bounded job moves across fresh processes, an external effect is deliberately interrupted after its receipt is written, and a later continuation resumes without replaying the effect.

The repo has also received and merged an external contributor PR, and the first scoped public release is live.

I’d especially value feedback from people working on agent runtimes, tool orchestration, long-horizon automation, or chat-native agents.

Repo: https://github.com/paper-daemon/AgentLink

## Short social version

Building AgentLink to turn an ordinary chat thread into a **long-running AI-agent execution slot**.

The new public MIT demo shows a job surviving across fresh physical turns/processes, including an intentional interruption after an external effect. The next continuation resumes from durable state and does not replay the effect.

Chat should be able to outlive one response.

https://github.com/paper-daemon/AgentLink

Feedback, failure cases, and stars are welcome if this is a problem you care about.

## Sharing boundary

Please do not describe the unpublished production AgentLink core as open source. Public contribution surfaces are independently licensed where stated, including the Chat Long-Turn Continuity Demo and Receipt Replay Simulator under MIT.

Do not coordinate votes, fake engagement, or manipulate ranking systems. Share the project because the technical problem is relevant, and let readers decide whether it deserves a star.
