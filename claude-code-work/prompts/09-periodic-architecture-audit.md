# 09 — Periodic Full Architecture Audit

Perform a periodic health audit of the application's architecture and its persistent documentation.

The current source code is authoritative.

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