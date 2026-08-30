# AI State

**Project:** Bonsai Dev  
**[Meta: Agent-maintained | Current Session Baton Pass | Bonsai 1.4 Bootstrap Truth | Keep Minimal]**

## Bootstrap Note

This project is using Bonsai 1.4 to build Bonsai 2.0.

While Bonsai 1.4 is the active runtime, this `state.md` is the authoritative current resume state expected by v1.4.

Do not create a parallel `agent_state.md` during bootstrap.

The state is converted to `agent_state.md` during validated v2 promotion.

## Current Execution State

**Current Phase:** Integrated Code Maps
**Active Phase Plan File:** None
**Phase Plan Status:** None
**Current Phase Pass:** Phase Planning
**Phase Execution Mode:** To determine at activation
**Execution Readiness:** Phase planning required
**Current Objective:** Resolve Phase 4 execution mode and draft its detailed execution plan for human review.

* **Current Snapshot:** Phases 1–3 are complete. Phase 3 focused conformance checks passed across references,
  routing, ownership, v2 naming, lazy loading, invoking-gate return, Project Management scenarios, and staged-tree
  purity. Approved-contract gaps in active-phase-plan routing and safe confirmed project creation/design guidance
  were corrected in `bonsai/prompts/implementation.md`. Phase 4 map behavior and Phase 5 topology/promotion
  validation remain unclaimed.
* **Active Plan:** Phase 4 is active but unplanned. Recommend Single-pass because Phase 1 already approved the
  durable mapping contracts; create a detailed plan because ordered map integration and validation work materially
  benefits from a resumable execution surface.
* **Active Files:** [`state.md`, `plan.md`, `artifact_contracts/code_maps.md`, `bonsai/specification.md`,
  `bonsai/README.md`, `.bonsai/templates/plan_phase_template.md`]
* **Blockers / Risks:** [None]

**Exact Next Step:** Resolve Phase 4 as Single-pass and draft `plan/plan_phase_4.md` from the approved mapping
contracts and phase-plan template for human review.
**Success Condition:** Phase 4 mode, scope, ordered work, validation boundaries, and deferrals are reconciled across
the roadmap, state, and a complete `Ready for Review` phase plan; stop at the Phase Plan Approval Gate before map
implementation.

### Approved Dry-Run Baseline

None

## Maintenance Rules

* `state.md` describes current resume state, not session history.
* Keep only information needed for the next Bonsai 1.4 session to resume correctly.
* While v1.4 is active, do not create duplicate v2 execution-memory files.
* Replace stale facts with current truth rather than appending history.
* Keep this file short enough to read at every implementation-session startup.
* Keep phase execution mode, phase-plan approval state, and execution readiness consistent with `plan.md`.
* When an active phase plan exists, treat it as the detailed execution authority for the phase after approval.
* The v2 staged distribution lives under `bonsai/`; generated test output must not be written there.
* Promotion and execution-memory conversion do not occur until the staged v2 is validated in Phase 5.
