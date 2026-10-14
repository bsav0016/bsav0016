# A security and correctness review of my own projects

In October 2026 I audited my own portfolio before making more of it public. I found real problems: credentials committed to git history, an unauthenticated payment webhook, and rule bugs in a game server. This note covers what I found, how I handled it, and what I now do differently. I am publishing it because the history of these repositories shows the mistakes, and I would rather explain them than have a reviewer discover them.

## Summary

| Area | What I found | Impact | Resolution |
| --- | --- | --- | --- |
| Credentials in git history | A live Stripe key, Django `SECRET_KEY` values, an SSH private key, a hosted-database client key and certificate, and a market-data API key, across four backend repositories | The repositories were private, so exposure was limited. I treated every value as compromised anyway | Rotated every one, then published the repository that was meant to be public |
| Unauthenticated purchase webhook | A payment-provider webhook endpoint in AlgoTracker accepted any request | Anyone who could reach the server could credit an account for free (up to 10,000 credits per request) | Shared-secret header, constant-time comparison, fails closed, with tests |
| Game rule bugs | Server-side piece numbering was inverted, so a win credited the wrong player's rating; winners were stored as `"1"` or `"2"`; malformed input returned HTTP 500 | Wrong results in ranked online games | Fixed, covered with tests, and added draw detection |
| Dead and broken logic | The computer opponent's "block four in a row" step never ran, because it compared objects by identity | The AI was weaker than designed | Fixed and tested |
| Build bug | A dependency was only installed nested inside another, so Android native linking missed it and the app rendered a blank screen | Release builds from the lockfile could ship broken | Listed as a direct dependency |

## Timeline and how each problem surfaced

**Credentials.** I ran a secrets scan over all my repositories. Nothing sensitive was in the current code, but the history was another matter: the Stripe key had been committed in 2022 and removed in 2024, which does not remove it from history. I wrote a small history scanner (file, commit and rule only, never the value) and later ran gitleaks as well. The two tools disagreed usefully: gitleaks missed a hard-coded API key inside a JSON-style dictionary, and my own rules caught it. I now run both.

**The webhook.** I found it by reading the code before making the repository public, not by a scanner. The endpoint trusted the request body and credited whatever product it named. The production server was paused at the time, so it was not being exploited, but making the code public would have documented the hole. I fixed it before the flip.

**Game bugs.** I found these by writing the tests I had always skipped. One test failed because the first move on the board was stored as player 2.

**The build bug.** I hit it while taking screenshots. A local Android build rendered a blank screen, and the device log showed a native module that had never been linked.

## Decisions and tradeoffs

- **I rotated keys instead of rewriting history.** Rewriting history breaks every clone and fork, and it does not make a leaked secret safe, because anyone who already has it keeps it. Rotation is what actually neutralises a credential. The old values remain in history and are now dead.
- **I rotated the Stripe key with a grace period, not a delete.** I did not know whether the leaked key was also the one my live shop used. I rolled it with a short overlap, swapped the new value onto the server, tested a real checkout, and let the old key expire. Deleting first would have broken checkout.
- **I made the webhook fail closed.** If the secret is not configured, the endpoint rejects every request. A missing environment variable should never reopen the hole. The cost is that the secret must be set before deploying, and I documented the rollout order for that reason.
- **I kept deployment out of pull-request checks.** CI runs tests, linting and a build on every pull request. Releases stay a separate, deliberate step.
- **I let the type check report before I made it block.** The AlgoTracker app started with known type errors, and failing every pull request on old errors would have trained me to ignore the check. I fixed them afterwards and made the check required.

## What I do differently now

- Secret scanning with push protection is on for public repositories, and I run a history scan before changing any repository's visibility.
- Configuration comes from environment variables with explicit placeholders in `.env.example`. Production settings fail loudly if a required value is missing.
- Security-critical paths get tests that try to break them: forged webhooks, malformed input, wrong types and out-of-range values.
- Each application gets its own payment key and its own webhook secret, so one leak cannot affect another project, and rotating one is routine.
- CI actions are pinned to commit hashes, workflow permissions are read-only, and Dependabot raises updates.
- Where my GitHub plan allows it (public repositories), branch protection requires the checks to pass before merging into the default branch.

## Still true

- The rotated values are still visible in the git history of those repositories. They no longer work.
- These repositories have a single maintainer, so my own review is the only review. I would want a second pair of eyes on the webhook fix and the payment flow before putting real money through it again.

## How I worked

I did this work with an AI coding assistant (Claude Code) and reviewed and ran each change myself, including the key rotations on my own servers and accounts.
