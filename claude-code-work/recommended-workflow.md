# Recommended Workflow

A simple execution guide for the 14 Claude Code prompts.

## Phase 1 — One-Time Application Setup

Run these once when first analyzing the application.

| Prompt | Run when | Purpose |
|---|---|---|
| **01 — Initial Reconnaissance** | First setup | Understand the full application, modules, architecture, DB, Swing, framework, integrations, and risks. |
| **02 — Create Architecture Reference** | After 01 | Store the findings in persistent architecture documents. |
| **03 — Create/Update CLAUDE.md** | After 02 | Create concise project instructions for Claude Code. |
| **04 — Independent Architecture Audit** | After 03 | Re-check the architecture documentation against the source. |
| **05 — Code Review Guidelines** | After 04 | Create project-specific code-review rules. |
| **11 — Simulation & Credit Risk Dossier** | For your focus modules | Build reusable knowledge for Simulation and Credit Risk. |

## Phase 2 — Before a Change Request

Run these before implementing a significant CR.

| Prompt | Run when | Purpose |
|---|---|---|
| **10 — CR Impact Analysis** | First | Find the real blast radius: code, projects, DB, framework, integrations, Ops flows, and regressions. |
| **12 — Legacy Change Safety Assessment** | After 10 | Check legacy-specific risks: Java 8, Swing, Oracle, Hibernate/JDBC, wrapper framework, shared runtime, etc. |
| **14 — NRT Test Impact Analysis** | After 12 | Map the CR to affected NRT modules/JUnit cases and identify coverage gaps. |
| **07 — Pre-Implementation Architecture Review** | After 14 | Review the proposed design using the code, legacy, dependency, and testing constraints discovered so far. |


### Flow

```
10 → 12 → 14 → 07 → IMPLEMENT
```

## Phase 3 — After Implementation

| Prompt | Run when | Purpose |
|---|---|---|
| **06 — Standard Code Review** | After implementation | Review the change and surrounding code for defects and regressions. |
| **13 — Regression & Release Readiness** | After code review | Determine required JUnit NRT/regression testing, deployment checks, and release blockers. |
| **08 — Update Architecture Docs** | Last | Update persistent architecture knowledge after the change. |

### Flow

```
IMPLEMENT → 06 → 13 → 08
```

## Phase 4 — Periodic Maintenance

| Prompt | Run when | Purpose |
|---|---|---|
| **09 — Periodic Architecture Audit** | After major changes/releases | Detect architecture drift, stale documentation, and new risks. |

## Quick Reference

### First-time setup
```
01 → 02 → 03 → 04 → 05
              ↓
              11 (Simulation/Credit Risk)
```

### Significant CR
```
10 → 12 → 14 → 07 → IMPLEMENT → 06 → 13 → 08
```

### Small / clearly isolated CR
```
10 → 06 → 13
```

Use the full workflow whenever the change has unclear cross-module, DB, framework, UI, or NRT impact.
