# AI State

**Project:** Bonsai Dev  
**[Meta: Agent-maintained | Current Session Baton Pass | Bonsai 1.4 Bootstrap Truth | Keep Minimal]**

## Bootstrap Note

This project is using Bonsai 1.4 to build Bonsai 2.0.

While Bonsai 1.4 is the active runtime, this `state.md` is the authoritative current resume state expected by v1.4.

Do not create a parallel `agent_state.md` during bootstrap.

The state is converted to `agent_state.md` during validated v2 promotion.

## Current Execution State

**Current Phase:** Archaeology and Artifact Contracts  
**Active Phase Plan File:** None  
**Phase Plan Status:** None  
**Current Phase Pass:** Phase Planning  
**Phase Execution Mode:** Single-pass  
**Execution Readiness:** Phase planning required  
**Current Objective:** Draft the detailed Phase 1 archaeology/contract plan and stop for human review before standard-artifact rewriting begins.

* **Current Snapshot:** Bonsai 1.4 remains the active runtime in `.bonsai`. Bonsai 2.0 is being built in the temporary sibling `bonsai/` staging tree. `bonsai/specification.md` is v2 final truth and `bonsai/README.md` is the current v2 usage guide. The self-hosting project lives at `.bonsai/projects/bonsai-dev/` and intentionally uses v1.4 `plan.md` / `state.md` naming until promotion. Initial grouped artifact contracts have been seeded but still require Phase 1 archaeology. Generated test output will live outside `bonsai/`; eventual promotion will archive the current `.bonsai`, construct and validate a complete candidate, promote v2, convert execution-memory names, prove a fresh v2 session, and then remove staging.
* **Active Files:** [`requirements.md`, `architecture.md`, `plan.md`, `state.md`, `artifact_contracts/README.md`, `artifact_contracts/core_workflows.md`, `artifact_contracts/project_workflows.md`, `artifact_contracts/code_maps.md`, `artifact_contracts/promotion_validation.md`, `bonsai/specification.md`, `bonsai/README.md`, `.bonsai/templates/plan_phase_template.md`]
* **Blockers / Risks:** [Phase 1 cannot begin until its detailed plan is drafted and approved; primary project risk is losing mature Bonsai 1.4 behavior by simplifying or relocating it before its rationale and edge cases are captured]

**Exact Next Step:** Create `plan/plan_phase_1.md` from `.bonsai/templates/plan_phase_template.md`. The plan must sequence bounded archaeological extraction beginning with the core execution cluster, define Keep / Adapt / Drop / Missing classification and contract-review gates, keep mapping archaeology as a distinct high-volume batch, forbid substantive staged v2 implementation during Phase 1, update `plan.md` and `state.md` to record the plan as `Ready for Review`, and stop at the Phase Plan Approval Gate.  
**Success Condition:** `plan/plan_phase_1.md` exists as a reviewable Phase 1 plan, identifies the archaeological source batches and contract outputs, protects learned behavior from premature rewriting, defines how missing v2 responsibilities are assigned, keeps the staged distribution untouched except for approved project-memory/design inputs, is recorded as `Plan Status: Ready for Review`, and leaves execution readiness at `Awaiting human review`.

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
