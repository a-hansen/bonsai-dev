# Agent Plan

**Project:** `bonsai-dev`  
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** Implement the approved workspace refactor from the shared seam outward. First establish `workspace.md`, workspace-aware startup, and implementation routing without breaking existing project startup. Then generalize shared lifecycle and handoff while preserving project-only semantics. Next move mapping onto repository-local workspace memory with scoped planning and separate generated output. Finish by reconciling creation prompts, project-map associations, documentation/category guides, stale references, and end-to-end validation. Keep each phase bounded and let Phase 1 detailed planning determine whether any independently review-worthy contract step warrants two-pass execution.

## Roadmap

### Phase Summaries

1. **Workspace Foundation and Routing:** Establish the project/map workspace contract, add `workspace.md`, refactor startup and implementation routing around active workspace identity, preserve ordinary project startup behavior, and prove the basic project/map resolution seam. | **Mode:** `Two-pass contract-first` | **Status:** `Complete` | **Plan:** `plan/agent_plan_phase_1.md` | **Plan Status:** `Approved`
2. **Shared Lifecycle and Project Compatibility:** Generalize shared `agent_plan.md`/`agent_state.md` roles, make handoff workspace-aware, support project/map fresh-session continuation, and preserve project-specific phase, final-truth, contract, review, and completion semantics. | **Mode:** `Single-pass` | **Status:** `Complete` | **Plan:** `plan/agent_plan_phase_2.md` | **Plan Status:** `Complete`
3. **Map Workspace Execution:** Refactor code mapping around repository-local map workspaces, optional scoped detailed plans, map-specific reconciliation/completion, source/map identity, separate reusable generated output, map creation, and retirement of `map_state.md`. | **Mode:** `To determine during planning` | **Status:** `Active` | **Plan:** `None` | **Plan Status:** `None`
4. **Creation, Associations, Cleanup, and Validation:** Rework/rename project creation, add project-to-map association management, reconcile category guides and README/examples, remove stale superseded references, and validate the complete project/map workspace model in embedded and reusable-home scenarios. | **Mode:** `To determine at activation` | **Status:** `Pending` | **Plan:** `None` | **Plan Status:** `None`

## Active Phase Detail

- **Goal:** Move code mapping onto repository-local map workspaces with resumable execution memory, map-specific reconciliation, source/output identity, separate generated output, and retirement of the legacy map-state model.
- **Execution Readiness:** `Phase planning required`
- **Scope:** Repository-local map roadmap/state; optional flat scoped map plans; compatible map execution and handoff; source/map identity; generated-output separation and reconciliation; map creation; retirement of `map_state.md` and its template.
- **Approved Constraints:** Keep map behavior distinct from project phases and final truth; keep generated maps separate from workspace execution memory; preserve explicit map identity, lazy loading, source authority, and current shared lifecycle gates.
- **Planning Boundary:** Phase 3 has just become current and has no applicable approved detailed plan or lightweight execution basis. Planning must determine its execution mode and whether a detailed plan is warranted before implementation can be authorized.
- **Validation:** To be made concrete during Phase 3 planning from approved requirements, architecture, specification, current mapping artifacts, and the completed shared workspace lifecycle.
- **Done When:** To be made concrete in the approved Phase 3 execution basis without pulling Phase 4 creation, association, broad cleanup, or end-to-end work forward.

## Deferred and Completed

- **Deferred:** Creation-prompt renames/rework beyond Phase 3's map-creation scope; project map associations; documentation/reference cleanup; full workspace validation.
- **Completed:** Workspace Foundation and Routing; Shared Lifecycle and Project Compatibility; Artifact Discovery and Index Maintenance; Bonsai v2 self-hosting build, validation, promotion, fresh-session proof, and staging-tree removal.

## Maintenance Rules

- Keep this file roadmap-level; detailed sequencing belongs in a warranted phase plan.
- Keep phase, mode, plan identity/status, and readiness consistent with `agent_state.md`.
- Phase 1 always receives a reviewed `plan/agent_plan_phase_1.md` before implementation.
- Later phase plans are conditional, not automatic.
- Preserve current execution truth and compress completed detail.
