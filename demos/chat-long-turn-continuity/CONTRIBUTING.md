# Contributing to the Chat Long-Turn Continuity Demo

Thanks for helping test the public continuity contract behind AgentLink.

This directory is independently MIT licensed. The unpublished AgentLink production core is not part of this contribution surface.

## Good contribution areas

Useful, narrow contributions include:

- worker-handoff regression tests
- stale-owner / lease-expiry scenarios
- longer checkpoint chains across fresh processes
- deterministic interruption and resume cases
- stronger assertions that completed work is not restarted
- additional receipt / reconciliation edge cases
- clearer timeline output or documentation
- portability fixes that keep the demo dependency-free

Start with the repository's `good first issue` queue when possible:

https://github.com/paper-daemon/AgentLink/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22

## Run locally

```bash
cd demos/chat-long-turn-continuity
python3 run_demo.py
python3 -m unittest -v test_continuity_demo.py
```

No credentials, network services, or third-party Python packages are required.

## Reliability rules to preserve

A contribution should not weaken these invariants without explicit evidence and discussion:

- a new physical process may continue the same durable job
- completed steps are not restarted from zero
- an interruption is not automatically proof that an external effect failed
- a recorded effect receipt prevents blind replay
- worker ownership / handoff remains inspectable in durable state
- the execution timeline stays deterministic enough to test

## Pull requests

Prefer one focused change with a clear regression test.

Please include:

1. what behavior changed
2. why the change matters to continuity
3. how you reproduced or tested it
4. any new failure case introduced by the test

Keep the change inside this independently licensed demo unless the linked issue explicitly requires another public surface.

## Privacy and security boundary

Do not add:

- credentials or tokens
- private endpoints or internal URLs
- hostnames or network topology
- user/customer data
- production logs
- private AgentLink source or runbooks
- screenshots containing unrelated personal data

If a finding depends on sensitive private details, sanitize it before posting publicly.

## Scope honesty

This simulator demonstrates a continuity contract. It does not claim to reproduce undocumented ChatGPT internals or the private production AgentLink runtime.

Keep public claims tied to behavior that the demo and tests actually reproduce.
