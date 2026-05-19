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
2. **<Phase 2 Name>:** <Objective> | **Mode:** <Single-pass / Two-pass contract-first> |
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
* Current session status, exact next action, and recommended AI level belong in `state.md`.
* Add a separate `plan/plan_phase_<N>.md` when a phase requires deep sequencing, two-pass execution,
  or enough detail that it would bloat this file.
* Compress completed phase detail aggressively once it no longer helps execution.