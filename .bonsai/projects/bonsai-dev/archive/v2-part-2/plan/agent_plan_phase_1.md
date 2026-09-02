# Agent Plan - Phase 1: Artifact Discovery and Index Maintenance

**[Meta: Agent-maintained | Completed Phase Detail | Keep Concise]**  
**Project:** bonsai-dev | **Parent:** `../agent_plan.md`  
**Phase Status:** Complete  
**Plan Status:** Approved  
**Mode:** Single-pass

## Objective & Scope

**Objective:** Implement the approved specification-first discovery model in the active Bonsai standard so contributors can route from `specification.md` to concise prompt, skill, and template guides, while authorized standard-artifact lifecycle changes reliably keep those guides accurate.  
**Inputs:** Approved `requirements.md`, `architecture.md`, and revised `<bonsai-home>/specification.md`; the active standard under `.bonsai/`; the Artifact Discovery roadmap scope.  
**In Scope:** Create the artifact-index maintenance skill and the three canonical category guides; integrate artifact-index routing and completion reconciliation into the implementation workflow; add focused validation for guide completeness, reference integrity, active-Bonsai-Home-relative identities, and the maps exclusion; reconcile execution memory at completion.  
**Out of Scope / Do Not Do Yet:** `maps/maps.md` or any global/runtime-map router; Portable Design Context; Archive workflow changes; semantic review artifacts; fresh-session continuation changes; contextual Dry Run promotion; numbered project selection; public-release README work; redesign or repurposing of unrelated standard artifacts.  
**Expected Deliverables:** `.bonsai/skills/artifact_index.md`, `.bonsai/skills/skills.md`, `.bonsai/prompts/prompts.md`, `.bonsai/templates/templates.md`; bounded integration updates to `.bonsai/prompts/implementation.md` and `.bonsai/skills/handoff.md`; focused automated validation under `tests/`; reconciled `agent_plan.md`, `agent_state.md`, and this phase plan.

## Execution Constraints

- **Implementation Scope:** The active Bonsai standard's specification-conformance artifacts, the focused validation surface, and agent-owned execution memory for this phase.
- **Approved Boundaries:** `specification.md` remains authoritative; category guides are concise routing aids rather than peer authority; artifact-index maintenance covers standard prompts, skills, and templates only; identities resolve beneath the active Bonsai Home in embedded and reusable-home modes; ordinary internal edits do not trigger guide churn; runtime code maps remain outside the feature.
- **Durable Contracts:** Implement the already-approved canonical identities `<bonsai-home>/skills/skills.md`, `<bonsai-home>/prompts/prompts.md`, `<bonsai-home>/templates/templates.md`, and `<bonsai-home>/skills/artifact_index.md`, with the approved lifecycle triggers and routing responsibilities. No additional contract gate is required.
- **Human Review Focus:** Confirm the work is single-pass and bounded; the ordered steps cover skill behavior, workflow integration, all three guides, and meaningful validation; exclusions and authority boundaries remain explicit; no deferred public-release work is absorbed.

## Ordered Work

### Implementation

- **Step 1 — Add category-guide maintenance and routing:** Create the artifact-index skill with its approved trigger, ownership, reconciliation, validation, and return rules; update the implementation kernel and handoff workflow only where needed to route qualifying lifecycle changes and prevent completion with inaccurate guides. | **Files:** `.bonsai/skills/artifact_index.md`, `.bonsai/prompts/implementation.md`, `.bonsai/skills/handoff.md` | **Done:** Authorized additions, removals, renames, and material responsibility changes to standard prompts, skills, or templates route through the owning skill before handoff can complete, while ordinary internal edits and runtime map work do not. | **Status:** Complete
- **Step 2 — Create concise category guides:** Inventory the active standard and create responsibility-oriented guides for current prompts, skills, and templates, including the new maintenance skill without making any guide self-referential or duplicating detailed workflow rules. | **Files:** `.bonsai/skills/skills.md`, `.bonsai/prompts/prompts.md`, `.bonsai/templates/templates.md` | **Done:** Each relevant current artifact is represented once in its category guide, each reference resolves relative to `<bonsai-home>`, descriptions are sufficient for routing, and no maps guide is introduced. | **Status:** Complete
- **Step 3 — Add and run focused validation:** Add a dependency-free validation check for the four canonical identities, exact category coverage, resolvable references, concise routing structure, the absence of `maps/maps.md`, and equivalent validation when the standard root is supplied as an embedded or reusable Bonsai Home. | **Files:** `tests/bonsai_artifact_discovery.py` | **Done:** Positive validation passes against the active standard and an isolated reusable-home copy; mutation cases detect a missing entry, a dangling reference, and an unexpected maps router without changing durable inputs. | **Status:** Complete
- **Step 4 — Reconcile the completed phase:** Review the implemented standard against approved requirements and architecture, classify actual final-truth impact, record actual checks, and update only current execution truth. | **Files:** `.bonsai/projects/bonsai-dev/agent_plan.md`, `.bonsai/projects/bonsai-dev/agent_state.md`, `/agent_plan_phase_1.md` | **Done:** Phase status, plan status, readiness, and exact next step agree; completed detail is concise; any required final-truth action or blocker is surfaced at its owning gate. | **Status:** Complete

## Validation & Done Criteria

- **Validation Strategy:** Run the focused standard-library validation against `.bonsai` and its isolated reusable-home fixture; exercise negative mutations for omitted, dangling, and forbidden routing entries; manually review guide descriptions and workflow routing for authority duplication and lifecycle-trigger precision.
- **Architecture / Contract Validation:** Verify all four approved canonical identities exist; guide references resolve beneath the supplied standard root; relevant prompt, skill, and template artifacts have exact guide coverage; `artifact_index.md` owns reconciliation; implementation and handoff route qualifying lifecycle changes; no `maps/maps.md` exists; no guide duplicates detailed specification or workflow behavior.
- **Definition of Done:** The active standard conforms to the approved Artifact Discovery model, focused validation passes, all required guides and maintenance routing are present and accurate, maps and deferred enhancements remain excluded, actual final-truth impact is reconciled, and execution memory records the next real work boundary.

## Context & Wrap-up

- **Dependencies:** Approved revised `specification.md`; current active standard artifact inventory; Python 3 standard library for focused validation.
- **Risks:** `None` unresolved.
- **Open Questions:** None.
- **Completion Summary:** **Outcome:** Phase complete with specification-first progressive discovery, lifecycle-owned guide reconciliation, three accurate category guides, and the explicit maps exclusion | **Checks:** `python3 tests/bonsai_artifact_discovery.py` passed for the embedded standard, an isolated reusable-home copy, and missing-entry, dangling-reference, and forbidden-maps mutations; focused manual review confirmed lifecycle-trigger precision, exact guide coverage, reference integrity, and routing-level descriptions | **Final-Truth Impact:** `None` | **Next Boundary:** No approved implementation step remains; the human must select and design the next bounded Bonsai work package before execution resumes.

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
