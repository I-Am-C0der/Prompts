# 01 — Initial Codebase Reconnaissance

You are performing a deep architectural reconnaissance of this application.

This is an analysis-only task.

## Rules

- Do NOT modify source code.
- Do NOT refactor anything.
- Do NOT create or modify project documentation yet.
- Analyze the repository as a whole before forming conclusions.
- Prefer evidence from the actual source over assumptions.
- Clearly distinguish:
  - Confirmed: directly supported by source/config/tests.
  - Inferred: a reasonable conclusion from available evidence.
  - Uncertain: insufficient evidence; state what would need to be checked.
- Do not stop after inspecting only the obvious entry points or a few representative files.

## Analyze

1. Project purpose and major business capabilities.
2. Technology stack, frameworks, build system, runtime, and deployment model.
3. Application entry points and startup lifecycle.
4. Repository/module/package structure.
5. Major components and their responsibilities.
6. Dependencies and important third-party integrations.
7. Request/event/data execution flows.
8. Database access, persistence, transactions, and data ownership.
9. External APIs, messaging, queues, scheduled jobs, and asynchronous processing.
10. Authentication, authorization, configuration, secrets, and security boundaries.
11. Error handling, exception propagation, retries, fallbacks, and failure behavior.
12. Logging, metrics, tracing, and observability.
13. Concurrency, threading, synchronization, caching, and resource management.
14. API contracts and important integration boundaries.
15. Test architecture, test coverage patterns, fixtures, and build/test commands.
16. CI/CD and deployment configuration where present.
17. Architectural patterns and conventions actually used.
18. Coupling, cohesion, circular dependencies, duplicated responsibilities, and suspicious boundaries.
19. Performance-sensitive areas and likely bottlenecks.
20. Technical debt and areas with elevated change risk.

## Output

Produce a structured report with:

- Executive summary
- Technology/runtime overview
- Repository/module map
- Application entry points
- Major components and responsibilities
- Important execution/data flows
- Persistence and transaction model
- External integrations
- Security/configuration model
- Error/reliability model
- Concurrency/resource model
- Testing/build/deployment model
- Architectural patterns
- Coupling and boundary analysis
- Performance considerations
- Technical debt / risk areas
- Important unknowns
- Recommended next analysis steps

Do not recommend broad refactoring merely because a different architecture might be cleaner. Focus on accurately understanding the existing system.
