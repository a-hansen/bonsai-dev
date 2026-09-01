# AI Plan - Phase 1: Archaeology and Artifact Contracts

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**

**Project:** Bonsai Dev | **Parent:** `../../../../../../../../Users/Aaron/Desktop/.bonsai-old/projects/bonsai-dev/plan.md`

**Phase Status:** Completed

**Plan Status:** Approved

**Mode:** Single-pass

## Objective & Scope

**Objective:** Produce a reviewed, rebuildable behavioral contract layer for the Bonsai 2.0 standard by extracting mature Bonsai 1.4 behavior, reconciling it with the v2 specification, and deliberately classifying retained, adapted, retired, and missing responsibilities before staged implementation begins.

**Inputs:** [`requirements.md` REQ-5 through REQ-16 and Phase 1 Boundaries] | [`architecture.md` Distribution Purity, Golden Artifact Model, Artifact Contract Layer, Archaeological Flow, Core Workflow Decomposition, Mapping Architecture, Promotion Architecture, Fresh-Session Self-Hosting Proof, Phase Architecture, Guardrails] | [`bonsai/specification.md`] | [`bonsai/README.md`] | [Current `.bonsai/` standard artifacts] | [Seeded `artifact_contracts/`]

**In Scope:** [Complete the standard-artifact inventory, extract behavior and protected edge cases in bounded source batches, classify each material rule as Keep / Adapt / Drop / Missing, reconcile all classifications against the v2 specification, assign required v2 responsibilities to an artifact or explicitly unresolved seam, deepen the four seeded contract groups, define validation obligations for later phases, review each contract batch before using it as implementation authority]

**Out of Scope / Do Not Do Yet:** [Create or materially rewrite staged v2 standard artifacts under `bonsai/`, implement `.bonsai/start.md`, alter the running Bonsai 1.4 standard, create generated tests or output, create code maps merely to exercise mapping, finalize helper-script packaging, promote Bonsai 2.0, convert active execution-memory filenames, redesign mature map structures without archaeological evidence]

**Expected Deliverables:** [`artifact_contracts/README.md` with a closed inventory and contract-status summary, deepened `artifact_contracts/core_workflows.md`, deepened `artifact_contracts/project_workflows.md`, deepened `artifact_contracts/code_maps.md`, deepened `artifact_contracts/promotion_validation.md`, explicit validation obligations and unresolved-responsibility records sufficient for Phases 2 through 5]

## Execution Constraints

* **Implementation Scope:** `.bonsai/projects/bonsai-dev/artifact_contracts/`, this active phase plan, and execution-memory reconciliation in `.bonsai/projects/bonsai-dev/plan.md` and `.bonsai/projects/bonsai-dev/state.md`. Existing `.bonsai/` standard artifacts and the staged `bonsai/` specification/README are read-only archaeological and final-truth inputs during this phase.
* **Approved Boundaries:** `.bonsai/` remains the running Bonsai 1.4 runtime; `bonsai/` remains the temporary candidate distribution and receives no substantive implementation in Phase 1; generated output stays outside `bonsai/`; v1.4 `plan.md` / `state.md` naming remains authoritative until promotion; the v2 specification wins over archaeological evidence; artifact contracts describe behavior and may not silently revise final truth.
* **Public Contracts:** The human-owned behavioral contracts under `artifact_contracts/` are the durable design surfaces refined by this phase. No source-level API, schema, protocol, persistent format, or implementation abstraction is created.
* **Human Review Focus:** For each batch, verify that valuable v1.4 behavior and edge cases are accounted for, every classification is supported by evidence and the v2 specification, obsolete control-plane assumptions are dropped deliberately, missing v2 behavior has an appropriate owner or remains explicitly unresolved, and later validation can prove the contract without relying on chat history.

## Ordered Work

### Implementation

* **Step 1 — Close the archaeological inventory and evidence method:** Reconcile the initial inventory against the actual standard files under `.bonsai/`; identify each existing artifact, target v2 artifact or unresolved responsibility seam, applicable v2 specification sections, and destination contract group. Record the evidence discipline: source artifact and protected behavior, specification rule, Keep / Adapt / Drop / Missing classification, rationale, owning contract, and validation obligation. Treat repository-specific `.bonsai/developer_context.md` and `.bonsai/projects/` memory as context or fixtures, not distribution artifacts. | **Files:** [`.bonsai/` standard inventory, `bonsai/specification.md`, `artifact_contracts/README.md`] | **Done:** Every current standard artifact and known missing v2 responsibility is routed to a bounded batch, deliberately excluded with rationale, or recorded as an unresolved seam; no directory membership is mistaken for authority.

* **Step 2 — Extract and review the core execution cluster:** Begin archaeology with `.bonsai/implementation_prompt.md`, then inspect the directly related phase execution, final-truth, dry-run, handoff, and tooling-memory skills. Extract distributed menu rules and the missing bootstrap boundary without assuming the v1 monolith survives. Reconcile against the specification sections for startup, implementation, readiness, gates/menus, contract-first work, dry runs, observations, session boundaries, framework prompts/skills, and maintenance. Update contracts for `.bonsai/start.md`, `prompts/implementation.md`, `skills/menu.md`, `skills/phase_execution.md`, `skills/final_truth_update.md`, `skills/dry_run.md`, `skills/handoff.md`, and `skills/agent_context.md`. | **Status:** Completed; Contract Batch Approved | **Files:** [`.bonsai/implementation_prompt.md`, `.bonsai/skills/phase_execution.md`, `.bonsai/skills/final_truth_update.md`, `.bonsai/skills/dry_run.md`, `.bonsai/skills/handoff.md`, `.bonsai/skills/tooling_memory.md`, `artifact_contracts/core_workflows.md`, `artifact_contracts/README.md`] | **Done:** Core startup/routing/gate behavior and protected edge cases are explicitly classified; startup identity and implementation routing have a clear boundary; reusable menu behavior is assigned; operational-memory behavior is reconciled with scoped agent context; the human reviewed and approved the batch before project/context archaeology proceeds.

* **Step 3 — Extract and review project, context, and template workflows:** Inspect project-memory synthesis, standard context examples, phase/icebox templates, and user-facing v1 guidance relevant to project workflows. Reconcile against specification sections for Bonsai environments, projects, ownership, final truth, execution memory, developer/agent context, context layering, lazy loading, project-memory creation, and templates. Decide the smallest justified ownership seams for Manage Projects, Create Bonsai Home, and developer-context layering without inventing files merely to complete the inventory. Classify the existing `task-tracker` project only as possible later validation material; do not convert it automatically. | **Status:** Completed; Contract Batch Approved | **Files:** [`.bonsai/design_session.md`, `.bonsai/README.md`, `.bonsai/developer_context.example.md`, `.bonsai/templates/plan_phase_template.md`, `.bonsai/templates/icebox_template.md`, `artifact_contracts/core_workflows.md`, `artifact_contracts/project_workflows.md`, `artifact_contracts/README.md`] | **Done:** Project-memory creation and template contracts cover preserved synthesis behavior; all three missing/context responsibility seams are assigned with no remaining Step 3 ownership decision; v2 ownership differences are explicit; cross-batch core delegation wording is reconciled; the human approved the batch before mapping archaeology proceeds.

* **Step 4 — Perform mapping archaeology as a distinct bounded batch:** Only after the core control-plane boundary is reviewed, inspect `.bonsai/maps/repo_session.md`, `.bonsai/maps/map_prompt.md`, `.bonsai/maps/README.md`, and the existing templates. Process `.bonsai/maps/map_system.md` in bounded sections covering file/layer responsibilities, evidence discipline, editing rules, mapping targets, build order, compression, done criteria, update triggers, prioritization, drift prevention, naming, and operating stance. Reconcile each candidate against the specification's Code Maps, Integrated Mapping Workflow, Manage Code Maps, multi-repository source-universe, archaeological-work, and map-maintenance rules. Preserve mature data structures only when their navigation value survives the v2 source/project/context identity changes. Explicitly verify the known archaeological naming/reference defects around stale `repo_prompt.md`, nonexistent `templates/map_repo_template.md`, and `templates/symbol_index.tsv` versus `symbol_index_template.tsv`; derive intended behavior from actual artifacts and consumers, do not preserve compatibility names or invent artifacts to repair v1 drift, record resulting identity/ownership decisions, and require validation against stale references and divergent artifact identities. Preserve the v2 decision that map creation and maintenance are user-directed/contextual rather than automatic or continuous. | **Status:** Completed; Contract Batch Approved | **Files:** [`.bonsai/maps/repo_session.md`, `.bonsai/maps/map_prompt.md`, `.bonsai/maps/map_system.md`, `.bonsai/maps/README.md`, `.bonsai/maps/templates/`, `artifact_contracts/code_maps.md`, `artifact_contracts/README.md`] | **Done:** Every material mapping rule and existing map artifact is classified; control-plane behavior is separated from reusable map-data behavior; source identity, map-store placement, project calibration, agent-context integration, evidence authority, and maintenance triggers are contractually clear; optional lookup artifacts remain optional unless evidence justifies them; known stale references and naming drift have evidence-based identity decisions and recurrence-prevention validation obligations; the human reviewed and approved the batch before promotion/validation archaeology proceeds.

* **Step 5 — Extract and review validation and promotion obligations:** Reconcile requirements and architecture for distribution purity, test/output separation, rollback, candidate construction, preservation boundaries, execution-memory conversion, live promotion, fresh-session proof, and post-promotion collapse against the specification's validation cases and clean-rebuild objective. Identify behaviors with no v1 artifact as Missing rather than manufacturing implementation seams. Define what later tests must prove while leaving test harnesses, generated outputs, exact helper packaging, and live promotion unimplemented. | **Status:** Completed; Contract Batch Approved | **Files:** [`requirements.md`, `architecture.md`, `bonsai/specification.md`, `artifact_contracts/promotion_validation.md`, `artifact_contracts/README.md`] | **Done:** Promotion and validation contracts state inputs, exact memory classification/conversion policy, prohibited partial states, verified backup/rollback conditions, transactional swap invariants, v1.4-to-v2 execution-memory conversion expectations, fresh-session self-hosting acceptance, staging-removal boundary, and later validation obligations; host-specific swap/helper packaging remains explicit, and the current `task-tracker` example has a required pre-promotion disposition gate rather than automatic conversion or silent loss; the human reviewed and approved the batch before cross-contract closure proceeds.

* **Step 6 — Close cross-contract coverage and Phase 1 review:** Check every implemented or required standard artifact against the contract schema: role, trigger, inputs, responsibilities, prohibitions, reads, writes, delegation, human gates, preserved behavior, v2 changes, and validation. Check cross-artifact ownership for gaps and duplication; reconcile user-facing promises in `bonsai/README.md`; ensure every Drop has a specification-based rationale and every Missing responsibility has an owner or explicit unresolved decision. Produce a concise contract coverage/status summary and validation trace for later phases. If archaeology exposes a specification clarification or revision, stop and route it through final-truth reconciliation instead of editing the specification implicitly. | **Status:** Completed; final Phase 1 review approved | **Files:** [`artifact_contracts/README.md`, `artifact_contracts/core_workflows.md`, `artifact_contracts/project_workflows.md`, `artifact_contracts/code_maps.md`, `artifact_contracts/promotion_validation.md`, `bonsai/specification.md`, `bonsai/README.md`] | **Done:** The complete contract layer is reviewable and sufficient to rebuild the staged standard without chat memory or blind copying; all batch reviews are resolved; Phase 1 final review confirms readiness to activate Phase 2 or records explicit blockers.

## Validation & Done Criteria

* **Validation Strategy:** Inventory comparison against `rg --files` output for the actual `.bonsai/` standard; source-to-contract trace review for each batch; contract-schema completeness check for each target artifact or unresolved seam; cross-check against all applicable `bonsai/specification.md` sections and user-facing `bonsai/README.md`; targeted searches for unclassified `TBD`, `TODO`, unresolved, missing, obsolete v1 names, and unstated validation obligations; human review at the end of each bounded batch and final Phase 1 coverage review.
* **Architecture Validation:** Confirm `.bonsai/` was not modified as a standard implementation, `bonsai/` received no substantive implementation or generated output, execution memory retained v1.4 names, the specification remained authoritative, map data was not redesigned without archaeological evidence, and contract grouping did not become an invented runtime module boundary.
* **Definition of Done:** [Every existing standard artifact is inventoried and classified, every v2 target artifact or required unresolved seam has an identifiable complete contract, high-value v1.4 behavior and edge cases are preserved or deliberately retired, conflicts resolve in favor of approved v2 final truth, missing responsibilities are assigned or explicitly blocked on a named human decision, later-phase validation obligations are traceable, all contract batches and the complete layer have been reviewed, no substantive staged v2 implementation occurred]

## Context & Wrap-up

* **Dependencies:** [Approved Bonsai v2 requirements and architecture, authoritative `bonsai/specification.md`, current `bonsai/README.md`, readable Bonsai 1.4 archaeological artifacts, seeded artifact contracts, human contract review at bounded gates]
* **Risks:** [Mature behavior may be implicit across several v1 files, the monolithic v1 control plane may obscure the correct v2 owner, `map_system.md` volume may encourage shallow extraction, user-facing guidance may promise behavior absent from the specification or contracts, contract groups may accidentally be treated as implementation modules, unresolved promotion mechanics may be decided prematurely]
* **Open Questions:** [Smallest source-identity metadata shape and dependency-to-map resolution mechanics to validate through later multi-repository work, safest host-specific swap mechanism for Phase 5, helper-script packaging where the specification intentionally remains unresolved, approved fixture relocation/adaptation or retirement of the v1.4 `task-tracker` example before live promotion]
* **Completion Summary:** **Outcome:** All 23 v1.4 standard artifacts and all known missing v2 responsibilities were
  classified and routed; four bounded contract batches were approved; cross-contract schema, ownership,
  user-guide conformance, and later-phase validation traces were closed and approved without staged implementation.
  **Unlocked:** Phase 2 bootstrap and core execution activation planning from the approved contract layer.

## Maintenance Rules

* Treat this file as the authoritative detailed execution plan for this phase.
* Keep `plan.md` at roadmap level. Do not duplicate phase-level sequencing there.
* Keep `state.md` aligned with this file for:
    * phase-plan approval state,
    * current pass,
    * exact next step,
    * review-gate status,
    * blockers,
    * phase completion state.
* Preserve approved project architecture and contracts during execution.
* Do not introduce interfaces, abstraction layers, adapters, builders, dependency constraints, or other
  structures merely to satisfy Bonsai workflow.
* Implementation style and test style follow project conventions, approved project memory,
  developer context, and applicable external skills.
* If required behavior conflicts with approved architecture or an approved contract, stop and require
  phase-plan correction, final-truth clarification, or final-truth revision before continuing.
* When a review gate, blocker state, phase status, or plan approval state changes, verify whether `state.md`
  and `plan.md` require corresponding updates.
* If this phase plan becomes incomplete, stale, or inconsistent with current approved project direction,
  correct it before substantive phase execution continues.
* Set `Plan Status: Approved` only after explicit human approval.
* Compress completed phase detail when it no longer helps execution, while preserving enough summary
  to explain the outcome and what it unlocked.
