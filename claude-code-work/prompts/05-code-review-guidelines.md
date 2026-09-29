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
