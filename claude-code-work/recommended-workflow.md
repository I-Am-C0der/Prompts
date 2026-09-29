# Recommended Workflow — Legacy Investment-Banking Application

This document is the practical execution guide for the 14-prompt Claude Code workflow.

## Phase 0 — Preconditions

Before starting:

1. Start Claude Code at the application repository root.
2. Verify the branch/worktree.
3. Confirm the repository is complete enough for source, build, configuration, and test analysis.
4. Prefer a clean worktree/checkpoint before documentation changes.
5. Never provide secrets or production/customer data to Claude.
6. If DB/test-environment access is unavailable, record the limitation rather than guessing.

## Phase A — Establish durable system knowledge

### Step A1 — 01 Initial Reconnaissance

Purpose:
- understand the whole shared application
- map business modules and runtime architecture
- identify project/runtime/deployment boundaries
- analyze Swing, Oracle, Hibernate/JDBC, wrapper framework, integrations, operations, and risks

Output is analysis only.

### Step A2 — 02 Create Architecture Reference

Create/update the persistent architecture reference, including:

- CODEBASE_OVERVIEW
- ARCHITECTURE
- MODULES
- DATA_FLOW
- DOMAIN_AND_OPERATIONAL_FLOWS
- DATABASE_AND_PERSISTENCE
- UI_AND_FRAMEWORK
- DEPENDENCIES
- MODULE_RISK_MAP
- TESTING_AND_NON_REGRESSION
- KNOWN_ISSUES

### Step A3 — 03 Create/Update CLAUDE.md

Keep CLAUDE.md concise and operational.

It should tell Claude:
- what the application is
- critical Java 8/Swing/Oracle/Hibernate/JDBC constraints
- wrapper-framework constraints
- important project/runtime boundaries
- testing expectations
- where deeper architecture documentation lives

### Step A4 — 04 Independent Architecture Audit

Independently compare source to the documentation.

Correct:
- wrong dependencies
- missing modules
- stale DB information
- incorrect Swing/framework behavior
- wrong operational flows
- missing NRT relationships
- undocumented shared-runtime risks

### Step A5 — 05 Code Review Guidelines

Create project-specific review rules covering:
- architecture
- Java 8
- Swing
- Oracle/Hibernate/JDBC
- wrapper framework
- security
- data correctness
- operational workflows
- NRT testing
- deployment/release risks

### Step A6 — 11 Simulation & Credit Risk Dossier

Because these are the current focus modules, create a dedicated durable dossier covering:
- module architecture
- workflows
- calculations
- data sources
- persistence
- cross-module dependencies
- important JUnit NRT cases
- risk hotspots
- future CR entry points

## Phase B — Before a significant Change Request

### Step B1 — 10 CR Impact Analysis

Determine the real blast radius.

Trace:
- current behavior
- requirement-to-code mapping
- affected files/classes/projects
- upstream/downstream consumers
- hidden dependencies
- Oracle objects
- transactions
- Swing path
- wrapper framework
- reports/jobs/integrations
- Ops workflow
- regression surface

Do not implement.

### Step B2 — 12 Legacy Change Safety Assessment

Assess the proposed implementation against:
- Java 8
- Swing
- Oracle
- Hibernate/JDBC
- wrapper framework
- shared runtime/classpath
- legacy implicit contracts
- operational safety
- rollback

Do not implement.

### Step B3 — 07 Pre-Implementation Architecture Review

Convert the impact analysis into:
- current-state understanding
- candidate designs
- design trade-offs
- affected files/classes
- DB/config changes
- test strategy
- rollout/rollback plan
- stop conditions

Do not implement.

### Step B4 — 14 NRT Test Impact Analysis

Map the CR to:
- affected application modules
- corresponding NRT modules
- relevant JUnit test classes/cases
- direct/partial/indirect/missing coverage
- required test changes
- targeted and broader NRT execution

Do not implement.

## Phase C — Implementation

Implement the approved design using the normal development process.

During implementation, continue to respect:
- Java 8 compatibility
- Swing EDT rules
- Oracle/Hibernate/JDBC transactions
- wrapper-framework contracts
- shared project/classpath implications
- local module conventions
- NRT test architecture

## Phase D — After implementation

### Step D1 — 06 Standard Code Review

Review:
- complete diff
- surrounding code
- callers/consumers
- DB references
- framework behavior
- NRT tests
- architecture docs

Only report actionable evidence-backed findings.

### Step D2 — 13 Regression & Release Readiness

Determine:
- requirement coverage
- true regression surface
- module NRT suites
- relevant JUnit cases
- missing coverage
- DB/deployment readiness
- Ops workflow impact
- reports/audit impact
- release blockers
- residual risks

Do not provide a vague overall rating.

### Step D3 — 08 Update Architecture Documentation

Synchronize only the technical facts changed by the implementation.

Update the NRT architecture reference when:
- new tests were added
- tests moved/renamed
- a module's NRT relationship changed
- regression expectations changed
- test fixtures/setup changed materially

## Phase E — Periodic maintenance

Run 09 Periodic Architecture Audit after:
- several significant CRs
- major releases
- major shared-framework changes
- substantial DB changes
- noticeable documentation drift

Specifically check for NRT architecture drift and whether important production flows have become weakly tested.

## Phase F — Small CR path

For a genuinely isolated change:

1. 10 — CR Impact Analysis
2. 06 — Standard Code Review
3. 13 — Regression & Release Readiness
4. 08 — Documentation update only when required

If impact or test scope is unclear, use the full workflow.

## Decision discipline

Use these distinctions:

**Not ideal**
- old code
- inconsistent style
- duplicated logic
- unusual local pattern

These are not automatically review findings.

**Unsafe**
- data-integrity problem
- broken transaction behavior
- security violation
- incorrect operational result
- shared-runtime regression
- EDT/threading defect
- incompatible DB/framework behavior
- missing protection for a material regression path

These deserve concrete investigation and action.

## Persistent artifacts

For a substantial CR, retain:
- CR impact analysis
- legacy safety assessment
- architecture/design review
- NRT impact analysis
- code review
- regression/release readiness assessment

These provide a durable technical record for maintenance, handover, future CRs, and regression analysis.
