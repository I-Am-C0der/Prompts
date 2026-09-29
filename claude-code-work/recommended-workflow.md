# Recommended Workflow

## Phase A — Establish the architecture baseline

Run once, from the application root:

1. **01 — Initial Reconnaissance**
2. **02 — Create Architecture Reference**
3. **03 — Create/Update CLAUDE.md**
4. **04 — Independent Architecture Audit**
5. **05 — Create Code Review Guidelines**
6. **11 — Simulation & Credit Risk Module Dossier** when relevant

The objective is to build persistent context so later CRs do not require the same repository-wide discovery.

## Phase B — Before a significant Change Request

### 1. Impact analysis
Run **10 — Change Request / CR Impact Analysis**.

Determine the real blast radius:
- UI entry point
- business/service path
- affected files/classes/projects
- upstream/downstream consumers
- shared utilities
- Oracle objects
- Hibernate/JDBC transaction behavior
- wrapper-framework involvement
- configuration
- reports/jobs/integrations
- Ops workflow impact
- regression scope

### 2. Legacy safety assessment
Run **12 — Legacy Change Safety Assessment**.

Check compatibility and hidden hazards across Java 8, Swing, Oracle, Hibernate/JDBC, the wrapper framework, shared runtime behavior, and legacy implicit contracts.

### 3. Architecture/design review
Run **07 — Pre-Implementation Architecture Review**.

Turn impact analysis into a concrete implementation plan and identify stop conditions before coding.

## Phase C — After implementation

### 4. Code review
Run **06 — Standard Code Review**.

Review the complete diff plus surrounding code, callers, consumers, DB references, and relevant architecture documentation.

### 5. Regression/release readiness
Run **13 — Post-Change Regression & Release Readiness**.

Build the regression matrix and assess:
- direct and indirect regression
- DB/schema changes
- deployment order
- configuration
- shared packaging
- Ops workflow behavior
- auditability
- reports
- rollback/recovery

### 6. Architecture documentation
Run **08 — Update Architecture Documentation**.

Synchronize only the facts that changed.

## Phase D — Periodic audit

Run **09 — Periodic Architecture Audit** after several significant changes, a major release, or when the documentation begins to drift.

## Small-change path

For a genuinely isolated change:
1. 10 — Impact Analysis
2. 06 — Code Review
3. 08 — Documentation update only if required

"Small" does not mean "isolated." Confirm the dependency surface first.

## Working discipline

- Never assume a named project is the only affected project.
- Distinguish project, package, compile-time, runtime, deployment, DB/data, and operational boundaries.
- Trace upstream callers and downstream consumers.
- Search inheritance, interfaces, reflection, configuration strings, framework registration, listeners/events, scheduled jobs, SQL/table references, reports, and shared utilities.
- Treat Oracle and wrapper-framework behavior as part of the dependency graph.
- Preserve safe local legacy patterns rather than forcing global stylistic uniformity.
- Distinguish "not ideal" from "unsafe".
- Record unknowns instead of guessing.
- Avoid broad redesign unless the CR actually requires it.

## What to retain for substantial CRs

Keep the:
- CR impact analysis
- architecture/design review
- code review
- regression/release readiness assessment

These become reusable technical records for maintenance, handover, and future CRs.

## JUnit non-regression testing

Each application module has a corresponding non-regression test module containing multiple JUnit test cases for different functionality and operational scenarios.

For a CR, the test workflow should be:

1. Identify the affected application module(s).
2. Identify each corresponding NRT module.
3. Find existing JUnit coverage for the changed flow.
4. Map requirements to relevant existing test cases.
5. Identify missing coverage and whether an existing test should be extended or a new test added.
6. Expand regression scope to NRT modules of transitively affected/shared modules.
7. After implementation, run targeted NRT tests first, then broader relevant NRT suites as justified by the blast radius.
8. Record unexecuted tests and environment/data limitations.

Use **14 — Non-Regression Test Impact Analysis** before substantial implementation or when the regression surface is unclear.

## Persistent JUnit NRT architecture reference

Maintain `docs/architecture/TESTING_AND_NON_REGRESSION.md` as the durable map of application modules to their JUnit non-regression modules, important test cases, test fixtures/data, integration dependencies, and coverage gaps.

When the test architecture changes, update this document using Prompt 08. Use Prompt 14 to perform detailed CR-to-test mapping before implementation.