# AI State

**Project:** Bonsai Dev  
**[Meta: Agent-maintained | Current Session Baton Pass | Bonsai 1.4 Bootstrap Truth | Keep Minimal]**

## Bootstrap Note

This project is using Bonsai 1.4 to build Bonsai 2.0.

While Bonsai 1.4 is the active runtime, this `state.md` is the authoritative current resume state expected by v1.4.

Do not create a parallel `agent_state.md` during bootstrap.

The state is converted to `agent_state.md` during validated v2 promotion.

## Current Execution State

**Current Phase:** Validation, Promotion, and Self-Hosting Proof
**Active Phase Plan File:** None
**Phase Plan Status:** Required
**Current Phase Pass:** Not established
**Phase Execution Mode:** Unresolved
**Execution Readiness:** Phase planning required
**Current Objective:** Activate Phase 5 through execution-mode assessment and a reviewed detailed phase plan.

* **Current Snapshot:** Phases 1–4 are complete. Phase 4 focused conformance passed for the full staged mapping
  artifact graph and bounded workflow contracts. The supplied released-source scenario created a reusable `aon`
  map in the active Bonsai Home, preserved its archive unchanged, used no project/Git assumptions, and left no
  runtime map data in `bonsai/`. Full topology, automatic-discovery, promotion, and fresh-session claims remain
  unproven and belong to Phase 5.
* **Active Plan:** None. Phase 5 requires detailed sequencing and review before its multi-topology validation and
  destructive self-promotion work can execute.
* **Active Files:** [`state.md`, `plan.md`, future `plan/plan_phase_5.md`]
* **Blockers / Risks:** [Phase 5 execution mode is unresolved; no Phase 5 plan is approved]

**Exact Next Step:** Assess Phase 5 execution mode against approved project truth and existing artifact contracts,
then draft `plan/plan_phase_5.md` from the canonical template and present the Phase Plan Approval Gate.
**Success Condition:** Phase 5 has a justified execution mode and a review-ready detailed plan covering required
validation, preservation, rollback, promotion, execution-memory conversion, fresh-session proof, staging cleanup,
human gates, and explicit stop conditions without beginning destructive execution.

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
