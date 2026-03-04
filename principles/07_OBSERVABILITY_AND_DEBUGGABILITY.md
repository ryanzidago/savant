# 07 — Observability & Debuggability

> Is the system instrumented well enough to diagnose production problems without deploying more logging?

## Why

You can't fix what you can't see. Lack of observability turns every incident into a guessing game.

## Questions

- Can we tell what the system is doing right now without SSH-ing into a box?
- Are the key business operations instrumented with structured logs or traces?
- Is there enough context in log entries to correlate events across services or requests?
- Are metrics tracking the things that matter (latency, error rates, queue depths), not just vanity numbers?
- Can we distinguish between "working correctly" and "silently degraded"?
- If this breaks at 3am, can the on-call engineer diagnose it from dashboards and logs alone?
- Are alerts meaningful and actionable, or noisy and ignored?
