# 07 — Pre-Implementation Architecture Review

Before implementing a substantial change, perform an architecture/design review.

Do NOT implement the change yet.

When available, read the outputs of **10 — CR Impact Analysis**, **12 — Legacy Change Safety Assessment**, and **14 — NRT Test Impact Analysis**, plus `docs/architecture/REPOSITORY_VISIBILITY.md`. Use them as inputs, but re-verify material assumptions against the source.

## Analyze

1. Current architecture relevant to the requested change.
2. Existing components that should own the new behavior.
3. Affected modules/classes/packages.
4. Existing interfaces and extension points.
5. Data model and persistence implications.
6. Transaction/consistency implications.
7. Concurrency implications.
8. External integration implications.
9. Security/authorization implications.
10. Configuration/deployment implications.
11. Error/retry/idempotency behavior.
12. Performance/resource implications.
13. Observability and operational requirements.
14. Testing strategy.
15. Backward compatibility.

## Design

Propose one or more viable implementation approaches.

For each approach describe:
- affected components
- important changes
- advantages
- disadvantages
- risks
- migration/compatibility considerations

Do not rank approaches as "best" based on subjective preference. Instead explain the trade-offs and the conditions under which each approach fits.

Then provide a concrete implementation plan:
- files/components likely to change
- sequence of changes
- tests to add/update
- documentation that should be updated
- rollout considerations
- rollback considerations

Clearly separate facts about the current system from proposed design decisions.

## Legacy-specific design checks

Before coding, verify:
- whether an existing module-local pattern should be extended instead of introducing a new abstraction
- whether shared classes create cross-project blast radius
- whether Oracle changes affect Hibernate and JDBC consumers differently
- whether Swing work can block the EDT
- whether wrapper-framework hooks/security context must be preserved
- whether build/package changes affect unrelated projects
- whether Ops workflows, reports, audit/history, or downstream processing change
- whether rollback is practical in the existing deployment model

## Legacy/domain/test constraints

Before selecting the implementation approach, explicitly account for:
- existing application domain invariants supported by code
- NRT cases that currently protect the behavior
- NRT coverage gaps that the implementation may need to close
- testability of the proposed design
- dates/calendars, precision/rounding, state transitions, reconciliation, audit, approvals, batch, and duplicate-processing behavior where applicable

Do not invent domain rules or accept prior analysis blindly; verify material assumptions against the source.
