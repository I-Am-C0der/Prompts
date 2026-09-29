# Claude Code — Work Application Workflow

A reusable workflow and prompt set for analyzing, documenting, reviewing, and maintaining a medium-to-complex application with Claude Code CLI.

> **Scope:** Work-related application development only. This repository section is intentionally independent of any personal projects.

## Recommended sequence

1. `01-initial-reconnaissance.md` — understand the application without changing source.
2. `02-create-architecture-reference.md` — create persistent architecture documentation.
3. `03-create-claude-md.md` — create a concise project-level `CLAUDE.md`.
4. `04-independent-architecture-audit.md` — independently verify the documentation against source.
5. `05-code-review-guidelines.md` — establish project-specific review rules.
6. `06-standard-code-review.md` — use for normal change/PR reviews.
7. `07-pre-implementation-architecture-review.md` — use before substantial changes.
8. `08-update-architecture-docs.md` — refresh documentation after architectural changes.
9. `09-periodic-architecture-audit.md` — periodically detect architectural drift.

## Model usage

For a genuinely complex codebase, a deeper-reasoning model can be used for the initial reconnaissance, architecture documentation, independent audit, and critical subsystem analysis. Use a strong general coding model for major implementation/refactoring work and a faster model for routine reviews and smaller changes.

The prompts deliberately require Claude to distinguish:
- confirmed facts from source code
- reasonable inferences
- unresolved/uncertain areas

The source code remains authoritative when documentation and implementation disagree.

## Persistent documentation layout

The architecture workflow creates:

```
docs/
└── architecture/
    ├── CODEBASE_OVERVIEW.md
    ├── ARCHITECTURE.md
    ├── MODULES.md
    ├── DATA_FLOW.md
    ├── DEPENDENCIES.md
    ├── KNOWN_ISSUES.md
    └── CODE_REVIEW_GUIDELINES.md
```

Keep `CLAUDE.md` concise. It should contain project instructions and references to the architecture documents rather than duplicating the entire architecture.
