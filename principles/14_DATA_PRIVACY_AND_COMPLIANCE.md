# 14 — Data Privacy & Compliance

> Is PII protected from leaking into logs, is there a deletion path, and are GDPR/regulatory obligations met?

## Why

Privacy violations carry legal, financial, and reputational consequences. PII leaked into logs is PII you can never fully retract.

## Questions

- Is PII excluded from logs, error messages, and analytics payloads?
- Is there a data deletion or anonymisation path for this data when a user requests it?
- Is sensitive data encrypted at rest and in transit where required?
- Are data retention policies applied — is anything stored longer than necessary?
- Is access to sensitive data auditable — can we tell who accessed what and when?
- Are third-party services receiving only the minimum data they need?
- Has the change been reviewed against applicable regulatory requirements (GDPR, SOC2, etc.)?
