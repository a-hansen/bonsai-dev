# AI Plan - Phase 3: Context and Project Workflows

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**  
**Project:** Bonsai Dev | **Parent:** `../../../../../../../../Users/Aaron/Desktop/.bonsai-old/projects/bonsai-dev/plan.md`  
**Phase Status:** Completed  
**Plan Status:** Approved  
**Mode:** Single-pass

## Objective & Scope

**Objective:** Complete the staged Bonsai v2 context and project workflow layer under `bonsai/`, implement the
approved Phase 1 artifact contracts owned by Phase 3, and close the Phase 2 deferred integration obligations that
can now be exercised without claiming Phase 4 map behavior or Phase 5 operating-model validation.  
**Inputs:** [`requirements.md` REQ-1–REQ-8, REQ-16] | [`architecture.md` Bootstrap Repository Model,
Distribution Purity, Authority Chain During Bootstrap, Artifact Contract Layer, Core Workflow Decomposition,
Phase Architecture] | [`artifact_contracts/core_workflows.md`] | [`artifact_contracts/project_workflows.md`] |
[`artifact_contracts/README.md` responsibility routing and Phase 3 validation trace] | [`bonsai/specification.md`
Bonsai Environment Model through Out-of-Scope Observations, Framework Prompts/Skills/Templates, Session Boundaries,
and File Maintenance Discipline] | [`bonsai/README.md` corresponding user-facing workflows] | [Completed Phase 2
bootstrap/router/menu artifacts and deferred obligations]  
**In Scope:** [`bonsai/prompts/create_project_memory.md`; `bonsai/skills/phase_execution.md`;
`bonsai/skills/final_truth_update.md`; `bonsai/skills/dry_run.md`; `bonsai/skills/handoff.md`;
`bonsai/skills/agent_context.md`; `bonsai/skills/bonsai_home.md`; `bonsai/templates/plan_phase_template.md`;
`bonsai/templates/icebox_template.md`; developer-context layering and Phase 3 routing completion in
`bonsai/prompts/implementation.md`; integration and focused validation with existing `bonsai/start.md`,
`bonsai/skills/menu.md`, and inline Project Management]  
**Out of Scope / Do Not Do Yet:** [Reimplementing or extracting inline Project Management into another artifact;
rewriting the running `.bonsai/` v1.4 runtime; converting active `bonsai-dev` execution-memory filenames; Phase 4
code-map artifacts or behavior; the Phase 5 general validation harness, six topology proofs, promotion, rollback,
or staging removal; helper-script packaging; a v2 `tooling.md` or `developer_context.example.md` compatibility
artifact; generated output under `bonsai/`; changes to human-owned `bonsai/specification.md`, `bonsai/README.md`,
requirements, architecture, or approved artifact contracts without the applicable final-truth gate]  
**Expected Deliverables:** [`bonsai/prompts/create_project_memory.md`; six Phase 3 workflow skills under
`bonsai/skills/`; `bonsai/templates/plan_phase_template.md`; `bonsai/templates/icebox_template.md`; completed
Phase 3 context/routing behavior in `bonsai/prompts/implementation.md`; focused conformance evidence that closes
the Phase 2 deferrals owned by Phase 3]

## Execution Constraints

* **Implementation Scope:** The staged `bonsai/` distribution and agent-owned Phase 3 execution memory only.
  Existing `bonsai/start.md`, `bonsai/prompts/implementation.md`, and `bonsai/skills/menu.md` are integration
  dependencies; modify them only where the approved Phase 3 contracts require completion or expose a concrete
  contract gap.
* **Approved Boundaries:** Keep `.bonsai/` as the running v1.4 runtime; keep `bonsai/` independently shippable and
  free of generated output; use v2 `agent_` execution-memory names in staged artifacts; keep developer context
  human-owned and limited to home/repository scopes; keep agent context agent-owned at home/repository/project
  scopes; keep project memory repository-local; keep Bonsai Home identity environment-derived; keep Web UI
  project-memory synthesis separate from coding-session project creation; preserve lazy workflow/facet loading and
  invoking-gate return semantics.
* **Public Contracts:** None established or changed. This phase implements already-approved Phase 1 artifact and
  responsibility contracts. Inline Project Management is already implemented by the Phase 2 router and menu; Phase
  3 integrates and validates it without reimplementation, correcting it only if Phase 3 exposes a gap against the
  approved `PROJECT-MANAGE-*` contract.
* **Human Review Focus:** Confirm single-pass mode, the seven-step artifact order, the non-reimplementation boundary
  for Project Management, the separation of focused Phase 3 validation from Phase 5 topology validation, and the
  prohibition on silently changing human-owned specification/guide/contracts.

## Ordered Work

### Implementation

* **Step 1 Agent and developer context:** Implement scoped operational-memory behavior and complete lazy
  developer-context layering in the implementation router. | **Status:** Completed | **Files:**
  [`bonsai/skills/agent_context.md`, `bonsai/prompts/implementation.md`] | **Done:** Home/repository/project agent
  context layers broad-to-specific at the narrowest reusable scope; home/repository developer context loads only
  for relevant facets with repository specificity winning; human/agent ownership, conflict reporting, blocker
  placement, qualification, pruning, authorization, and no-secret rules match `CORE-CONTEXT-*` and
  `PROJECT-DEVELOPER-*`; no v2 tooling-memory compatibility artifact is introduced.
* **Step 2 Phase execution and phase-plan template:** Implement the v2 phase-planning, mode-selection, plan-review,
  and contract-first workflow together with its only reusable phase-plan template. | **Status:** Completed |
  **Files:** [`bonsai/skills/phase_execution.md`, `bonsai/templates/plan_phase_template.md`] | **Done:** Mandatory
  initial planning, selective later plans, single-pass terminology, two-pass contract criteria, native Pass A
  review surfaces, approval/session gates, current-state reconciliation, v2 filenames, and no-invented-abstraction
  boundaries satisfy `CORE-PHASE-*` and `PROJECT-PHASE-TEMPLATE-*`; instantiated-plan guidance has no competing
  single/two-pass branches.
* **Step 3 Final truth and dry runs:** Implement final-truth reconciliation and optional read-only execution
  previews as separate lazy workflows. | **Status:** Completed | **Files:**
  [`bonsai/skills/final_truth_update.md`, `bonsai/skills/dry_run.md`] | **Done:** `None` / `Clarification` /
  `Revision`, affected-document handling, explicit human authorization, Bonsai-specification authority,
  invoking-gate return, dry-run read-only behavior, compact baseline lifecycle, and no routine dry-run gate satisfy
  `CORE-TRUTH-*` and `CORE-DRY-*`.
* **Step 4 Project-memory synthesis:** Implement the Web UI project-memory workflow from its approved synthesis
  contract. | **Status:** Completed | **Files:** [`bonsai/prompts/create_project_memory.md`] | **Done:** The
  prompt preserves conversational design and blocking-clarification discipline; produces a complete extractable
  zip rooted at `.bonsai/projects/main/` or an explicitly named safe project; emits v2-owned core memory and only
  warranted layered truth/context; keeps developer context and implementation out; initializes design/readiness
  honestly; and leaves detailed Phase 1 planning to implementation, satisfying `PROJECT-MEMORY-*`.
* **Step 5 Bonsai Home workflow:** Implement the bounded embedded-to-reusable-home workflow and its return to
  resolved startup identity. | **Status:** Completed | **Files:** [`bonsai/skills/bonsai_home.md`] | **Done:**
  The workflow requires configured `BONSAI_HOME`, validates source and target, creates or safely populates the
  target when authorized, preserves repository-local project memory, performs no implicit environment
  configuration, stores no home-path fallback in context, and returns through `start.md` and the invoking gate,
  satisfying `PROJECT-HOME-*`.
* **Step 6 Handoff and icebox:** Implement completion/resume reconciliation and the first-use human-owned icebox
  template together. | **Status:** Completed | **Files:** [`bonsai/skills/handoff.md`,
  `bonsai/templates/icebox_template.md`] | **Done:** Handoff reconciles current execution memory before completion,
  reports only authorized-step changes/checks, removes stale state, routes qualifying operational context, exposes
  observation count before details, preserves observations only by human choice, returns from subordinate work,
  records standalone readiness/next-step fields, and offers peer session choices; the template is instantiated only
  for the first selected observation and satisfies `CORE-HANDOFF-*` and `PROJECT-ICEBOX-TEMPLATE-*`.
* **Step 7 Integrated Phase 3 conformance:** Validate the complete Phase 3 workflow graph with the Phase 2
  bootstrap/router/menu spine and close every Phase 2 deferral owned by Phase 3. | **Status:** Completed |
  **Files:** [`bonsai/start.md`, `bonsai/prompts/implementation.md`, `bonsai/skills/menu.md`, all Phase 3
  deliverables] | **Done:** Focused reference, routing, ownership, naming, purity, and scenario checks pass. All
  Phase 2/3 standard-root-relative references resolve; the intentionally absent Phase 4 map artifacts remain
  guarded. Router corrections close active-phase-plan loading and safe confirmed Project Management creation plus
  Web UI design guidance. Explicit and contextual routing, invoking-gate return, staged v2 names, lazy loading,
  human/agent ownership, Phase 3 workflow delegation, and the approved Project Management scenarios conform.
  `bonsai/README.md` and `bonsai/specification.md` remain unchanged authorities; Phase 4 map implementation and
  Phase 5 topology/promotion validation remain unclaimed.

## Validation & Done Criteria

* **Validation Strategy:** After each step, perform focused static contract/specification/README conformance checks
  and scenario walkthroughs at the stable workflow seam. At Step 7, check cross-artifact paths, ownership and v2
  filenames, trigger/delegation closure, gate return, deferred-work guards, staged-tree purity, and all Phase 3 rows
  in the approved validation trace. Do not create the general Phase 5 harness or write generated output under
  `bonsai/`; record any scenario requiring a real fresh session, multi-topology fixture, or host-side archive/swap as
  still deferred rather than passed.
* **Architecture Validation:** Verify `.bonsai/` remains the untouched running v1.4 standard; all candidate
  artifacts remain standard-root-relative under `bonsai/`; repository project memory never moves into Bonsai Home;
  project-memory synthesis remains a Web UI artifact producer; context scopes and ownership do not blur; workflow
  responsibilities follow the approved router/skill/template seams; no extra Project Management artifact,
  configuration framework, compatibility layer, or generated distribution debris appears.
* **Definition of Done:** All nine missing Phase 3 standard artifacts exist and satisfy their approved contracts;
  the implementation router completes Phase 3 context/delegation behavior; existing inline Project Management is
  integrated and contract-validated without reimplementation; Phase 2 deferrals owned by Phase 3 are closed;
  focused checks pass; Phase 4/5 obligations remain accurately deferred; roadmap, phase plan, and state are
  reconciled for Phase 4 activation without claiming full staged-distribution validation or promotion readiness.

## Context & Wrap-up

* **Dependencies:** [Approved Phase 1 artifact contracts; completed Phase 2 `start.md`, implementation router, and
  menu; staged `bonsai/specification.md` and `bonsai/README.md`; running Bonsai 1.4 bootstrap runtime]
* **Risks:** [Duplicating Project Management or other router ownership in new skills; making the implementation
  kernel monolithic; eagerly loading context; confusing developer and agent context ownership/scopes; allowing
  Bonsai Home creation to mutate repository memory or host configuration; claiming prompt/scenario behavior proven
  without the later Phase 5 harness; leaking bootstrap v1.4 names or staging-only paths into the v2 standard]
* **Open Questions:** [None blocking plan review. If implementation exposes an approved-contract gap in inline
  Project Management or another Phase 2 artifact, correct only that gap and report it; if satisfying a contract
  requires changing the specification, README, approved artifact contracts, requirements, or architecture, stop at
  final-truth reconciliation rather than silently expanding Phase 3.]
* **Completion Summary:** **Outcome:** [All nine Phase 3 artifacts and the completed implementation-router
  integration satisfy the approved focused conformance trace; Phase 2 deferrals owned by Phase 3 are closed;
  no final-truth change or generated distribution debris was introduced] | **Unlocked:** [Phase 4 integrated code
  maps activation planning]

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
* Implementation style and test style follow project conventions, approved project memory, developer context, and
  applicable external skills.
* If required behavior conflicts with approved architecture or an approved contract, stop and require phase-plan
  correction, final-truth clarification, or final-truth revision before continuing.
* When a review gate, blocker state, phase status, or plan approval state changes, verify whether `state.md` and
  `plan.md` require corresponding updates.
* If this phase plan becomes incomplete, stale, or inconsistent with current approved project direction, correct
  it before substantive phase execution continues.
* Set `Plan Status: Approved` only after explicit human approval.
* Compress completed phase detail when it no longer helps execution, while preserving enough summary to explain
  the outcome and what it unlocked.
