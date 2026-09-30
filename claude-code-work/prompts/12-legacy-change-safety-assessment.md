# 12 — Legacy Change Safety Assessment

Assess whether a proposed implementation is safe within the existing legacy architecture.

**Do NOT implement the change.**

## Context

The application is:
- Java 8
- Swing desktop
- Oracle
- Hibernate + JDBC
- wrapper-framework based
- traditionally built as a shared application
- split into projects/modules without independent microservice runtime isolation
- maintained by a large heterogeneous developer team with materially different module-level patterns

## Repository visibility

Read `docs/architecture/REPOSITORY_VISIBILITY.md` when available. If a safety-relevant shared class, framework component, configuration, build/deployment artifact, caller/consumer, or DB-related source is outside the local working tree, inspect it selectively through available Git evidence before assessing the change. Do not perform a full checkout merely for the safety assessment. Distinguish Confirmed — Local, Confirmed — Git, Inferred, and Unverified evidence.

## JAR/binary dependencies

Read `docs/architecture/JAR_AND_BINARY_DEPENDENCIES.md` when present. If a safety-relevant dependency is supplied by a JAR, inspect the exact artifact and relevant classes/methods through bytecode/decompilation where necessary. Check binary compatibility, classpath/version conflicts, static state, framework hooks, DB access, and threading behavior that can be established. Distinguish JAR/bytecode evidence from source evidence.

## GUI/database lineage

If the change affects a Swing screen or DB write path, consult `docs/architecture/GUI_DATABASE_LINEAGE.md` when present. Verify menu/action routing, screen lifecycle, persistence path, transaction boundary, trigger/procedure side effects, permission conditions, and any JAR-backed implementation involved.

## Assess

### 1. Shared runtime/classpath
Check:
- shared classes
- binary compatibility
- initialization order
- static state
- singleton behavior
- library/classpath conflicts
- packaging/deployment effects

### 2. Swing
Check:
- EDT access
- blocking calls
- long-running DB/API calls
- background threads
- thread handoff
- lifecycle
- event ordering
- re-entrancy

### 3. Oracle
Check:
- transaction boundaries
- connection handling
- locking
- commit/rollback
- query load
- index assumptions where evidence exists
- schema compatibility
- procedures/packages/functions
- triggers
- sequences
- concurrent processing
- partial updates

### 4. Hibernate + JDBC
Check:
- transaction/session consistency
- flush timing
- stale state
- native SQL side effects
- cache consistency
- connection ownership
- exception propagation

### 5. Wrapper framework
Check:
- required hooks
- security context
- configuration
- lifecycle/interception
- framework-managed services
- unsafe bypasses

### 6. Legacy implicit contracts
Determine whether the change alters:
- initialization/order assumptions
- exception behavior relied upon elsewhere
- object lifecycle
- shared mutable state
- local module conventions
- backward compatibility
- hidden integration behavior

Do not reject a change merely because it is not modern.

### 7. Business/operational safety
Check:
- data integrity
- duplicate processing
- auditability
- recovery
- Ops workflow compatibility
- reports
- downstream effects
- rollback practicality

## Output

### Safety summary
### Legacy constraints
### Specific hazards introduced
### Existing implicit contracts at risk
### Database/transaction hazards
### Swing/threading hazards
### Framework/security hazards
### Shared-runtime hazards
### Operational/regression hazards
### Required safeguards
### Pre-implementation verification checklist

Classify material risks as **Critical, High, Medium, or Low** and cite concrete evidence.
