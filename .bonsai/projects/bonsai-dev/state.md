# AI State

**Project:** Bonsai Dev  
**[Meta: Agent-maintained | Current Session Baton Pass | Bonsai 1.4 Bootstrap Truth | Keep Minimal]**

## Bootstrap Note

This project is using Bonsai 1.4 to build Bonsai 2.0.

While Bonsai 1.4 is the active runtime, this `state.md` is the authoritative current resume state expected by v1.4.

Do not create a parallel `agent_state.md` during bootstrap.

The state is converted to `agent_state.md` during validated v2 promotion.

## Current Execution State

**Current Phase:** Context and Project Workflows
**Active Phase Plan File:** None
**Phase Plan Status:** None
**Current Phase Pass:** Phase Planning
**Phase Execution Mode:** Unresolved
**Execution Readiness:** Phase planning required
**Current Objective:** Resolve Phase 3 execution mode and draft a detailed Phase 3 plan if warranted.

* **Current Snapshot:** Phase 2 is complete. Integrated checks confirm coherent bootstrap/router/menu ownership,
  canonical paths, v2 execution-memory names, guarded later-skill references, README/specification alignment, and a
  pure five-file staged distribution. Deferred obligations remain binding: Phase 3 owns broader project-memory and
  context workflows, phase execution, final-truth, dry-run, handoff, agent context, Bonsai Home, and related
  end-to-end workflow behavior; Phase 4 owns code-map behavior; Phase 5 owns full operating-model scenario
  validation.
* **Recommended Mode:** Single-pass — Phase 3 implements already-approved artifact contracts and does not establish
  another independently review-worthy durable contract.
* **Recommended Phase Plan:** Create one — the phase has ordered workflow artifacts, multiple bounded validation
  points, and inherited deferred obligations that must remain visible across implementation steps. Treat inline
  Project Management as an existing Phase 2 dependency to integrate and validate, not reimplement; correct it only
  if Phase 3 exposes an approved-contract gap.
* **Active Files:** [`state.md`, `plan.md`, `requirements.md`, `architecture.md`, `artifact_contracts/README.md`,
  `artifact_contracts/core_workflows.md`, `artifact_contracts/project_workflows.md`, `bonsai/specification.md`,
  `bonsai/README.md`, `.bonsai/skills/phase_execution.md`, `.bonsai/templates/plan_phase_template.md`]
* **Blockers / Risks:** [None]

**Exact Next Step:** Execute Phase 3 activation planning: assess and resolve execution mode, draft a detailed
`plan/plan_phase_3.md` from the phase-plan template if warranted, assign inherited deferred obligations to concrete
owning steps or later validation, treat inline Project Management as an existing Phase 2 dependency to integrate
and validate rather than reimplement, reconcile roadmap/state, and stop at the applicable plan-review gate.
**Success Condition:** Phase 3 mode is resolved, any warranted detailed plan is complete and ready for review,
Phase 2 deferred obligations remain explicitly routed, roadmap/state agree, and no Phase 3 implementation begins
before the applicable approval gate.

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
