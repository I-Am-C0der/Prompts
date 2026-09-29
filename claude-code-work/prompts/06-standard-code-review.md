# 06 — Standard Code Review

Perform a thorough code review of the current change/PR.

Before reviewing:
- Read `CLAUDE.md`.
- Read the relevant architecture documentation.
- Verify important assumptions against the source code.
- Inspect the complete change and relevant surrounding code.

## Review for

- correctness and functional regressions
- architectural violations
- broken module boundaries
- unexpected coupling
- API/contract changes
- database/query problems
- transaction and consistency issues
- concurrency/thread-safety problems
- error handling and failure paths
- retry/idempotency behavior
- security issues
- performance regressions
- resource leaks
- caching problems
- configuration/environment issues
- observability gaps
- backward compatibility
- missing or inadequate tests

## Output format

Report findings only when they are actionable and supported by the code.

For each finding include:

**[SEVERITY] Short title**
- File/line or precise location
- What is wrong
- Why it matters
- Concrete remediation

Use:
- CRITICAL
- HIGH
- MEDIUM
- LOW

Then provide:

### Review summary
- overall areas reviewed
- test/verification observations
- important residual risks
- questions that require clarification

Do not modify files unless explicitly asked.
Do not report stylistic preferences as defects unless they violate an established project convention or create a concrete problem.

## Legacy-specific review emphasis

When a changed file belongs to a shared/common project, trace its consumers before deciding the change is local.

For DB changes, review ORM and JDBC callers plus the real transaction boundary.

For Swing changes, review EDT and background-worker behavior.

For wrapper-framework changes, verify the framework's security and lifecycle behavior.

Prioritize evidence-backed data-integrity, operational-correctness, security, shared-runtime, and broad-regression findings above stylistic differences between modules.
## JUnit NRT review

For every functional change, explicitly inspect the relevant module's non-regression test module.

Determine:
- which existing JUnit cases protect the changed behavior
- whether those tests still assert the intended behavior
- whether negative/error/recovery cases are represented
- whether shared-code changes require NRT coverage in additional modules
- whether the change introduces a regression path that the current NRT suite would not detect

When reporting a missing test, identify the appropriate existing NRT module/package and the scenario that should be covered. Avoid generic "add more tests" comments.

## Banking/domain-invariant review

Where applicable, verify existing application invariants involving:
- dates/calendars/cut-offs/time zones
- currency and unit semantics
- precision and rounding
- lifecycle/state transitions
- reconciliation/control totals
- audit/history
- approvals/entitlements
- batch/end-of-day dependencies
- duplicate processing

Only report defects when the repository and requirement provide evidence. Do not infer banking rules from domain intuition.

## JUnit NRT effectiveness

For relevant NRT tests, verify that the tests actually exercise the changed path and assert the behavior that could regress.

Look specifically for:
- weak or incidental assertions
- tests that do not reach the changed branch
- over-mocking that bypasses relevant logic
- missing boundary/error/rollback assertions
- environment-dependent behavior
- fixtures/setup that bypass the important production condition

When identifying missing coverage, name the relevant NRT module/package and scenario.
