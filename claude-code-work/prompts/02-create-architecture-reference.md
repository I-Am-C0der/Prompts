# 02 — Create Persistent Architecture Reference

Convert the repository reconnaissance into a durable architecture reference for this legacy investment-banking application.

## Rules

- Validate important findings against source before documenting them.
- Modify documentation only under `docs/architecture/`.
- Do NOT modify application source code.
- Source code is authoritative.
- Do not claim behavior without evidence.
- Do not turn project boundaries into fake runtime/service boundaries.
- Preserve high-value legacy details that future CRs need.
- Mark material uncertainty explicitly.
- Do not copy secrets or production/customer data.

## Create/update

### 1. CODEBASE_OVERVIEW.md
Include:
- application purpose and users
- business capabilities
- technology/runtime stack
- build/deployment model
- project/module structure
- entry points
- shared infrastructure
- external systems
- operational context
- major change-risk areas

### 2. ARCHITECTURE.md
Include:
- actual architectural style
- runtime topology
- project/package boundaries
- component responsibilities
- dependency directions
- shared runtime state
- wrapper framework
- Swing/UI layers
- integration boundaries
- persistence boundaries
- transaction model
- cross-cutting concerns
- architectural constraints
- important risks

Explicitly distinguish organisational project separation from runtime/deployment isolation.

### 3. MODULES.md
For each major module/project:
- responsibility
- important packages/classes
- entry points
- dependencies/dependents
- public/internal interfaces
- DB objects used
- external systems used
- important invariants
- operational significance
- change hazards
- test coverage/gaps
- maintenance clues supported by source

### 4. DATA_FLOW.md
Document important end-to-end flows:
UI/event -> validation -> business processing -> persistence/integration -> output/audit -> user-visible result.

Include transaction boundaries, side effects, retries, failures, and recovery.

### 5. DOMAIN_AND_OPERATIONAL_FLOWS.md
Document:
- Ops workflows
- preconditions
- state transitions
- validations
- operational side effects
- audit/history
- reports/exports
- downstream impacts
- recovery paths

Do not invent business rules.

### 6. DATABASE_AND_PERSISTENCE.md
Document:
- Oracle schema areas
- tables/entities
- Hibernate mappings
- JDBC/raw SQL
- HQL/JPQL where used
- procedures/packages/functions
- views/triggers/sequences/synonyms
- transaction boundaries
- session/connection lifecycle
- commit/rollback behavior
- locking/concurrency
- query hotspots
- data ownership
- deployment/schema dependencies
- mixed Hibernate/JDBC risks

### 7. UI_AND_FRAMEWORK.md
Document:
- Swing screens/actions/listeners
- EDT/background processing
- UI-to-business/data boundaries
- UI lifecycle
- wrapper-framework initialization/lifecycle
- security hooks
- configuration
- common established patterns
- risky patterns

### 8. DEPENDENCIES.md
Document:
- project-to-project dependencies
- shared libraries/utilities
- wrapper framework
- third-party libraries
- DB dependencies
- external systems
- configuration dependencies
- compile-time/runtime/deployment relationships
- hidden dependencies discovered through reflection/configuration/framework registration

### 9. MODULE_RISK_MAP.md
For each major module, capture evidence-backed:
- change blast radius
- coupling
- DB sensitivity
- UI sensitivity
- concurrency sensitivity
- integration sensitivity
- operational/financial criticality
- test confidence
- documentation confidence

Prefer Low/Medium/High with justification. Do not invent arbitrary numeric scores.

### 10. KNOWN_ISSUES.md
Document concrete evidence-backed:
- architectural risks
- technical debt
- fragile areas
- reliability/data-integrity concerns
- performance concerns
- security concerns
- testing gaps
- documentation gaps
- unresolved architectural questions

### 11. MODULE_DOSSIER_SIMULATION_CREDIT_RISK.md
Include when the Simulation/Credit Risk deep-dive has been performed.

## Final verification

Before finishing:
1. Cross-check the documents for contradictions.
2. Make sure project/runtime/deployment boundaries are described correctly.
3. Make sure DB, UI/framework, operational, and cross-module dependencies are represented.
4. Remove stale or unsupported claims.
5. Identify important unknowns requiring human validation.

Finish with:
- top facts future CRs must know
- highest-risk areas
- high-value unknowns requiring verification

## JUnit non-regression documentation

Add the NRT test architecture to the persistent reference.

In MODULES.md, document for each relevant application module:
- corresponding non-regression test module/project
- important JUnit test classes
- functional/operational areas covered
- shared test infrastructure
- important DB/integration test dependencies
- notable test gaps

In a suitable architecture document, preserve the relationship:

application module -> production flow -> NRT module -> JUnit test cases -> test data/dependencies

Do not equate test count with coverage quality.

### 12. TESTING_AND_NON_REGRESSION.md
Document the application's JUnit non-regression architecture:
- application module -> NRT module relationship
- major JUnit test classes/cases
- functionality/operations covered
- shared test utilities/base classes
- fixtures/test data
- DB/integration dependencies
- critical regression-sensitive scenarios
- known coverage gaps
- tests that cover shared/common application components

Document what the tests actually exercise. Do not use test count as a proxy for coverage quality.