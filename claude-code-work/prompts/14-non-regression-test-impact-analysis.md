# 14 — Non-Regression Test Impact Analysis

Use this prompt to map a Change Request to the application's module-specific JUnit non-regression testing.

**Do NOT implement application code.**

## Context

Each application module has its own non-regression test module/project containing multiple JUnit test cases covering different functionalities and operational scenarios.

The application is a legacy investment-banking post-settlement system with Java 8, Swing, Oracle, Hibernate, JDBC, a shared wrapper framework, and a shared traditionally built runtime.

## Objective

Determine exactly which NRT tests should protect the CR and where coverage is missing.

## Repository visibility

Read `docs/architecture/REPOSITORY_VISIBILITY.md` when available. The local working tree may be a partial/sparse checkout. When an affected production module's NRT project, JUnit class, shared test utility, fixture, or dependent production module is outside the checkout, inspect the relevant repository tree and source through available read-only Git evidence. Retrieve only the files necessary to establish the test relationship. Do not perform a full checkout merely for test-impact analysis. Distinguish Confirmed — Local, Confirmed — Git, Inferred, and Unverified. Do not conclude that a test or NRT module is absent merely because it is not checked out.

## JAR/binary dependencies

If the changed production or test flow depends on classes supplied by JARs rather than visible source, consult `docs/architecture/JAR_AND_BINARY_DEPENDENCIES.md` and inspect relevant compiled classes/methods selectively when needed to map the real behavior and NRT impact. Do not treat the absence of source as absence of implementation.

## GUI/database lineage

When a CR changes a GUI action, screen, persistence path, or database object, use `docs/architecture/GUI_DATABASE_LINEAGE.md` when present to identify the exact user action and data flow that the NRT cases should protect. If lineage is JAR-backed or conditional, preserve those conditions in the test scope.

## 1. Identify affected production modules

Use the CR impact analysis and source code to identify:
- directly affected modules
- transitively affected/shared modules
- shared/common code consumers
- affected workflows

Do not assume the named module is the complete regression scope.

## 2. Locate corresponding NRT modules

For each affected production module, identify:
- NRT project/module
- package structure
- JUnit test classes
- base test classes
- shared test utilities
- fixtures/test data
- DB/integration setup

## 3. Map the CR to existing tests

Create:

| CR requirement | Production flow | Application module | NRT module | JUnit class/case | Scenario covered | Coverage status |
|---|---|---|---|---|---|---|

Coverage status should distinguish:
- Directly covered
- Partially covered
- Indirectly covered
- Not covered
- Cannot verify

## 4. Analyze test quality for the changed behavior

For relevant tests, inspect:
- assertions
- test inputs
- boundary cases
- negative/error paths
- rollback/recovery
- database state
- setup/teardown
- mocks/stubs
- shared fixtures
- hidden environment assumptions

Do not equate test existence with useful regression protection.

## 5. Identify test changes required

Determine:
- which existing tests should be updated
- which new tests are genuinely necessary
- which additional module NRT suites should run
- whether a test should be unit, DB/integration, or broader regression coverage

Avoid duplicate tests when an existing test can be extended appropriately.

## 6. Regression execution plan

Separate:
- targeted JUnit tests
- affected-module NRT suite
- dependent/shared-module NRT suites
- broader regression tests
- manual Ops/UI scenarios where JUnit cannot reproduce the behavior

Record environment/data/external-system limitations.

## 7. Output

### Affected production modules

### NRT module mapping

### Requirement-to-test mapping

### JUnit coverage matrix

### Coverage gaps

### Required test changes

### Test execution plan

### Unverified areas / environment limitations

### Final CR regression-test scope

The goal is to make the testing plan precise enough that another developer can identify and execute the correct JUnit NRT cases without rediscovering the entire test architecture.


## Test effectiveness

Determine whether relevant tests can actually detect the regression the CR could introduce.

Check:
- assertions verify the changed output/state rather than only incidental non-null/existence conditions
- the changed execution path is actually exercised
- mocks/stubs do not bypass the behavior under review
- boundary and negative/error paths are covered where relevant
- rollback/recovery behavior is tested where relevant
- fixtures/test data reproduce the important production condition
- environment-dependent behavior is identified
- a passing test is not treated as evidence for scenarios it never exercises

When identifying a weakness, state the specific regression that could escape detection and the relevant JUnit/NRT scenario that should protect against it.
