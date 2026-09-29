# 02 — Create Persistent Architecture Reference

Using the completed codebase reconnaissance, create a persistent architecture reference for this repository.

The source code is authoritative. Do not invent behavior that cannot be supported by the repository.

## Rules

- Inspect the repository thoroughly enough to validate the reconnaissance.
- Create/update only documentation under `docs/architecture/`.
- Do NOT modify application source code.
- Clearly mark uncertainty where the source does not provide enough evidence.
- Prefer concrete references to modules/classes/packages/configuration over generic descriptions.
- Avoid documenting implementation details that are trivial or likely to become noise.
- Keep the documents useful for future code reviews and change requests.

Create these files:

### 1. CODEBASE_OVERVIEW.md

Include:
- application purpose
- major capabilities
- technology stack
- runtime/build/deployment overview
- repository structure
- major modules
- important entry points
- key external systems
- important operational characteristics

### 2. ARCHITECTURE.md

Include:
- architectural style/patterns actually present
- major components
- component responsibilities
- dependency directions
- architectural boundaries
- important interfaces
- data ownership
- persistence architecture
- integration boundaries
- synchronous/asynchronous interactions
- important cross-cutting concerns
- architectural constraints
- known architectural risks

### 3. MODULES.md

For each important module/package:
- responsibility
- important classes/components
- dependencies
- dependents
- public interfaces
- data ownership
- important invariants
- change-risk areas

### 4. DATA_FLOW.md

Document important end-to-end flows such as:
- inbound request/event
- validation
- business processing
- persistence
- external calls
- asynchronous work
- response/output
- error paths

Use Mermaid diagrams where they materially improve understanding.

### 5. DEPENDENCIES.md

Document:
- major internal dependencies
- important external libraries/frameworks
- external services
- database/storage dependencies
- messaging dependencies
- integration assumptions
- compatibility constraints

### 6. KNOWN_ISSUES.md

Document evidence-backed:
- architectural risks
- technical debt
- fragile areas
- known coupling
- reliability risks
- performance concerns
- security concerns
- testing gaps
- unresolved questions

Do not turn subjective preferences into "issues."

At the end, provide a concise summary of what was created and the most important architectural facts discovered.
