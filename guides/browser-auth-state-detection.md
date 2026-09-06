# Browser auth-state detection without false logout alarms

Browser automation often fails when it treats a transient page title, one bad navigation, or a stale route as proof that an account is logged out.

A safer rule is to classify authentication from positive evidence.

## Authenticated

Treat the session as authenticated when the current DOM exposes account-only navigation or controls for the configured account, for example:

- Home / Profile / Notifications navigation that is only available after sign-in
- an authenticated composer or account menu
- a profile/account surface whose identity matches the configured target

One failed navigation should not override stronger authenticated DOM evidence.

## Logged out

Classify the session as logged out only when a positive login/signup gate is observed, such as:

- a sign-in form
- a login/signup interstitial
- an explicit provider-login requirement
- an account chooser that requires credentials before continuing

Do not invent or auto-enter credentials when the expected account is not already authenticated.

## Why this matters

False logout detection causes avoidable browser resets, account switching, duplicate tabs, and unnecessary credential prompts. In long-running agent workflows, that can turn a recoverable navigation failure into a destructive state change.

The practical contract is simple:

1. Observe the current DOM.
2. Prefer positive authenticated evidence over page-title heuristics.
3. Require a positive login gate before declaring `LOGGED_OUT`.
4. Keep account identity separate from route health.
5. Preserve idempotency so a recovery attempt cannot repeat an already-completed external effect.

This pattern is especially useful for social publishing, marketplace workflows, and any browser task where the session can remain authenticated while individual routes fail.