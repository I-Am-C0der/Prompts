# Claude Code — Legacy Investment-Banking Application Workflow

Reusable Claude Code CLI prompts for analyzing, planning, reviewing, and safely changing a legacy internal investment-banking post-settlement application.

## Application context

- Internal Ops-facing application developed over 15+ years.
- Capabilities include post-settlement, settlement, custody movements, simulation, credit risk, reporting, and other operational modules.
- Java 8 with Java Swing desktop GUI.
- Oracle database using Hibernate and JDBC.
- Shared wrapper framework providing additional security/features.
- Multiple projects/modules exist for categorisation, but the application is not independently deployed as microservices; it is a traditionally built shared application.
- Roughly 75 developers have worked across the system, so module-level architecture, coding style, abstractions, exception handling, and conventions can vary significantly.
- Current development focus: Simulation and Credit Risk.

These are starting assumptions to verify against the repository. Do not treat them as proof of runtime behavior.

## Core principles

1. Source code is authoritative.
2. Project/module boundaries are not automatically runtime or deployment boundaries.
3. Shared classes, libraries, configuration, framework services, and DB objects are part of the blast radius.
4. Analyze Oracle + Hibernate + JDBC together.
5. Treat Swing EDT/threading and UI responsiveness as production behavior.
6. Treat the wrapper framework as a security/runtime dependency.
7. Understand safe local legacy patterns before introducing new abstractions.
8. Prioritize data integrity, operational correctness, auditability, recoverability, and regression safety.
9. Label material findings Confirmed, Inferred, or Uncertain.
10. Avoid speculative modernization unless the actual CR requires it.

## Prerequisites

- Claude Code CLI installed and authenticated on the work laptop.
- Complete application repository available locally.
- Claude Code started at the correct repository root.
- Correct branch/worktree verified before documentation changes.
- Prefer a clean working tree or isolated worktree/checkpoint.
- Build, configuration, and test files available.
- Representative test environment/data where practical.
- Never paste or commit credentials, tokens, certificates, customer information, production payloads, or other secrets.
- Database access is optional; unavailable behavior must be recorded as unverified.

## One-time baseline

Run:

1. `prompts/01-initial-reconnaissance.md`
2. `prompts/02-create-architecture-reference.md`
3. `prompts/03-create-claude-md.md`
4. `prompts/04-independent-architecture-audit.md`
5. `prompts/05-code-review-guidelines.md`
6. `prompts/11-simulation-credit-risk-module-dossier.md` when those modules are an active development area.

This creates the durable technical context needed by future CRs.

## Significant CR workflow

For a substantial Change Request:

1. `prompts/10-change-request-impact-analysis.md`
2. `prompts/12-legacy-change-safety-assessment.md`
3. `prompts/07-pre-implementation-architecture-review.md`
4. Before implementation, run `prompts/14-non-regression-test-impact-analysis.md` when the test impact is non-trivial or unclear.
5. Implement the approved change.
6. `prompts/06-standard-code-review.md`
6. `prompts/13-post-change-regression-and-release-readiness.md`
7. `prompts/08-update-architecture-docs.md`

## Lightweight workflow

For a genuinely isolated change:

1. 10 — Change Request Impact Analysis
2. 06 — Standard Code Review
3. 08 — Architecture documentation update only if behavior/architecture changed

Do not call a change isolated until callers, consumers, shared code, configuration, and DB usage have been considered.

## Evidence convention

- **Confirmed** — directly supported by source/configuration/tests or verified runtime evidence.
- **Inferred** — reasonable conclusion derived from available evidence.
- **Uncertain** — insufficient evidence; state what must be checked.

## Legacy investigation priorities

Claude should actively search for:
- cross-project/shared-class dependencies
- reflection and string/configuration references
- shared classpath and packaging assumptions
- Swing EDT violations and blocking operations
- static mutable state, singletons, and caches
- Oracle tables/columns/views/triggers/sequences/synonyms/procedures/packages/functions
- Hibernate session/flush/lazy-loading behavior
- JDBC connection/transaction handling
- mixed Hibernate/JDBC transaction effects
- locking and concurrent processing
- wrapper-framework lifecycle/security hooks
- scheduled/batch processing
- report/export dependencies
- audit/history behavior
- exception swallowing
- retries/idempotency
- deployment/configuration effects
- financial/data correctness
- missing regression tests

## Model usage

Use deeper reasoning for:
- initial reconnaissance
- architecture extraction
- independent architecture audits
- CR impact analysis
- Simulation/Credit Risk deep-dives
- difficult legacy-safety assessments

Use strong coding/reasoning for:
- substantial implementation
- difficult debugging
- detailed code reviews

Use faster models for:
- routine reviews
- straightforward maintenance
- documentation-only tasks

## Persistent architecture reference

Normally maintain:

- `docs/architecture/CODEBASE_OVERVIEW.md`
- `docs/architecture/ARCHITECTURE.md`
- `docs/architecture/MODULES.md`
- `docs/architecture/DATA_FLOW.md`
- `docs/architecture/DOMAIN_AND_OPERATIONAL_FLOWS.md`
- `docs/architecture/DATABASE_AND_PERSISTENCE.md`
- `docs/architecture/UI_AND_FRAMEWORK.md`
- `docs/architecture/DEPENDENCIES.md`
- `docs/architecture/MODULE_RISK_MAP.md`
- `docs/architecture/KNOWN_ISSUES.md`
- `docs/architecture/CODE_REVIEW_GUIDELINES.md`
- `docs/architecture/MODULE_DOSSIER_SIMULATION_CREDIT_RISK.md` when applicable

Keep `CLAUDE.md` concise; store deep architecture knowledge in these persistent documents.

## Sensitive-data rule

Architecture analysis must not copy secrets, credentials, customer information, production payloads, or other restricted data into prompts or documentation. Use sanitized examples and descriptions where needed.

## JUnit module-level non-regression testing

Each application module has its own **non-regression test module/project** containing multiple JUnit test cases covering different functionalities and operational scenarios.

Treat these NRT modules as part of the application's maintainability and change-impact model.

For future CR analysis, Claude should:
- identify the NRT module associated with the affected application module
- locate existing JUnit test classes/cases covering the affected functionality
- map CR requirements to existing NRT coverage
- identify related NRT cases in dependent/shared modules
- distinguish direct NRT coverage from broader regression scenarios
- identify missing tests when the CR changes behavior not covered by existing cases
- avoid creating duplicate tests when an existing test can be updated appropriately
- inspect test fixtures/data/setup/teardown and shared test utilities before proposing changes
- verify whether tests are unit-level, DB/integration-level, or broader operational/regression tests
- treat a passing JUnit test as evidence for the tested scenario, not proof that the entire regression surface is safe

The architecture reference should maintain a durable map between modules, NRT modules, major functional areas, and important JUnit test cases where that information can be established safely.


- `docs/architecture/TESTING_AND_NON_REGRESSION.md`
- `docs/architecture/MODULE_DOSSIER_SIMULATION_CREDIT_RISK.md` when applicable