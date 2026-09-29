# Claude Code — Work Application Workflow

A reusable workflow and prompt set for analyzing, documenting, reviewing, and maintaining a medium-to-complex application with Claude Code CLI.

> **Scope:** Work-related application development only. This repository section is intentionally independent of any personal projects.

## Recommended sequence

1. `01-initial-reconnaissance.md` — understand the application without changing source.
2. `02-create-architecture-reference.md` — create persistent architecture documentation.
3. `03-create-claude-md.md` — create a concise project-level `CLAUDE.md`.
4. `04-independent-architecture-audit.md` — independently verify the documentation against source.
5. `05-code-review-guidelines.md` — establish project-specific review rules.
6. `06-standard-code-review.md` — use for normal change/PR reviews.
7. `07-pre-implementation-architecture-review.md` — use before substantial changes.
8. `08-update-architecture-docs.md` — refresh documentation after architectural changes.
9. `09-periodic-architecture-audit.md` — periodically detect architectural drift.

## Model usage

For a genuinely complex codebase, a deeper-reasoning model can be used for the initial reconnaissance, architecture documentation, independent audit, and critical subsystem analysis. Use a strong general coding model for major implementation/refactoring work and a faster model for routine reviews and smaller changes.

The prompts deliberately require Claude to distinguish:
- confirmed facts from source code
- reasonable inferences
- unresolved/uncertain areas

The source code remains authoritative when documentation and implementation disagree.

## Persistent documentation layout

The architecture workflow creates:

```
docs/
└── architecture/
    ├── CODEBASE_OVERVIEW.md
    ├── ARCHITECTURE.md
    ├── MODULES.md
    ├── DATA_FLOW.md
    ├── DEPENDENCIES.md
    ├── KNOWN_ISSUES.md
    └── CODE_REVIEW_GUIDELINES.md
```

Keep `CLAUDE.md` concise. It should contain project instructions and references to the architecture documents rather than duplicating the entire architecture.


## Legacy application context

This workflow is specifically tuned for a legacy internal investment-banking post-settlement application used by Ops teams.

Known context to verify against the repository:
- Developed over 15+ years.
- Capabilities include post-settlement, settlement, custody movements, simulation, credit risk, reports, and other operational modules.
- Java 8 with Java Swing desktop UI.
- Oracle database using both Hibernate and JDBC.
- Shared wrapper framework providing additional security/features.
- Projects are separated for categorisation, but they are not independently deployed microservices; they form one traditionally built shared application and are ultimately built/deployed together.
- Roughly 75 developers have worked on different areas over time, so module-level code structure, design patterns, naming, exception handling, and abstraction quality can differ substantially.
- Current focus: Simulation and Credit Risk.

### Principles for this legacy system
1. Treat project separation as categorisation unless runtime/deployment isolation is proven.
2. Trace shared classes, utilities, configuration, wrapper-framework hooks, and database objects across projects.
3. Analyze Swing EDT/background processing and UI responsiveness.
4. Analyze Oracle, Hibernate, JDBC, transactions, locking, and session/connection lifecycle together.
5. Preserve safe local legacy patterns rather than forcing stylistic uniformity across modules.
6. Prioritize data integrity, operational correctness, auditability, recoverability, and regression risk.
7. Classify material findings as Confirmed, Inferred, or Uncertain.
8. Avoid speculative microservice/rewrite/modernization recommendations unless the actual CR requires them.

## Prerequisites
- Claude Code CLI installed and authenticated on the work laptop.
- Complete application repository available locally.
- Run Claude Code from the correct repository root.
- Verify the intended branch/worktree before permitting documentation changes.
- Prefer a clean working tree or isolated worktree/checkpoint.
- Relevant build, configuration, and test files available.
- Representative test environment/data when possible.
- Never paste or commit credentials, tokens, certificates, customer information, production payloads, or other secrets.
- Database access is optional; unavailable database behavior must be marked unverified.

## Recommended CR sequence
For a substantial Change Request, use:
10-change-request-impact-analysis.md -> 12-legacy-change-safety-assessment.md -> 07-pre-implementation-architecture-review.md -> implementation -> 06-standard-code-review.md -> 13-post-change-regression-and-release-readiness.md -> 08-update-architecture-docs.md

Use 11-simulation-credit-risk-module-dossier.md to establish durable technical knowledge for the Simulation and Credit Risk modules.