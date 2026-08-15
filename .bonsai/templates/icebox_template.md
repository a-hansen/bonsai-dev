# AI Icebox

**Project:** <Project name>  
**[Meta: Agent-maintained | Human-triaged Deferred Observations | Non-authoritative | Not an Approved Backlog]**

## Purpose

Preserve selected out-of-scope observations that the human has explicitly chosen to remember for possible
future consideration.

The icebox is not an automatic observation log.

Agents may notice out-of-scope issues during design or implementation, but must not write them here until
the human chooses to preserve or defer them.

Do not create a project `icebox.md` merely because this template exists. Create it only when the human first
chooses to preserve an observation, and instantiate the first approved observation as `ICE-001`.

An item in the icebox is worth remembering, not approved for execution.

## Entries

### ICE-001 — <Short observation title>

**Status:** <Deferred | Promoted | Rejected | Superseded>  
**Observed During:** <Design synthesis | Phase <N> | Pass A | Pass B | Other context>  
**Observation:** <Concise independently understandable description>  
**Why Keep It:** <Why the human chose to preserve it>  
**Possible Destination:** <requirements.md | architecture.md | plan.md | code/maps | issue tracker | Unknown>

## Status Guidance

* **Deferred:** Human chose to preserve the observation for possible future consideration.
* **Promoted:** Human approved moving the item into authoritative project memory or active execution work.
* **Rejected:** Human decided not to pursue a previously preserved item.
* **Superseded:** Later project direction made the preserved item obsolete or redundant.

## Maintenance Rules

* Add an entry only after the human explicitly chooses to preserve or defer an out-of-scope observation.
* When creating `icebox.md` from this template, replace the sample `ICE-001` placeholders with the approved
  observation and project name. Do not leave unused template placeholders in the project file.
* Do not automatically create icebox entries for bugs, technical debt, missing tests, refactor opportunities,
  documentation gaps, or speculative improvements discovered during implementation.
* Do not treat icebox entries as requirements, architecture decisions, roadmap commitments, or authorized work.
* Keep entries compact, specific, and independently understandable.
* Prefer one entry per distinct observation rather than combining unrelated ideas.
* Preserve only enough context for a future human to decide whether the item still matters.
* When an entry is promoted, update its status and destination.
* Do not preserve rejected observations merely for historical completeness. Delete them when no continuing
  value remains.
* Prune superseded entries when they no longer provide useful project memory.
* Do not copy icebox entries into `state.md`, phase plans, or handoff summaries unless one becomes active work.