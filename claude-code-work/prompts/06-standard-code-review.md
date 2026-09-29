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
