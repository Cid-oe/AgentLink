# Share AgentLink

AgentLink is a public technical showcase for reliability infrastructure around long-running AI workers. The production core remains private, while selected demos and proofs are published so specific execution ideas can be inspected, tested, and improved safely.

## One-line description

**AgentLink explores persistent, permissioned and recoverable execution for long-running AI workers, with a public MIT-licensed demo for idempotent recovery after interrupted side effects.**

## 30-second demo

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

A useful question behind the public demo is:

> What should an agent do when a network interruption happens after an external side effect may already have occurred?

The demo treats **unknown as different from failed**. A completed effect is skipped, a definitely-not-started action may retry, and an uncertain effect stops for reconciliation rather than being blindly replayed.

## Community-post version

I’m working on AgentLink, an execution-layer project for long-running AI workers. One reliability rule I care about is that a timeout or disconnect should not automatically mean an external action failed.

I published a tiny MIT-licensed simulator that makes that behavior executable: completed effects are skipped, not-started actions may retry, and uncertain outcomes stop for reconciliation instead of blind replay. It runs locally with Python’s standard library only.

The project has also received and merged an external contributor PR, and the first scoped demo release is now public.

I’d especially value feedback on failure cases where this recovery model is too conservative or still permits duplicate side effects.

Repo: https://github.com/paper-daemon/AgentLink

## Short social version

Building AgentLink around one stubborn reliability rule for AI agents: **timeout ≠ proof of failure**.

The public MIT demo shows how to avoid blindly replaying external side effects after interruption. Runs locally in ~30 seconds, no credentials or dependencies.

First release is live, and an external contributor PR has already landed.

https://github.com/paper-daemon/AgentLink

If this is a problem you care about, feedback, failure cases, and stars are welcome.

## Sharing boundary

Please do not describe the unpublished production AgentLink core as open source. The independently licensed public contribution surface is explicitly identified in the repository, including `demos/receipt-replay-simulator/` under MIT.

Do not coordinate votes, fake engagement, or ask people to manipulate ranking systems. Share the project because the technical problem is relevant, and let readers decide whether it deserves a star.