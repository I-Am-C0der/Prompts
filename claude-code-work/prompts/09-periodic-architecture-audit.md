# 09 — Periodic Full Architecture Audit

Perform a periodic health audit of the application's architecture and its persistent documentation.

The current source code is authoritative.

## Repository visibility

Also compare the current local working-tree scope with `docs/architecture/REPOSITORY_VISIBILITY.md` and the repository structure available through Git. Check whether new modules/projects, shared dependencies, NRT projects, or build/deployment components exist outside the local checkout and could affect the documented architecture. Use selective read-only Git inspection where needed; do not perform a full checkout merely for the audit.

## Compare

- current source tree
- `CLAUDE.md`
- all files under `docs/architecture/`
- recent significant changes where useful

## Look for

- architectural drift
- stale documentation
- undocumented modules/components
- dependency-boundary violations
- growing coupling
- duplicated responsibilities
- new circular dependencies
- changes to data ownership
- changed transaction boundaries
- changed asynchronous flows
- new reliability risks
- new security risks
- performance-sensitive changes
- operational/observability gaps
- test coverage gaps
- resolved issues still documented as active
- new technical debt worth recording

## Output

Provide:

1. Current architecture summary.
2. Documentation discrepancies.
3. Architectural drift since the previous reference.
4. New risks.
5. Resolved risks/issues.
6. Important unknowns.
7. Documentation changes required.

Update the relevant architecture documents after the audit.

Do NOT modify application source code as part of this task.

Avoid speculative redesign. The goal is architectural accuracy, maintainability, and early identification of meaningful risks.

## JAR/binary dependency drift

Audit `docs/architecture/JAR_AND_BINARY_DEPENDENCIES.md` and current classpath artifacts for relevant version drift, duplicate classes, changed binary dependencies, missing source coverage, and stale assumptions about compiled modules. Use selective read-only inspection.

## GUI/database lineage drift

Audit `docs/architecture/GUI_DATABASE_LINEAGE.md` for stale screen names, menu paths, action mappings, DB write paths, conditional navigation, and JAR-backed GUI relationships. Cross-check representative lineage paths against current source/JAR/configuration/database evidence. Record broken or unverified links instead of inferring replacements.

## Legacy-specific periodic checks

Look for accumulating:
- duplicated logic across projects
- growing dependency on shared utilities
- hidden database coupling
- static/global state
- exception swallowing
- recurring transaction/session problems
- recurring EDT blocking
- wrapper-framework bypasses
- stale report/audit/Ops assumptions
- architecture documentation that is no longer useful for future CR impact analysis
## JUnit NRT architecture drift

Also audit:
- application-module to NRT-module mappings
- stale or renamed JUnit classes/cases in documentation
- critical workflows with weak NRT coverage
- test fixtures/data that no longer represent the production flow
- shared-code changes whose NRT coverage is concentrated in only one module
- regression suites that no longer exercise important paths
