# AI Plan

**Project:** <Project name>  
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** <Short statement of execution strategy, sequencing logic, and how phases reduce risk>

## Roadmap

### Phase Summaries

1. **<Phase 1 Name>:** <Objective> |
   **Mode:** <To determine at activation / Single-pass / Two-pass contract-first> |
   **Status:** <Pending / Active / Awaiting Review / Blocked / Complete> |
   **Plan:** <`plan/plan_phase_<N>.md` or `None`> |
   **Plan Status:** <None / Draft / Ready for Review / Approved / Superseded>
2. **<Phase 2 Name>:** <Objective> |
   **Mode:** <To determine at activation / Single-pass / Two-pass contract-first> |
   **Status:** <Pending / Active / Awaiting Review / Blocked / Complete> |
   **Plan:** <`plan/plan_phase_<N>.md` or `None`> |
   **Plan Status:** <None / Draft / Ready for Review / Approved / Superseded>

## Active Phase Detail

*(Use ONLY if the active phase does not have a separate `plan/plan_phase_<N>.md` file. Otherwise
write: "See active phase plan file.")*

* **Goal:** <Concrete phase outcome>
* **Execution Readiness:** <Design required / Phase planning required / Awaiting human review / Ready to execute / Blocked / Complete>
* **Scope:** [Implementation areas this phase may touch, if known]
* **Approved Constraints:** [Relevant architectural or dependency constraints, or `None`]
* **Ordered Steps:**
    1. <Step>
    2. <Step>
* **Validation:** [List phase-level checks or review gates]
* **Done When:** [List completion conditions]

## Deferred & Completed

* **Deferred:** [List intentionally postponed roadmap items]
* **Completed:** [Phase Name] -> Unlocked: [What it enabled]

## Maintenance Rules

* Keep this file focused on the durable execution roadmap, not current-session handoff details.
* Current session status, exact next action, blockers, current pass state, and active dry-run baseline belong in `state.md`.
* Keep phase status, execution mode, phase-plan references, and phase-plan approval state consistent with `state.md`.
* When `state.md` records a phase-level or pass-level transition, verify whether this roadmap also requires a corresponding update.
* Add a separate `plan/plan_phase_<N>.md` when a phase requires detailed sequencing, a durable contract review gate,
  multiple meaningful review or validation gates, or enough execution detail that it would bloat this file.
* Do not create a phase plan merely to document ordinary implementation decomposition.
* When a `plan/plan_phase_<N>.md` file exists, treat it as the authoritative detailed execution plan for that phase.
  Do not partially duplicate phase-level sequencing here.
* If an active phase plan file exists but is incomplete, stale, or inconsistent with current approved
  project direction, update that phase plan rather than expanding `Active Phase Detail`.
* Use `Mode: To determine at activation` when execution mode should be resolved closer to implementation
  rather than guessed prematurely.
* A phase plan marked `Draft` or `Ready for Review` is not implementation authorization.
* A phase plan marked `Approved` has completed its planning gate. If no other blocker or contract gate remains,
  `state.md` should make the next executable step explicit and mark execution readiness accordingly.
* Compress completed phase detail aggressively once it no longer helps execution.