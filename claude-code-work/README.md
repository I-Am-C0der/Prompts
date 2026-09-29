# Claude Code — Legacy Investment-Banking Application Workflow

Reusable Claude Code CLI prompts for analyzing, planning, reviewing, testing, and safely changing a legacy internal investment-banking application.

## 1. Application context

This workflow is specifically designed around the following application context:

- Internal post-settlement application used primarily by the Operations (Ops) team.
- Developed and maintained for more than 15 years.
- Covers settlement, custody movements, simulation, credit risk, reports, and other operational modules.
- Java 8.
- Java Swing desktop GUI.
- Oracle database.
- Hibernate and JDBC are both used.
- A shared wrapper framework provides additional security and application features.
- The application is split into multiple projects/modules for categorisation, but it is **not a microservices architecture**. The projects form a traditionally built shared application and are built/deployed together.
- Approximately 75 developers have worked across the application over time, so different modules can have materially different coding styles, designs, abstractions, error handling, and conventions.
- Current development focus: **Simulation and Credit Risk**.
- Each application module has its own **JUnit non-regression (NRT) module/project**, containing multiple test cases for different functionalities and operational scenarios.

These facts are context for the prompts, not proof. Claude must verify important details against the repository.

## 2. Core principles

1. **Source code is authoritative.** Documentation is a maintained reference, not proof of behavior.
2. **Do not assume project boundaries are runtime boundaries.** A project split may be organisational, build-related, runtime-related, or deployment-related; determine which is actually true.
3. **Trace the whole blast radius.** Shared classes, utilities, configuration, framework services, DB objects, reports, jobs, and NRT suites can create indirect dependencies.
4. **Analyze Oracle + Hibernate + JDBC together.** ORM code alone may not reveal the actual transaction, SQL, locking, or DB-object behavior.
5. **Treat Swing behavior as production behavior.** EDT safety, UI responsiveness, background work, lifecycle, and blocking calls matter.
6. **Treat the wrapper framework as an architectural/security dependency.** Do not bypass or change it without understanding its responsibilities.
7. **Respect safe local legacy patterns.** Do not force one coding style across modules simply because the codebase evolved under many developers.
8. **Prioritize operational and data correctness.** Auditability, recoverability, state transitions, calculations, reports, and Ops workflows matter as much as compile/test success.
9. **Use evidence labels.** Material findings should be classified as Confirmed, Inferred, or Uncertain.
10. **Preserve existing domain invariants.** Where applicable, investigate existing application rules involving dates/calendars/cut-offs, currencies/units, precision/rounding, state transitions, reconciliation/control totals, audit/history, approvals/entitlements, batch dependencies, and duplicate-processing prevention. Derive them from application evidence; do not invent banking rules.
11. **Avoid speculative modernization.** Do not recommend rewrites, microservices, framework migrations, or broad refactors unless the actual change requires them.
11. **Tests are evidence, not proof of everything.** A passing JUnit NRT case proves the scenario it exercises; it does not prove unrelated workflows are unaffected.
12. **Never expose sensitive information.** Do not copy secrets, credentials, customer data, production payloads, or restricted configuration into prompts or generated documentation.

## 3. Prerequisites

Before running the workflow:

- Claude Code CLI is installed and authenticated on the work laptop.
- The complete application repository is available locally.
- Claude Code is started from the correct application repository root.
- The intended branch/worktree is verified.
- For documentation-changing prompts, prefer a clean working tree or isolated worktree/checkpoint.
- Build, configuration, and test files are available.
- Representative test environment/data is available where practical.
- Database access is useful but optional. If DB behavior cannot be verified, record it as Uncertain.
- Do not paste credentials, tokens, certificates, customer information, production data, or other secrets into Claude Code.

## 4. Prompt catalog

### Foundation and architecture

| # | Prompt | Purpose |
|---|---|---|
| 01 | Initial Reconnaissance | Understand the full application, runtime architecture, dependencies, persistence, UI, framework, operations, and risk hotspots. |
| 02 | Create Architecture Reference | Turn the findings into persistent architecture documentation. |
| 03 | Create/Update CLAUDE.md | Create concise, operational Claude Code instructions for the application. |
| 04 | Independent Architecture Audit | Re-verify the architecture documentation against source and detect drift/missing knowledge. |
| 05 | Code Review Guidelines | Create application-specific review rules rather than generic checklist advice. |

### Change Request and implementation

| # | Prompt | Purpose |
|---|---|---|
| 07 | Pre-Implementation Architecture Review | Review design and implementation approach before coding. |
| 10 | Change Request / CR Impact Analysis | Determine the true technical blast radius before coding. |
| 12 | Legacy Change Safety Assessment | Check Java 8, Swing, Oracle, Hibernate/JDBC, wrapper framework, shared-runtime, and legacy implicit-contract risks. |
| 14 | Non-Regression Test Impact Analysis | Map the CR to the correct module NRT project and JUnit cases and identify test gaps. |

### After implementation

| # | Prompt | Purpose |
|---|---|---|
| 06 | Standard Code Review | Review the implementation in full legacy context. |
| 13 | Post-Change Regression & Release Readiness | Determine regression scope, NRT execution, deployment checks, and release blockers. |
| 08 | Update Architecture Documentation | Synchronize the persistent technical reference after architectural/behavioral changes. |

### Domain-focused

| # | Prompt | Purpose |
|---|---|---|
| 11 | Simulation & Credit Risk Module Dossier | Build reusable technical/domain knowledge for the Simulation and Credit Risk modules. |

### Periodic maintenance

| # | Prompt | Purpose |
|---|---|---|
| 09 | Periodic Architecture Audit | Detect architectural drift and stale documentation. |

## 5. One-time baseline setup

Run these once from the application root:

1. `01-initial-reconnaissance.md`
2. `02-create-architecture-reference.md`
3. `03-create-claude-md.md`
4. `04-independent-architecture-audit.md`
5. `05-code-review-guidelines.md`
6. `11-simulation-credit-risk-module-dossier.md` for the current Simulation/Credit Risk development focus.

After this baseline exists, future sessions should read `CLAUDE.md` plus only the architecture documents relevant to the current work.

## 6. Standard significant-CR workflow

For a substantial Change Request:

```
10 — CR Impact Analysis
        ↓
12 — Legacy Change Safety Assessment
        ↓
07 — Pre-Implementation Architecture Review
        ↓
14 — NRT Test Impact Analysis
        ↓
Implementation
        ↓
06 — Standard Code Review
        ↓
13 — Regression & Release Readiness
        ↓
08 — Update Architecture Documentation
```

### Why this order

**10** establishes what the CR really touches.

**12** checks whether the proposed change is safe inside the legacy technology/runtime constraints.

**07** converts the impact map into a concrete design and implementation sequence.

**14** determines which existing JUnit NRT cases protect the change and where coverage is missing.

Then the implementation is performed.

**06** reviews the final implementation.

**13** verifies the broader regression and release surface.

**08** updates the persistent architecture reference.

## 7. Lightweight CR workflow

For a genuinely isolated change:

1. `10-change-request-impact-analysis.md`
2. `06-standard-code-review.md`
3. `13-post-change-regression-and-release-readiness.md`
4. Run `08-update-architecture-docs.md` only if the architecture/behavior reference changed.

Do not label a change "isolated" until callers, consumers, shared code, configuration, DB usage, and relevant NRT coverage have been considered.

## 8. JUnit NRT strategy

Each production module has a corresponding NRT test module/project with JUnit cases for different functionality and operations.

For a CR, Claude should:

1. Identify affected production modules.
2. Identify their corresponding NRT modules.
3. Locate existing JUnit classes/cases covering the changed flow.
4. Trace NRT coverage in shared/dependent modules.
5. Determine whether an existing test should be updated or a new test is required.
6. Identify negative, boundary, error, rollback, and recovery coverage.
7. Inspect fixtures, base test classes, setup/teardown, DB dependencies, mocks/stubs, and test data.
8. Distinguish targeted NRT execution from broader regression testing.
9. Record tests that could not be executed and the reason.

Maintain the durable mapping in:

`docs/architecture/TESTING_AND_NON_REGRESSION.md`

## 9. Persistent architecture documentation

The normal architecture reference is:

```
docs/
└── architecture/
    ├── CODEBASE_OVERVIEW.md
    ├── ARCHITECTURE.md
    ├── MODULES.md
    ├── DATA_FLOW.md
    ├── DOMAIN_AND_OPERATIONAL_FLOWS.md
    ├── DATABASE_AND_PERSISTENCE.md
    ├── UI_AND_FRAMEWORK.md
    ├── DEPENDENCIES.md
    ├── MODULE_RISK_MAP.md
    ├── TESTING_AND_NON_REGRESSION.md
    ├── KNOWN_ISSUES.md
    ├── CODE_REVIEW_GUIDELINES.md
    └── MODULE_DOSSIER_SIMULATION_CREDIT_RISK.md
```

Keep `CLAUDE.md` concise. Store deep technical knowledge in the architecture documents.

## 10. Evidence convention

Use:

- **Confirmed** — directly supported by source/configuration/tests or verified runtime evidence.
- **Inferred** — a reasonable conclusion derived from available evidence.
- **Uncertain** — insufficient evidence; state exactly what must be verified.

Do not turn an inference into a fact merely because the same assumption appears in documentation or naming.

## 11. Legacy investigation priorities

For this application, repeatedly check:

- project vs package vs compile-time vs runtime vs deployment boundaries
- shared classpath and common projects
- shared utilities, static state, singletons, and caches
- Swing EDT/background-worker behavior
- blocking DB/API work from the UI
- Oracle transactions, locking, and connection lifecycle
- Hibernate session/flush/lazy-loading behavior
- JDBC connection/transaction handling
- mixed Hibernate/JDBC effects
- tables, views, triggers, sequences, synonyms, procedures/packages/functions
- reflection and string/configuration dependencies
- wrapper-framework lifecycle/security hooks
- scheduled/batch processing
- reports/exports
- audit/history
- retries/idempotency
- exception swallowing
- deployment/packaging effects
- data/financial/risk calculation correctness
- module-level JUnit NRT coverage and gaps

## 12. Model allocation

Use deeper reasoning for repository reconnaissance, architecture extraction, independent audits, CR impact analysis, Simulation/Credit Risk deep-dives, NRT impact analysis, and difficult legacy-safety assessments.

Use a strong coding/reasoning model for substantial implementation, debugging, and detailed code review.

Use faster models for routine reviews and small documentation maintenance.

Use the more expensive model when deeper repository reasoning materially reduces implementation or regression risk, not merely because budget is available.


## 13. Banking/domain-invariant checks

Where applicable, future CR analysis should explicitly look for existing application invariants involving:
- business/trade/settlement/value dates
- calendars, holidays, cut-offs, and time zones
- currencies and units
- decimal precision and rounding
- lifecycle/state transitions
- reconciliation/control totals
- audit/history
- approvals/entitlements
- end-of-day/batch dependencies
- duplicate-processing prevention

These are discovery targets only. Claude must derive the actual rules from repository evidence and must not invent banking semantics.
