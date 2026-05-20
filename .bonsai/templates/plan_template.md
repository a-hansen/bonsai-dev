# AI Plan

**Project:** <Project name>  
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** <Short statement of execution strategy, sequencing logic, and how phases reduce
risk>

## Roadmap

### Phase Summaries

1. **<Phase 1 Name>:** <Objective> | **Mode:** <To determine at activation / Single-pass / Two-pass contract-first> |
   **Status:** <Pending / Active / Awaiting Review / Blocked / Complete> |
   **Plan:** <`plan/plan_phase_<N>.md` or `None`>
2. **<Phase 2 Name>:** <Objective> | **Mode:** <To determine at activation / Single-pass / Two-pass contract-first> |
   **Status:** <Pending / Active / Awaiting Review / Blocked / Complete> |
   **Plan:** <`plan/plan_phase_<N>.md` or `None`>

## Active Phase Detail

*(Use ONLY if the active phase does not have a separate `plan/plan_phase_<N>.md` file. Otherwise
write: "See active phase plan file.")*

* **Goal:** <Concrete phase outcome>
* **Ordered Steps:**
    1. <Step>
    2. <Step>
* **Validation:** [List phase-level tests, checks, or review gates]
* **Done When:** [List completion conditions]

## Deferred & Completed

* **Deferred:** [List intentionally postponed items]
* **Completed:** [Phase Name] -> Unlocked: [What it enabled]

## Maintenance Rules

* Keep this file focused on the durable execution roadmap, not current-session handoff details.
* Current session status, exact next action, blockers, current pass state, and recommended AI level belong in `state.md`.
* Keep phase status, execution mode, and active phase plan references consistent with `state.md`.
* When `state.md` records a phase-level or pass-level transition, verify whether this roadmap also requires a corresponding update.
* Add a separate `plan/plan_phase_<N>.md` when a phase requires deep sequencing, two-pass execution,
  multiple meaningful review or validation gates, or enough detail that it would bloat this file.
* When a `plan/plan_phase_<N>.md` file exists, treat it as the authoritative detailed plan for that phase.
  Do not partially duplicate phase-level sequencing here.
* If an active phase plan file exists but is incomplete, stale, or inconsistent with current approved
  project direction, update that phase plan rather than expanding `Active Phase Detail`.
* Use `Mode: To determine at activation` when the execution mode should be resolved closer to implementation
  rather than guessed prematurely.
* Compress completed phase detail aggressively once it no longer helps execution.