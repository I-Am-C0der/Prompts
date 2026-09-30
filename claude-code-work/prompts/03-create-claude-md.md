# 03 — Create or Update Project CLAUDE.md

Create a concise root-level `CLAUDE.md` for this repository.

## Rules

- Inspect the current repository and existing documentation first.
- If `CLAUDE.md` already exists, improve it rather than blindly replacing useful instructions.
- Keep it concise and operational.
- Do NOT duplicate the full architecture documentation.
- Do NOT modify application source code.
- Do not invent commands or conventions.

The file should contain:

1. Project purpose.
2. Technology stack.
3. Important build/test/run commands verified from the repository.
4. Coding and repository conventions that are actually established.
5. Important architectural rules and boundaries.
6. Testing expectations.
7. Security/reliability considerations.
8. Instructions for handling configuration/secrets.
9. Guidance for code reviews and substantial changes.
10. References to the persistent architecture documentation, for example:
   - `docs/architecture/CODEBASE_OVERVIEW.md`
   - `docs/architecture/ARCHITECTURE.md`
   - `docs/architecture/MODULES.md`
   - `docs/architecture/DATA_FLOW.md`
   - `docs/architecture/DEPENDENCIES.md`
   - `docs/architecture/KNOWN_ISSUES.md`
   - `docs/architecture/GUI_DATABASE_LINEAGE.md` when present

Make the instructions actionable for Claude Code. Keep architectural details in the dedicated documents.


## Legacy-specific additions

The resulting CLAUDE.md should also record concise verified rules for:
- Java 8 compatibility
- Swing EDT/background processing
- shared-project/runtime boundaries
- Oracle/Hibernate/JDBC transaction conventions
- wrapper-framework/security requirements
- cross-module impact expectations for CRs

Reference the deeper architecture documents rather than copying their details into CLAUDE.md.
## Legacy-specific additions

The resulting `CLAUDE.md` should also record concise verified rules for:
- Java 8 compatibility
- Swing EDT/background processing
- shared-project/runtime boundaries
- Oracle/Hibernate/JDBC transaction conventions
- wrapper-framework/security requirements
- cross-module impact expectations for CRs
- module-specific JUnit NRT expectations

It should explicitly point Claude to:
- `docs/architecture/TESTING_AND_NON_REGRESSION.md`
- the relevant module dossier where applicable

Keep the details in the deeper architecture documents rather than duplicating them in `CLAUDE.md`.

The resulting `CLAUDE.md` should also note that the local working tree may be partial/sparse and point Claude to `docs/architecture/REPOSITORY_VISIBILITY.md` for repository-scope and evidence-visibility guidance. It should also point to `docs/architecture/JAR_AND_BINARY_DEPENDENCIES.md` for relevant compiled dependencies when present.
