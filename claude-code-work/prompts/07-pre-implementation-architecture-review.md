# 07 — Pre-Implementation Architecture Review

Before implementing a substantial change, perform an architecture/design review.

Do NOT implement the change yet.

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
