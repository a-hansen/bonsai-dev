# AI State

**Project:** <Project name>  
**[Meta: Agent-maintained | Current Session Baton Pass | Volatile Operational Truth | Keep Minimal]**

## Current Execution State

**Current Phase:** <Phase Name>  
**Active Phase Plan File:** <`plan/plan_phase_<N>.md` or `None`>  
**Current Phase Pass:** <Not applicable | Phase Planning | Phase Plan Review | Pass A (Contract) | Contract Review | Pass B (Implementation) | Awaiting Review>  
**Phase Execution Mode:** <Single-pass | Two-pass contract-first | To determine at activation>  
**Current Objective:** <Single concrete objective>

* **Snapshot / Recent Work:** <2-3 lines on the current reality and the most recent meaningful work completed>
* **Active Files:** [List 3-7 resume-critical files only; not a list of every recently touched file]
* **Blockers / Risks:** [List active blockers, uncertainties, or review dependencies]

**Exact Next Step:** <Action>  
**Success Condition:** <What must be true when the next step is complete>  
**Recommended AI Level:** <Fast / Medium / Thinking / Max> - <Reason>

## Maintenance Rules

* Overwrite stale state instead of accumulating history.
* Keep this file short enough to read at every implementation-session startup.
* Use `Active Files` only for files the next implementation session is likely to resume in immediately.
* Do not use `Active Files` as a touched-files list, change log, or broad working-set inventory.
* Do not duplicate roadmap summaries from `plan.md`.
* Do not duplicate detailed phase sequencing from `plan/plan_phase_<N>.md`.
* Keep phase execution mode consistent with `plan.md` and any active `plan/plan_phase_<N>.md`.
* When recording a phase-level or pass-level transition, verify whether `plan.md` or the active phase plan also requires a corresponding update.
* Update after each meaningful execution step, review gate, blocker change, phase transition, pass transition, active phase plan change, or execution mode change.