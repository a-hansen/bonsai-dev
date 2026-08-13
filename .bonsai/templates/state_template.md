# AI State

**Project:** <Project name>  
**[Meta: Agent-maintained | Current Session Baton Pass | Volatile Operational Truth | Keep Minimal]**

## Current Execution State

**Current Phase:** <Phase Name>  
**Active Phase Plan File:** <`plan/plan_phase_<N>.md` or `None`>  
**Phase Plan Status:** <None / Draft / Ready for Review / Approved / Superseded>  
**Current Phase Pass:** <Not applicable | Phase Planning | Phase Plan Review | Single-pass Implementation | Pass A (Contract) | Contract Review | Pass B (Implementation) | Awaiting Review>  
**Phase Execution Mode:** <Single-pass | Two-pass contract-first | To determine at activation>  
**Execution Readiness:** <Design required | Phase planning required | Awaiting human review | Ready to execute | Blocked | Complete>  
**Current Objective:** <Single concrete objective>

* **Current Snapshot:** <1-2 lines describing only the present implementation reality needed to resume correctly>
* **Active Files:** [List 3-7 resume-critical files only; not every recently touched file]
* **Blockers / Risks:** [Active blockers, uncertainties, or review dependencies only]

**Exact Next Step:** <Action>  
**Success Condition:** <What must be true when the next step is complete>

### Approved Dry-Run Baseline

<`None`, or a compact active baseline containing only the approved basis, intended result, expected touch points, anticipated final-truth impact, and planned checks. Remove it when the work completes, is abandoned, or is redirected.>

## Maintenance Rules

* `state.md` describes current resume state, not session history.
* Keep only information needed for the next agent to resume the project correctly.
* Before every update, remove information that no longer affects resumption.
* Replace stale facts with current truth rather than appending newer versions.
* Remove completed next steps, resolved blockers, obsolete observations, superseded decisions,
  expired dry-run baselines, transient commentary, and files no longer relevant to immediate resumption.
* A fact should remain only if removing it could materially change what the next implementation session does.
* Keep this file short enough to read at every implementation-session startup.
* Use `Current Snapshot` for present reality only. Do not turn it into a recent-work log.
* Use `Active Files` only for files the next implementation session is likely to resume in immediately.
* Do not use `Active Files` as a touched-files list, change log, or broad working-set inventory.
* Do not duplicate roadmap summaries from `plan.md`.
* Do not duplicate detailed phase sequencing from `plan/plan_phase_<N>.md`.
* Keep phase execution mode, phase-plan approval state, and execution readiness consistent with
  `plan.md` and any active phase plan.
* A phase plan in `Draft` or `Ready for Review` state cannot correspond to `Execution Readiness: Ready to execute`
  unless the exact next executable work is independent of that plan.
* When recording a phase-level or pass-level transition, verify whether `plan.md` or the active phase plan
  also requires a corresponding update.
* Update after each meaningful execution step, review gate, blocker change, phase transition, pass transition,
  active phase plan change, execution mode change, or execution-readiness change.