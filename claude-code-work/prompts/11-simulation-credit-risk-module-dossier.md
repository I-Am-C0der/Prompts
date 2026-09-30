# 11 — Simulation & Credit Risk Module Deep-Dive

Create a durable technical/domain dossier for the Simulation and Credit Risk modules.

**Do NOT modify application source code.**

## Objective

Capture reusable knowledge so future CR analysis can begin from known module behavior instead of repeatedly rediscovering the repository.

## Rules

- Do not infer business rules solely from class/method names.
- Trace real execution paths.
- Verify calculations, persistence, inputs, and outputs from code.
- Classify material findings as Confirmed, Inferred, or Uncertain.
- Do not expose secrets or sensitive production data.
- Do not assume financial/risk semantics without repository or trusted project evidence.

## Repository visibility

The local working tree may not contain every application project. Read `docs/architecture/REPOSITORY_VISIBILITY.md` when present. For Simulation/Credit Risk dependencies outside the checkout, use selective read-only Git inspection where available to establish shared framework/common dependencies, cross-module callers/consumers, relevant Oracle/DB-related source, corresponding NRT projects, and build/deployment dependencies. Do not perform a full checkout merely for the dossier. Mark inaccessible areas Unverified.

## Simulation

Document:
- project/module structure
- screens and user actions
- entry points and workflows
- validations
- calculation/process flow
- orchestration
- inputs/data sources
- persistence
- outputs/reports
- audit/history
- state/lifecycle
- errors/retry/recovery
- concurrency/background work
- shared utilities
- wrapper-framework dependencies
- callers/consumers
- tests and gaps

For every material calculation identify:
- input data
- transformations
- units
- precision/rounding
- intermediate state
- output consumers
- persistence/audit
- evidence supporting the rule

Do not validate financial correctness from intuition alone.

## Credit Risk

Document:
- project/module structure
- screens/workflows
- inputs/data sources
- validations
- risk-processing/calculation flow
- persistence
- dependencies on other modules
- external/reference data
- outputs/reports
- audit/history
- security/permissions
- errors/recovery
- performance/concurrency
- tests/gaps

For material calculations identify:
- inputs
- transformations
- precision/rounding
- thresholds/limits where present
- aggregation/grouping
- output consumers
- persistence
- evidence supporting each rule

## Cross-module relationships

Trace relationships to:
- Settlement
- Custody
- reporting
- common/shared projects
- Oracle data
- wrapper framework
- external systems

Classify each dependency as:
- compile-time
- runtime
- database/data
- operational

## Future-CR readiness

Identify:
- likely change points
- shared classes with broad blast radius
- critical DB objects
- calculation-sensitive methods
- fragile workflows
- missing regression tests
- unknowns likely to block future CRs

## Output

Create/update:

docs/architecture/MODULE_DOSSIER_SIMULATION_CREDIT_RISK.md

Include:
1. Scope and confidence
2. Simulation architecture
3. Simulation workflows
4. Simulation calculation/data flow
5. Credit Risk architecture
6. Credit Risk workflows
7. Credit Risk calculation/data flow
8. Cross-module dependencies
9. Oracle/persistence dependencies
10. UI/framework dependencies
11. Risk hotspots
12. Test/verification map
13. Known unknowns
14. Future CR Quick Start

## JUnit NRT map

For Simulation and Credit Risk, also document:
- the corresponding NRT module for each production module
- important JUnit test classes/cases by functionality
- test fixtures and shared test utilities
- DB/integration dependencies
- calculation/regression-sensitive test cases
- missing coverage for critical workflows

For material calculations, identify which NRT cases provide protection against regressions in precision, rounding, boundary conditions, aggregation, and expected outputs where such tests exist.

## Domain invariants for Simulation and Credit Risk

Where applicable, identify existing invariants involving:
- valuation/business/scenario dates
- calendars/cut-offs/time zones
- currency/unit conventions
- precision and rounding
- thresholds/limits
- state transitions
- aggregation/reconciliation/control totals
- audit/history
- duplicate processing
- batch/end-of-day dependencies

For each material rule, identify repository evidence. Do not infer financial meaning from intuition alone.

## NRT test effectiveness

For calculation-sensitive tests, determine whether the JUnit NRT cases actually detect regressions in:
- precision/rounding
- boundary conditions
- aggregation
- expected outputs
- state transitions
- negative/error paths

Note weak or missing assertions and identify the specific scenario that could escape detection.
