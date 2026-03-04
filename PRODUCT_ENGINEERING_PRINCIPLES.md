# Product Engineering Principles

> Sixteen dimensions of quality, applied across every phase of the product development lifecycle.
>
> **Tech stack:** Elixir · Phoenix LiveView · React · PostgreSQL · Tailwind CSS

---

## The Lifecycle Phases

| Phase                             | Core mindset                                                     |
| --------------------------------- | ---------------------------------------------------------------- |
| **Design**                        | Are we solving the right problem the right way?                  |
| **Implementation**                | Am I building this correctly, safely, and completely?            |
| **Code Review**                   | Does this work meet the standard across all dimensions?          |
| **Release & Rollout**             | Can we ship this safely and reversibly?                          |
| **Monitoring & Maintenance**      | Is this holding up in production?                                |
| **Debugging & Incident Response** | Where did we fall short, and how do we find the root cause fast? |
| **Extending & Iterating**         | Can we change this safely and confidently?                       |

---

## The Sixteen Dimensions

| #   | Dimension                            | What it means                                                                                                         |
| --- | ------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| 1   | **Organisational Alignment**         | Does this work align with the broader org goals, and is it the right thing to be working on right now?                |
| 2   | **Business Logic & Intent**          | Does the work solve the right problem, and is the intent explicit and traceable?                                      |
| 3   | **Testing**                          | Is there proof the system behaves as intended — across happy paths, sad paths, and edge cases?                        |
| 4   | **Data Model & Schema Design**       | Does the schema faithfully represent the domain, with constraints enforced at the database level?                     |
| 5   | **Database Operations & Migrations** | Are migrations safe against production data, and are queries performant?                                              |
| 6   | **Error Handling & Propagation**     | Are errors explicit, propagated to the right boundary, and translated into something meaningful?                      |
| 7   | **Observability & Debuggability**    | Is the system instrumented well enough to diagnose production problems without deploying more logging?                |
| 8   | **Security & Authorization**         | Are access controls applied at the right layer, inputs sanitized, and tenant boundaries enforced?                     |
| 9   | **Performance & Scalability**        | Will this hold up under production load — bounded operations, efficient renders, no unnecessary work in the hot path? |
| 10  | **Code Quality & Simplicity**        | Is this the simplest correct solution, with clear naming and earned abstractions?                                     |
| 11  | **Maintainability & Changeability**  | Can a future engineer understand and safely modify this without understanding the entire system?                      |
| 12  | **API Design & Contracts**           | Are interfaces well-defined, consistent, and backward-compatible — both external and internal?                        |
| 13  | **UI Quality & Accessibility**       | Is the interface consistent, responsive, and accessible — with clear feedback, logical hierarchy, and usable by all?  |
| 14  | **Data Privacy & Compliance**        | Is PII protected from leaking into logs, is there a deletion path, and are GDPR/regulatory obligations met?           |
| 15  | **Reliability & Resilience**         | Can the system handle partial failures gracefully — with retry safety, idempotency, and no silent data loss?          |
| 16  | **Communication & Rollout**          | Do the right people know about this change, and is the rollout incremental and reversible?                            |

---
