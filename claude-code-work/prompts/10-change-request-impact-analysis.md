# 10 — Change Request / CR Impact Analysis

Use this prompt whenever a new Change Request arrives.

**Do NOT implement the CR.**

## Objective

Determine the true technical blast radius before coding in a legacy investment-banking application.

## Context

Known characteristics:
- Internal Ops-facing post-settlement application developed over 15+ years.
- Capabilities include settlement, custody movements, simulation, credit risk, reporting, and other operational modules.
- Java 8, Swing, Oracle, Hibernate, JDBC, and a shared wrapper framework.
- Multiple projects/modules exist for categorisation, but they are not independently deployed microservices; they form one traditionally built shared application.
- Roughly 75 developers have worked across the application over time, so local patterns can differ significantly between modules.
- Current focus: Simulation and Credit Risk.

Verify context against the repository where possible. Do not assume project boundaries are runtime boundaries.

The local working tree may be a partial/sparse checkout. Read `docs/architecture/REPOSITORY_VISIBILITY.md` when available. When CR impact could depend on code outside the working tree, inspect relevant repository tree/files through available read-only Git evidence before concluding a dependency is unavailable. Do not perform a full checkout merely for impact analysis.

## Inputs

Use:
- CR/business requirement
- acceptance criteria
- screenshots/examples
- named module/project
- architecture documents
- relevant source

Record ambiguity instead of guessing.

## 1. Establish current behavior

Trace the closest existing flow:

UI/event
-> validation
-> business/service
-> persistence/integration
-> output/report/audit
-> user-visible result

State what is actually implemented today.

## 2. Convert the CR into technical requirements

Create:

| CR requirement | Current behavior | Required behavior | Likely implementation area | Evidence | Confidence |
|---|---|---|---|---|---|

Separate:
- explicit requirements
- strongly supported implications
- assumptions requiring confirmation

## 3. Find the real impact surface

Identify:
- files/classes/methods
- interfaces and implementations
- inheritance/subclasses
- listeners/callbacks
- callers and consumers
- shared utilities/framework classes
- directly affected projects
- transitively affected projects
- projects requiring regression only

## 4. Search for hidden dependencies

Search beyond ordinary Java references for:
- reflection
- class names in configuration/resources
- string-based lookups
- framework registration
- event/listener registration
- schedulers/jobs
- SQL/table/column references
- stored procedures/packages/functions
- views/triggers/sequences/synonyms
- reports/exports
- shared configuration

## 5. Analyze database impact

Map:
- Oracle tables/columns
- entities/mappings
- HQL/JPQL/native SQL
- JDBC SQL
- procedures/packages/functions
- views/triggers/sequences/synonyms
- indexes where relevant
- transaction boundaries
- session/connection lifecycle
- commit/rollback
- locking/concurrency
- schema/deployment changes

Explicitly assess whether Hibernate and JDBC consumers see different behavior.

## 6. Analyze UI/framework impact

Map:
- Swing screens/actions/listeners
- EDT/background-worker paths
- long-running operations
- UI state/lifecycle
- wrapper-framework hooks
- authentication/authorization
- configuration

## 7. Analyze operational impact

Identify:
- Ops workflow changes
- audit/history
- reports/exports
- batch/scheduled processing
- external integrations
- recovery behavior
- backward compatibility

## 8. Risk and regression analysis

Assess evidence-backed:
- functional risk
- data-integrity risk
- transaction risk
- concurrency risk
- Swing/EDT risk
- security risk
- integration risk
- performance risk
- compatibility risk
- deployment risk
- regression risk
- rollback risk


## 9. NRT impact signal

Determine:
- which affected production modules have corresponding NRT modules
- which shared/dependent modules may require additional NRT regression
- whether the changed behavior appears to have existing NRT coverage
- whether detailed test-impact analysis is required before design/implementation

Do not perform the detailed test-case mapping here. Use **14 — NRT Test Impact Analysis** for exact JUnit case mapping, coverage-gap analysis, and test execution planning.

## 10. Banking/domain-invariant impact

Where applicable, identify existing application rules involving:
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

Only record rules supported by repository evidence. Do not infer banking rules from domain intuition.

## 11. Questions before coding

List business, DB/schema, framework, environment, and test questions that materially affect implementation.

## Output

### Executive impact summary
### Current behavior
### Required behavior
### Requirement-to-code map
### Technical impact map
### Affected files/classes/projects
### Database impact
### UI/framework impact
### Integration/operational impact
### Hidden dependencies
### Risk assessment
### Regression scope
### Open questions/assumptions
### Suggested implementation boundaries

For material conclusions, state **Confirmed**, **Inferred**, or **Uncertain**.