# 08 — Update Architecture Documentation After a Change

A substantial implementation change has been completed. Update the persistent architecture documentation so it accurately reflects the current application.

## Rules

- Current source code is authoritative.
- Inspect the actual changes and surrounding implementation.
- Compare source against the existing architecture documents.
- Make the minimum documentation changes necessary to keep the reference accurate.
- Do NOT modify application source code.
- Do not rewrite documents unnecessarily.
- Remove statements that are now demonstrably stale.
- Add new architectural facts, flows, dependencies, risks, or constraints introduced by the change.

Review and update as applicable:

- `CLAUDE.md`
- `docs/architecture/CODEBASE_OVERVIEW.md`
- `docs/architecture/ARCHITECTURE.md`
- `docs/architecture/MODULES.md`
- `docs/architecture/DATA_FLOW.md`
- `docs/architecture/DEPENDENCIES.md`
- `docs/architecture/KNOWN_ISSUES.md`
- `docs/architecture/CODE_REVIEW_GUIDELINES.md`

After updating, summarize:
- what changed architecturally
- which documents changed
- newly introduced risks/constraints
- any documentation questions that remain unresolved

## Additional documents to keep synchronized

Also update, when affected:
- docs/architecture/DOMAIN_AND_OPERATIONAL_FLOWS.md
- docs/architecture/DATABASE_AND_PERSISTENCE.md
- docs/architecture/UI_AND_FRAMEWORK.md
- docs/architecture/DEPENDENCIES.md
- docs/architecture/MODULE_RISK_MAP.md

For legacy changes, explicitly re-check shared-class blast radius, Oracle/Hibernate/JDBC transaction behavior, Swing threading, wrapper-framework integration, Ops workflows, reports, audit/history, and module risk/test confidence.
- `docs/architecture/TESTING_AND_NON_REGRESSION.md`

When a change modifies tests, test structure, NRT module relationships, fixtures, or regression expectations, keep this document synchronized.

## GUI/database lineage documentation

Keep `docs/architecture/TRACEABILITY_GUIDE.md` synchronized when tracing mechanisms, high-value anchors, JAR/resource locations, or navigation conventions change. Do not turn it into an exhaustive table/screen mapping.

When a change affects a GUI-to-database path, screen navigation, menu registration, or database write ownership, update `docs/architecture/TRACEABILITY_GUIDE.md` and synchronize affected UI/data-flow/dependency documents. Preserve exact evidence provenance and record broken or conditional paths explicitly.

## Binary dependency documentation

When a change affects a JAR/classpath dependency, update `docs/architecture/JAR_AND_BINARY_DEPENDENCIES.md` with the relevant artifact/version, changed relationship, and evidence provenance. Do not replace valid binary evidence with unsupported source-level claims.

## Repository visibility

Also keep `docs/architecture/REPOSITORY_VISIBILITY.md` synchronized when the change affects repository scope, newly relevant projects outside the local working tree, source-visibility assumptions, or evidence provenance. Do not remove valid visibility limitations simply because the current developer checkout is partial. When relevant source is outside the working tree, preserve the distinction between Confirmed — Local, Confirmed — Git, Inferred, and Unverified.