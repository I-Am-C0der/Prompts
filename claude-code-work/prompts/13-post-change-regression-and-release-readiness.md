# 13 — Post-Change Regression & Release Readiness

Assess a completed change for regression and release risk in this legacy investment-banking application.

**Do NOT modify source code.**

## Context

Known characteristics:
- Ops-facing investment-banking post-settlement application
- 15+ year legacy codebase
- Java 8 / Swing
- Oracle / Hibernate / JDBC
- shared wrapper framework
- multiple projects/modules in one traditionally built shared application
- heterogeneous module-level patterns

## Inputs

Use:
- CR/requirements
- final diff
- changed files
- architecture documents
- implementation notes
- tests already executed

## 1. Verify requirement coverage

Map:

| Requirement | Implementation | Test/verification evidence | Status |
|---|---|---|---|

Identify acceptance criteria without evidence.

## 2. Determine the true regression surface

Trace changed code to:
- callers
- implementors
- subclasses
- shared utilities
- dependent projects
- DB consumers
- reports
- integrations
- scheduled/batch jobs
- Swing workflows

Do not assume changed files define the regression boundary.

## 3. Build a regression matrix

| Area | Scenario | Why affected | Test type | Priority | Evidence/status |
|---|---|---|---|---|---|

Cover where relevant:
- primary workflow
- negative/validation paths
- data edge cases
- rollback/error paths
- related modules
- shared framework
- EDT/background behavior
- Oracle persistence
- Hibernate/JDBC interaction
- external integrations
- reports/exports
- concurrent processing

## 4. Database/deployment readiness

Check:
- DB scripts
- schema compatibility
- deployment order
- configuration
- shared packaging
- environment differences
- rollback/forward-fix strategy

## 5. Operational readiness

Check:
- Ops workflow impact
- audit/history
- logging/observability
- supportability
- recovery
- user-facing errors
- report/output compatibility

## 6. Release blockers and residual risk

Do not provide an overall subjective rating.

Provide:
- verified areas
- unverified areas
- blockers
- required tests
- deployment safeguards
- human confirmations
- residual risks
- documentation updates required

## Final output

### Requirement coverage
### Regression impact
### Regression matrix
### DB/deployment checks
### Operational checks
### Release blockers
### Residual risks
### Documentation updates required

## JUnit NRT execution and coverage

The application uses module-specific non-regression test modules containing JUnit test cases.

Before finalizing the assessment:
- identify the NRT module(s) corresponding to affected application module(s)
- identify existing JUnit cases that cover the changed behavior
- identify cases that should be extended because expected behavior changed
- identify genuinely new cases required for new behavior
- identify relevant NRT suites in transitively affected/shared modules
- distinguish targeted tests from broader regression suites
- record tests not executed and why
- record environment, DB, data, or external-system limitations

Add:

### JUnit NRT coverage matrix

| Application module | NRT module | JUnit class/case | Scenario | Why affected | Execution status | Gap/action |
|---|---|---|---|---|---|---|

A passing targeted test suite is evidence only for the scenarios actually exercised. Do not treat it as proof that unrelated workflows are unaffected.

## JUnit NRT effectiveness verification

For each important executed test/case, verify whether it actually protects the changed behavior.

Check:
- assertions cover the changed output/state
- the changed execution path is actually exercised
- mocks/stubs do not bypass the behavior under review
- boundary/error/rollback behavior is tested where relevant
- fixtures/test data reproduce the important production condition
- environment-dependent tests are identified
- a passing test is not being used as evidence for scenarios it never exercises

Call out weak test protection as a regression gap even when the test passes.
