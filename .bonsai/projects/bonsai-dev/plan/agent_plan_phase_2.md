# Agent Plan - Phase 2: Shared Lifecycle and Project Compatibility

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**
**Project:** `bonsai-dev` | **Parent:** `../agent_plan.md`
**Phase Status:** Complete
**Plan Status:** Complete
**Mode:** Single-pass

## Objective & Scope

**Objective:** Make the common workspace lifecycle and handoff behavior work for both projects and maps while preserving every project-only planning, final-truth, contract, review, and completion gate.
**Inputs:** Approved `.bonsai/specification.md`, `requirements.md`, and `architecture.md`; the active Phase 2 roadmap; the completed Phase 1 workspace-entry/routing seam; current `.bonsai/prompts/implementation.md`, `.bonsai/skills/handoff.md`, `.bonsai/skills/phase_execution.md`, and `.bonsai/skills/menu.md`; existing dependency-free workspace validation.
**In Scope:** Generalize shared `agent_plan.md`/`agent_state.md` reconciliation and handoff around the active workspace; branch explicitly into project- and map-specific completion rules; support current-session and fresh-session one-step continuation for both types; preserve project lifecycle behavior across implementation, phase execution, and handoff; add focused lifecycle validation; reconcile execution memory.
**Out of Scope / Do Not Do Yet:** Map source inspection, generated-map creation or maintenance, map/source identity implementation, scoped map-plan execution, or `map_state.md` retirement; project/map creation prompt renames or rework; project-to-map associations; README or broad stale-reference cleanup; migration of unrelated project or map memory; generic workspace types, registries, or storage; changes to human-owned final truth.
**Expected Deliverables:** Workspace-aware `.bonsai/skills/handoff.md`; only the bounded compatibility updates actually required in `.bonsai/prompts/implementation.md`, `.bonsai/skills/phase_execution.md`, and `.bonsai/skills/menu.md`; focused `tests/bonsai_workspace_lifecycle.py`; reconciled `.bonsai/projects/bonsai-dev/agent_plan.md`, `.bonsai/projects/bonsai-dev/agent_state.md`, and this phase plan.

## Execution Constraints

- **Implementation Scope:** The active standard's shared lifecycle, handoff, continuation, and project-compatibility instruction surfaces; focused isolated validation; this project's agent-owned execution memory.
- **Approved Boundaries:** Common behavior may own only workspace-wide plan/state reconciliation, readiness, exact-next-step derivation, common gate mechanics, and continuation. Project phase, final-truth, contract, icebox, and body-of-work completion remain project-specific. Map source/output identity, generated-output reconciliation, scoped map planning, and mapping-scope completion remain map-specific. Active workspace identity and auto-execute authorization remain session-local. The implementation must keep lazy loading and must not make Phase 3 map execution appear available before its owning workflow is compatible.
- **Durable Contracts:** None newly established. This phase implements the already approved workspace lifecycle and continuation contracts in project truth and `specification.md`; it must not introduce a new format, API, schema, protocol, extension point, or integration seam.
- **Human Review Focus:** Confirm that single-pass execution is appropriate; the planned shared/project/map ownership split matches approved truth; handoff and fresh-session continuation cover both workspace types without granting extra authorization; project-only gates remain intact; and Phase 3 mapping work stays deferred.

## Ordered Work

### Implementation

- **Step 1 — Generalize shared handoff and continuation:** **Status:** Complete | Make handoff consume active workspace identity and common execution memory, reconcile common state before explicit project/map branches, preserve the correct workspace-specific completion rules, and generate exact current-session/fresh-session choices for either type. Add focused lifecycle fixtures for shared reconciliation, project/map branching, one-step authorization expiry, mandatory-gate suppression, session-local identity, and exact project/map resume prompts. | **Files:** `.bonsai/skills/handoff.md`, `tests/bonsai_workspace_lifecycle.py` | **Done:** The handoff surface no longer assumes every workspace is a project; both types receive the approved common lifecycle; map handoff does not inherit project phases or final-truth rules; project behavior remains present; and the 11-case focused lifecycle harness passes.
- **Step 2 — Reconcile surrounding project compatibility:** **Status:** Complete | Compare implementation routing, phase execution, and menu behavior with the generalized handoff contract; make only required bounded updates so project startup, planning, contract review, phase completion, handoff return, and one-step continuation remain unchanged while map routing reaches only compatible common behavior. Extend focused validation for project review/blocker gates and the explicit unavailable-map-workflow boundary that remains until Phase 3. | **Files:** `.bonsai/prompts/implementation.md`, `.bonsai/skills/phase_execution.md`, `.bonsai/skills/menu.md`, `.bonsai/skills/handoff.md`, `tests/bonsai_workspace_lifecycle.py` | **Done:** The shared menu now preserves either project or map identity for ordinary resume; focused project review/blocker and incompatible-map assertions cover the already-aligned implementation, phase-execution, and handoff boundaries; and the 14-case lifecycle harness passes without pulling Phase 3 work forward.
- **Step 3 — Validate and reconcile Phase 2:** **Status:** Complete | Run the Phase 1 startup suite and the new lifecycle suite, perform focused prompt/truth and reference checks, classify actual final-truth impact, reconcile any materially affected category guide through its owning workflow, and update current execution memory before deriving Phase 3's actual planning gate. | **Files:** `tests/bonsai_workspace_foundation.py`, `tests/bonsai_workspace_lifecycle.py`, `.bonsai/projects/bonsai-dev/agent_plan.md`, `.bonsai/projects/bonsai-dev/agent_state.md`, `.bonsai/projects/bonsai-dev/plan/agent_plan_phase_2.md`; a category guide only if its routing description became materially inaccurate | **Done:** All 19 startup and 14 lifecycle cases pass; 10 focused truth/reference anchors and the scoped diff check pass; skills-guide coverage is complete at 9/9 and its routing descriptions remain accurate without an edit; actual final-truth impact is `None`; execution memory agrees that Phase 2 is complete and Phase 3 is active at its planning gate.

## Validation & Done Criteria

- **Validation Strategy:** Use dependency-free Python fixtures to inspect the active Markdown standard and model project/map lifecycle decisions without invoking an agent; cover executable continuation, mandatory review/blocker suppression, exact fresh-session prompt construction, and non-persistence of workspace identity; rerun the Phase 1 startup/routing suite; apply focused reference searches and `git diff --check` to the authorized change set.
- **Architecture / Contract Validation:** Verify shared handoff depends on active workspace identity plus common `agent_plan.md`/`agent_state.md`; project and map reconciliation remain explicit branches; projects retain phase planning, final-truth, durable-contract, review, icebox, and roadmap-exhaustion semantics; maps do not acquire them; map-specific source/output reconciliation stays delegated; fresh-session auto-execute authorizes exactly one reconstructed action and preserves explicit map identity.
- **Definition of Done:** Project and map workspaces share handoff, readiness, exact-next-step resumption, current-session continuation, and fresh-session one-step continuation; project lifecycle gates behave as before; incomplete Phase 3 map execution is not fabricated; focused startup and lifecycle validation passes; any required category-guide reconciliation is complete; actual final-truth impact is reconciled.

## Context & Wrap-up

- **Dependencies:** Approved workspace-refactor specification and project final truth; completed Phase 1 routing seam; current active standard artifacts; Python 3 standard library for focused validation.
- **Risks:** Markdown instructions are the executable workflow surface, so ambiguous common-versus-specific ownership can silently weaken project gates or imply premature map support; fresh-session wording can accidentally persist volatile state or broaden one-step authorization; current user-owned unrelated worktree changes must remain untouched.
- **Open Questions:** None.
- **Completion Summary:** **Outcome:** Complete; shared handoff and menu preserve project/map reconciliation, mandatory project gates, compatible-map boundaries, and exact continuation semantics. Validation passed 19 startup cases, 14 lifecycle cases, 10 focused truth/reference anchors, scoped diff checking, and 9/9 skills-guide coverage; final-truth impact was `None`, and no guide edit was required. | **Unlocked:** Phase 3, Map Workspace Execution, is active at its required planning gate.

## Maintenance Rules

- Treat this file as agent-owned active execution memory, not product or architecture truth.
- Keep `agent_plan.md` roadmap-level; do not duplicate this plan's detailed sequencing there.
- Keep `agent_state.md`, `agent_plan.md`, and this plan aligned for phase, mode, plan status, pass, review state, readiness, blockers, and exact next step.
- Preserve approved project final truth, contracts, and boundaries during execution.
- Do not introduce interfaces, adapters, builders, abstraction layers, dependency constraints, or other structure merely to satisfy Bonsai workflow.
- Follow project conventions and relevant source, developer-context, and agent-context guidance for implementation and testing style.
- If required behavior conflicts with approved final truth or a durable contract, stop for phase-plan correction, final-truth reconciliation, or renewed contract review as applicable.
- Set `Plan Status: Ready for Review` only when drafting is complete and approval is required. Set `Approved` only after explicit human approval.
- Reconcile execution memory whenever a gate or current execution fact changes. Correct a stale or inconsistent plan before substantive execution continues.
- Compress completed detail when it no longer helps resumption; preserve only enough summary to explain the outcome and next capability.
