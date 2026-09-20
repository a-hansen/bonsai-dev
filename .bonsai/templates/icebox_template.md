# Bonsai Icebox

**Project:** <Project name>  
**[Meta: Human-owned | Human-triaged Deferred Observations | Non-authoritative | Not an Approved Backlog]**

## Purpose

Preserve selected out-of-scope observations that the human explicitly chose to retain for possible later triage.

The icebox is not an automatic observation log, requirement source, architecture source, roadmap, or execution
plan. Preservation records that an item may be worth reconsidering; it does not authorize implementation.

Do not create a project `icebox.md` merely because this template exists. Create it only when the human first
authorizes preservation, and replace the entry below with that observation as `ICE-001`.

## Entries

### ICE-001 — <Short observation title>

**Status:** <Deferred | Promoted | Rejected | Superseded>  
**Observed During:** <Phase, pass, workflow, or other concise context>  
**Observation:** <Concise independently understandable description>  
**Why Keep It:** <Why the human chose to preserve it>  
**Possible Destination:** <Requirements | Architecture | Roadmap | Phase plan | Code or maps | Issue tracker | Unknown>

## Status Guidance

- **Deferred:** The human chose to preserve the observation for possible future consideration.
- **Promoted:** The human authorized moving it through the applicable design, roadmap, planning, or execution gate.
- **Rejected:** The human decided not to retain or pursue it.
- **Superseded:** Later project truth or another retained item made it obsolete or redundant.

## Maintenance Rules

- Instantiate the project name and every `ICE-001` field when creating `icebox.md`; leave no template
  placeholders in the project file.
- Add an entry or change its durable meaning only after explicit human authorization.
- Do not automatically preserve bugs, technical debt, missing tests, refactor opportunities, documentation gaps,
  or speculative improvements.
- Do not treat an entry as approved requirements, architecture, roadmap, planned work, or execution authority.
- Do not copy entries into `agent_plan.md`, `agent_state.md`, phase plans, or handoff summaries unless an item is
  separately promoted through its owning gate.
- Keep entries compact, specific, independently understandable, and distinct.
- Assign later entries the next unused `ICE-<NNN>` identifier.
- When an entry is promoted, record its actual destination.
- Remove rejected entries and prune superseded entries when they have no continuing value; do not preserve
  valueless history for completeness.
