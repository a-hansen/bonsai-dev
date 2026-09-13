# Agent Plan

**Project:** `bonsai-dev`  
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** Implement the approved workspace refactor from the shared seam outward. First establish `workspace.md`, workspace-aware startup, and implementation routing without breaking existing project startup. Then generalize shared lifecycle and handoff while preserving project-only semantics. Next move mapping onto repository-local workspace memory with scoped planning and separate generated output. Finish by reconciling creation prompts, project-map associations, documentation/category guides, stale references, and end-to-end validation. Keep each phase bounded and let Phase 1 detailed planning determine whether any independently review-worthy contract step warrants two-pass execution.

## Roadmap

### Phase Summaries

1. **Workspace Foundation and Routing:** Establish the project/map workspace contract, add `workspace.md`, refactor startup and implementation routing around active workspace identity, preserve ordinary project startup behavior, and prove the basic project/map resolution seam. | **Mode:** `Two-pass contract-first` | **Status:** `Complete` | **Plan:** `plan/agent_plan_phase_1.md` | **Plan Status:** `Approved`
2. **Shared Lifecycle and Project Compatibility:** Generalize shared `agent_plan.md`/`agent_state.md` roles, make handoff workspace-aware, support project/map fresh-session continuation, and preserve project-specific phase, final-truth, contract, review, and completion semantics. | **Mode:** `Single-pass` | **Status:** `Complete` | **Plan:** `plan/agent_plan_phase_2.md` | **Plan Status:** `Complete`
3. **Map Workspace Execution:** Refactor code mapping around repository-local map workspaces, optional scoped detailed plans, map-specific reconciliation/completion, source/map identity, separate reusable generated output, map creation, and retirement of `map_state.md`. | **Mode:** `Single-pass` | **Status:** `Complete` | **Plan:** `plan/agent_plan_phase_3.md` | **Plan Status:** `Complete`
4. **Creation, Associations, Cleanup, and Validation:** Rework/rename project creation, add project-to-map association management, reconcile category guides and README/examples, remove stale superseded references, and validate the complete project/map workspace model in embedded and reusable-home scenarios. | **Mode:** `To determine during planning` | **Status:** `Active` | **Plan:** `None` | **Plan Status:** `None`

## Active Phase Detail

- **Goal:** Reconcile creation workflows and project-to-map associations, complete remaining documentation and stale-reference cleanup, and validate the full workspace model in embedded and reusable-home scenarios.
- **Execution Readiness:** `Phase planning required`
- **Scope:** To be bounded through Phase 4 planning from the approved roadmap, requirements, architecture, specification, and current standard state.
- **Approved Constraints:** Preserve the two concrete workspace types, repository-local execution memory, generated-map separation, session-local active identity, project-only semantics, and progressive discovery; do not infer implementation authority from this roadmap summary.
- **Planning Boundary:** Phase 4 is newly active and has no applicable approved detailed plan or lightweight execution basis. Planning must determine the execution mode, whether a detailed plan is warranted, the bounded ordered work, and the approval gate.
- **Validation:** To be proposed during Phase 4 planning against the approved end-to-end creation, association, reference-integrity, and embedded/reusable-home outcomes.
- **Done When:** To be refined into an approval-ready Phase 4 execution basis without changing approved final truth.

## Deferred and Completed

- **Deferred:** Phase 4 implementation until its execution basis is planned and approved.
- **Completed:** Workspace Foundation and Routing; Shared Lifecycle and Project Compatibility; Map Workspace Execution; Artifact Discovery and Index Maintenance; Bonsai v2 self-hosting build, validation, promotion, fresh-session proof, and staging-tree removal.

## Maintenance Rules

- Keep this file roadmap-level; detailed sequencing belongs in a warranted phase plan.
- Keep phase, mode, plan identity/status, and readiness consistent with `agent_state.md`.
- Phase 1 always receives a reviewed `plan/agent_plan_phase_1.md` before implementation.
- Later phase plans are conditional, not automatic.
- Preserve current execution truth and compress completed detail.
