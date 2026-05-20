# AI Icebox

**Project:** <Project name>  
**[Meta: Agent-maintained | Non-authoritative Observation Store | Human-triaged | Not an Approved Backlog]**

## Purpose

Preserve useful out-of-scope observations discovered during design or implementation without
silently expanding active scope.

The icebox is for things worth remembering, not things approved for execution.

## Entries

### ICE-001 — <Short observation title>

**Status:** <Unreviewed | Reviewed | Promoted | Rejected | Superseded>  
**Observed During:** <Design synthesis | Phase <N> | Pass A | Pass B | Other context>  
**Observation:** <Concise description of the issue, opportunity, gap, or follow-up idea>  
**Why It May Matter:** <Short explanation of possible value, risk, or future relevance>  
**Possible Destination if Promoted:** <requirements.md | architecture.md | plan.md | state.md | code/maps | issue tracker | None / Unknown>  
**Notes:** <Optional concise context, constraints, or related files>

---

### ICE-002 — <Short observation title>

**Status:** <Unreviewed | Reviewed | Promoted | Rejected | Superseded>  
**Observed During:** <Design synthesis | Phase <N> | Pass A | Pass B | Other context>  
**Observation:** <Concise description of the issue, opportunity, gap, or follow-up idea>  
**Why It May Matter:** <Short explanation of possible value, risk, or future relevance>  
**Possible Destination if Promoted:** <requirements.md | architecture.md | plan.md | state.md | code/maps | issue tracker | None / Unknown>  
**Notes:** <Optional concise context, constraints, or related files>

## Triage Guidance

* **Unreviewed:** Preserved by an agent or during synthesis; no human disposition yet.
* **Reviewed:** Human has seen it, but it has not been promoted, rejected, or superseded.
* **Promoted:** Human approved moving it into authoritative project memory or active work.
* **Rejected:** Human decided not to pursue it.
* **Superseded:** Later project direction made the observation obsolete or redundant.

## Maintenance Rules

* Add entries only for observations that are useful to preserve but outside the currently approved scope.
* Do not treat icebox entries as requirements, architecture decisions, roadmap commitments, or authorized execution work.
* Do not execute, promote, reject, or supersede entries without explicit human direction, unless the user has explicitly requested icebox triage.
* Keep entries compact, specific, and independently understandable.
* Prefer one entry per distinct observation rather than combining unrelated ideas.
* Preserve enough context that a future human review can decide whether the item matters.
* When an entry is promoted, update its status and record the authoritative destination rather than deleting it immediately.
* Prune or compress rejected and superseded entries when they no longer provide useful project memory.