# Agent Plan

**Project:** `bonsai-dev`  
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** Implement the approved workspace refactor from the shared seam outward. First establish `workspace.md`, workspace-aware startup, and implementation routing without breaking existing project startup. Then generalize shared lifecycle and handoff while preserving project-only semantics. Next move mapping onto repository-local workspace memory with scoped planning and separate generated output. Finish by reconciling creation prompts, project-map associations, documentation/category guides, stale references, and end-to-end validation. Keep each phase bounded and let Phase 1 detailed planning determine whether any independently review-worthy contract step warrants two-pass execution.

## Roadmap

### Phase Summaries

1. **Workspace Foundation and Routing:** Establish the project/map workspace contract, add `workspace.md`, refactor startup and implementation routing around active workspace identity, preserve ordinary project startup behavior, and prove the basic project/map resolution seam. | **Mode:** `Two-pass contract-first` | **Status:** `Complete` | **Plan:** `plan/agent_plan_phase_1.md` | **Plan Status:** `Approved`
2. **Shared Lifecycle and Project Compatibility:** Generalize shared `agent_plan.md`/`agent_state.md` roles, make handoff workspace-aware, support project/map fresh-session continuation, and preserve project-specific phase, final-truth, contract, review, and completion semantics. | **Mode:** `To determine during planning` | **Status:** `Active` | **Plan:** `None` | **Plan Status:** `None`
3. **Map Workspace Execution:** Refactor code mapping around repository-local map workspaces, optional scoped detailed plans, map-specific reconciliation/completion, source/map identity, separate reusable generated output, map creation, and retirement of `map_state.md`. | **Mode:** `To determine at activation` | **Status:** `Pending` | **Plan:** `None` | **Plan Status:** `None`
4. **Creation, Associations, Cleanup, and Validation:** Rework/rename project creation, add project-to-map association management, reconcile category guides and README/examples, remove stale superseded references, and validate the complete project/map workspace model in embedded and reusable-home scenarios. | **Mode:** `To determine at activation` | **Status:** `Pending` | **Plan:** `None` | **Plan Status:** `None`

## Active Phase Detail

- **Goal:** Generalize the common plan/state and handoff lifecycle for both workspace types while preserving every project-only phase, final-truth, contract, review, and completion rule.
- **Execution Readiness:** `Phase planning required`
- **Scope:** Shared `agent_plan.md`/`agent_state.md` roles; workspace-aware handoff and fresh-session continuation; project compatibility across the existing implementation and phase-execution workflows; focused lifecycle validation established during planning.
- **Approved Constraints:** Share only mechanics genuinely common to projects and maps; keep project phase/final-truth behavior project-specific; keep map source/output behavior map-specific; preserve session-local workspace identity, lazy loading, and one-step auto-execute gates.
- **Planning Boundary:** Phase 2 has just become current and has no applicable approved detailed plan or lightweight execution basis. Planning must determine the appropriate execution mode and whether a detailed plan is warranted before implementation can be authorized.
- **Validation:** To be made concrete during Phase 2 planning from approved requirements, architecture, specification, and the current lifecycle artifacts.
- **Done When:** Shared lifecycle and handoff behavior supports project and map workspaces without weakening existing project gates, and the resulting checks demonstrate safe current-session and fresh-session continuation for both types.

## Deferred and Completed

- **Deferred:** Map-workspace execution and detailed planning; `map_state.md` retirement; creation-prompt renames/rework; project map associations; documentation/reference cleanup; full workspace validation.
- **Completed:** Workspace Foundation and Routing; Artifact Discovery and Index Maintenance; Bonsai v2 self-hosting build, validation, promotion, fresh-session proof, and staging-tree removal.

## Maintenance Rules

- Keep this file roadmap-level; detailed sequencing belongs in a warranted phase plan.
- Keep phase, mode, plan identity/status, and readiness consistent with `agent_state.md`.
- Phase 1 always receives a reviewed `plan/agent_plan_phase_1.md` before implementation.
- Later phase plans are conditional, not automatic.
- Preserve current execution truth and compress completed detail.
