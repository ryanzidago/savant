# 16 — Communication & Rollout

> Do the right people know about this change, and is the rollout incremental and reversible?

## Why

A good change shipped badly is a bad change. Surprises erode trust with users and teammates alike.

## Questions

- Have the people affected by this change (support, sales, other teams) been informed?
- Is the rollout incremental — can we ship to a subset of users first?
- Is the change reversible — can we roll back without data loss or broken state?
- Are feature flags or gradual rollout mechanisms in place where appropriate?
- Is there a runbook or checklist for the deployment, especially if it involves migrations or config changes?
- Are user-facing changes documented in release notes or changelogs?
- If something goes wrong during rollout, is the escalation path clear?
