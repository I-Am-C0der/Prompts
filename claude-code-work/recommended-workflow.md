# Recommended Workflow

## Initial setup

Run these in order:

1. `01-initial-reconnaissance.md`
2. `02-create-architecture-reference.md`
3. `03-create-claude-md.md`
4. `04-independent-architecture-audit.md`
5. `05-code-review-guidelines.md`

This creates a persistent baseline that future Claude Code sessions can reuse.

## During feature development

Before a substantial feature:
- `07-pre-implementation-architecture-review.md`

After implementation:
- `06-standard-code-review.md`
- `08-update-architecture-docs.md`

## For routine PRs

Use:
- `06-standard-code-review.md`

Claude should read `CLAUDE.md` and the relevant architecture documents before reviewing.

## Periodically

Run:
- `09-periodic-architecture-audit.md`

A practical cadence is after several significant changes, major releases, or whenever the architecture documentation starts feeling stale.

## Why this structure works

The architecture documents act as persistent context across Claude Code sessions.

`CLAUDE.md` stays short and operational, while the deeper architecture knowledge lives in `docs/architecture/`.

The source remains the authority. Documentation is a maintained reference, not a substitute for reading code.

## Suggested model allocation

Use the strongest available reasoning model for:
- initial deep reconnaissance of a complex application
- architecture extraction
- independent architecture audits
- difficult subsystem analysis

Use a strong coding model for:
- major feature implementation
- large refactors
- difficult debugging
- complex code reviews

Use a faster model for:
- routine PR reviews
- small changes
- documentation maintenance
- straightforward questions

Do not choose a more expensive model merely because it is available; use deeper reasoning where the additional analysis materially reduces risk.
