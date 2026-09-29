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
