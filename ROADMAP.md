# Public Roadmap

This roadmap describes intended directions, not guaranteed delivery dates.

AgentLink's root goal is to turn an ordinary chat thread into a durable AI-agent execution slot: the user starts from chat, while useful work can continue across physical model turns, interruptions, devices, tools, and worker handoffs until the bounded job is actually complete.

Reliability, receipts, idempotency, worker leases, and approval state exist to support that larger continuity goal.

## Now

- make chat-originated jobs resumable across physical model turns
- harden durable job / thread / checkpoint state outside conversational context
- expand the public Chat Long-Turn Continuity Demo and keep its dedicated CI green
- prove worker handoff resumes pending work instead of restarting completed work
- harden durable effect / receipt semantics so interrupted turns do not duplicate external actions
- distinguish unknown, failed, completed, and deliberately-abstained outcomes
- keep authority / approval state explicit and bounded during longer execution
- improve worker capability / availability handling
- recruit initial design partners with workflows that naturally outlive one response

## Next

- publish longer deterministic turn chains and explicit turn-budget scenarios
- demonstrate stale-owner recovery and intentional worker/lane handoff in public fixtures
- connect continuity proofs to safe real tool/browser/device demonstrations without exposing private runtime internals
- quantify continuity quality with failure injection and interruption matrices
- improve observability and audit exports for cross-turn execution
- evaluate multi-worker conflict-control strategies
- add model/provider lanes while keeping the execution substrate model-agnostic
- perform structured threat modeling and security review

## Later

- richer chat-native long-running execution profiles
- broader cloud / edge / device worker portability
- richer policy, authority expiry, delegation, and revocation controls
- external developer / partner interfaces for bounded worker capabilities
- standardized evaluation harness for long-running chat-native agent execution
- deployment profiles for teams that need durable work to survive model, browser, device, or service boundaries

## Public proof priorities

Public work should make the root thesis understandable without requiring access to the private production core.

Priority proof surfaces include:

1. **Chat Long-Turn Continuity** — a job survives fresh physical turns/processes and resumes from durable state.
2. **Worker handoff** — another worker claims the same job and continues pending work without replaying completed steps.
3. **Effect reconciliation** — an interrupted external effect is not blindly repeated when a receipt already proves it occurred.
4. **Bounded authority** — longer execution does not imply unlimited capability or bypass positive human/authentication gates.
5. **Inspectable evidence** — checkpoints, receipts, ownership changes, and completion remain understandable after interruption.

## Success signals

The project should be judged by measurable execution quality, not feature count alone:

- useful work completed across more than one physical chat/model turn
- successful resume rate from durable state
- percentage of resumptions that avoid restarting completed work
- worker handoff success rate
- duplicate external side-effect rate
- uncertain-outcome reconciliation rate
- human intervention rate
- reliable permission / approval enforcement
- successful third-party onboarding
- real design-partner use in bounded workflows

A useful north-star question is:

> Can someone start a real job from ordinary chat and trust that the job, its evidence, and its bounded authority survive longer than one response?
