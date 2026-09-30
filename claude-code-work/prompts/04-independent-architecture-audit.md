# 04 — Independent Architecture Audit

Perform a second, independent audit of the application's architecture and the architecture documentation.

Do not assume that the existing architecture documents are correct.

## Rules

- The current source code is authoritative.
- Read the relevant source independently before trusting documentation.
- Do NOT modify application source code.
- Correct inaccurate architecture documentation where necessary.
- Identify missing architectural knowledge.
- Distinguish confirmed facts, inferred behavior, and uncertainty.
- Do not preserve an existing statement merely because it appears in documentation.

## Audit

Compare the actual repository against:

- `CLAUDE.md`
- `docs/architecture/CODEBASE_OVERVIEW.md`
- `docs/architecture/ARCHITECTURE.md`
- `docs/architecture/MODULES.md`
- `docs/architecture/DATA_FLOW.md`
- `docs/architecture/DEPENDENCIES.md`
- `docs/architecture/KNOWN_ISSUES.md`

Check specifically for:

- incorrect component responsibilities
- missing modules
- incorrect dependency directions
- undocumented integrations
- incorrect data flows
- missing transaction boundaries
- incorrect concurrency assumptions
- undocumented failure paths
- stale configuration/build information
- missing security boundaries
- architectural risks absent from KNOWN_ISSUES
- documentation that is too detailed to remain useful

Update only the documentation necessary to make it accurate and maintainable.

Finish with:
- discrepancies found
- documentation corrected
- important knowledge still missing
- highest-risk architectural areas

## Repository visibility audit

Read `docs/architecture/REPOSITORY_VISIBILITY.md` and independently verify that it still reflects the repository structure available through Git.

Check for important modules/projects, shared/framework/build/deployment components, NRT infrastructure, and dependency relationships that may have been missed because they are not checked out locally. Use selective read-only Git inspection where needed. Do not treat local absence as repository absence or perform a full checkout merely for the audit. Record inaccessible areas as Unverified.

## Additional legacy drift checks

Explicitly audit for:
- project boundaries documented as if they were independent services
- shared classpath/package assumptions
- static/global state and singleton caches
- hidden Oracle object dependencies
- mixed Hibernate/JDBC transaction inconsistencies
- EDT/background-thread assumptions
- wrapper-framework bypasses
- missing audit/report/Ops workflow dependencies
- high-blast-radius modules with low test/documentation confidence