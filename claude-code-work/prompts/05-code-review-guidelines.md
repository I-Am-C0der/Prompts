# 05 — Create Project-Specific Code Review Guidelines

Create `docs/architecture/CODE_REVIEW_GUIDELINES.md`.

The goal is to establish review guidance specific to this application rather than generic software-engineering advice.

## Rules

- Derive the guidance from the actual source and architecture documentation.
- Do NOT modify application source code.
- Do not create generic checklist noise.
- Focus on failure modes that matter for this codebase.
- Explain why each project-specific check matters where useful.

Cover, as applicable:

1. Architecture and dependency boundaries.
2. Module/package responsibilities.
3. API contracts and compatibility.
4. Database access and query behavior.
5. Transaction boundaries and consistency.
6. Concurrency/thread safety.
7. Error handling and exception propagation.
8. Retries, idempotency, and failure recovery.
9. Security/authentication/authorization.
10. Input validation and data integrity.
11. Performance and resource usage.
12. Caching.
13. External integrations.
14. Configuration and environment differences.
15. Logging, metrics, tracing, and observability.
16. Tests and regression coverage.
17. Backward compatibility.
18. Deployment/operational concerns.
19. Known fragile areas from `KNOWN_ISSUES.md`.

Define practical review severity guidance:

- CRITICAL
- HIGH
- MEDIUM
- LOW

Severity should reflect impact and likelihood in this specific application, not generic stylistic preferences.


## Legacy-team review principle

Because approximately 75 developers have worked across the application, different modules may legitimately use different patterns. Do not enforce stylistic uniformity merely for consistency.

Flag a deviation when it creates a concrete defect, violates a verified local/framework contract, weakens security/data integrity, increases regression risk, or materially harms maintainability.

Add explicit review checks for shared consumers, Java 8 compatibility, Swing EDT safety, Oracle locking/transactions, mixed Hibernate/JDBC behavior, wrapper-framework security/lifecycle, Ops workflow impact, reports, audit/history, and cross-module regression.
## JUnit non-regression testing

Treat NRT coverage as part of code-review analysis.

Review whether:
- the changed behavior is covered by an existing JUnit NRT case
- an existing test must be updated because expected behavior changed
- a new NRT case is required because the behavior is genuinely new
- relevant negative/error/recovery paths are covered
- shared/common code changes require NRT coverage beyond the named module
- DB-dependent tests exercise the actual persistence behavior relevant to the change
- test setup/fixtures hide important production assumptions

Do not accept "tests exist" as sufficient evidence. Check that the tests exercise the affected behavior.

## Banking/domain-invariant review

Where applicable, review changes against existing application evidence for:
- business/trade/settlement/value dates
- holiday/calendar/cut-off/time-zone behavior
- currency and unit semantics
- decimal precision and rounding
- state transitions and lifecycle invariants
- reconciliation/control totals
- audit/history
- approval/entitlement rules
- end-of-day or batch dependencies
- duplicate-processing prevention

Do not invent domain rules. Verify the existing rule and the CR requirement from repository evidence.

## NRT test-effectiveness review

When evaluating regression tests, check whether a test can actually detect the failure the change could introduce.

Look for:
- assertions that do not verify the changed outcome
- tests that do not reach the changed branch
- over-mocking that bypasses the relevant behavior
- environment-dependent behavior presented as deterministic
- missing boundary/error/rollback assertions
- fixtures that hide the important production condition

Do not criticize test style without identifying a concrete regression that could escape detection.
