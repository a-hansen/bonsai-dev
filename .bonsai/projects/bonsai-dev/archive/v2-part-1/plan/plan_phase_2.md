# AI Plan - Phase 2: Bootstrap and Core Execution Model

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**  
**Project:** Bonsai Dev | **Parent:** `../../../../../../../../Users/Aaron/Desktop/.bonsai-old/projects/bonsai-dev/plan.md`  
**Phase Status:** Completed  
**Plan Status:** Approved  
**Mode:** Single-pass

## Objective & Scope

**Objective:** Implement the Phase 2 subset of the staged Bonsai v2 bootstrap and core implementation spine so a
repository-local `start.md` can resolve session identity, hand control to a minimal implementation router, and
present consistent startup and subordinate-workflow gates. Artifacts created in this phase may retain approved
responsibilities whose working dependencies are implemented in Phase 3; those obligations remain explicitly
deferred rather than implemented, stubbed, or treated as satisfied.  
**Inputs:** [`requirements.md` REQ-1–REQ-3, REQ-5–REQ-8] | [`architecture.md` Bootstrap Repository Model,
Staging Principle, Authority Chain During Bootstrap, Core Workflow Decomposition, Phase Architecture] |
[`artifact_contracts/core_workflows.md` contracts for `start.md`, `prompts/implementation.md`, and
`skills/menu.md`] | [`bonsai/specification.md` Bonsai Environment Model, Startup Bootstrap, Projects,
Implementation Workflow, Execution Readiness, Human Gates and Menus, Framework Prompts, Framework Skills]  
**In Scope:** [`bonsai/start.md`; `bonsai/prompts/implementation.md`; `bonsai/skills/menu.md`; Bonsai Home,
repository-home, and active-project identity resolution; minimum-state implementation routing; startup readiness
and gate behavior; contextual menu and invoking-gate return semantics; focused conformance checks for these
artifacts; explicit accounting for approved contract obligations deferred to Phase 3]  
**Out of Scope / Do Not Do Yet:** [Rewriting the running `.bonsai/` v1.4 runtime; converting active project memory
to v2 filenames; full project-lifecycle and project-memory workflows; Phase 3 execution/final-truth/dry-run/handoff/
agent-context skills; integrated code maps; general validation harness and generated test output; promotion,
rollback, or staging removal; helper-script packaging; placeholder files, no-op branches, or prose claims that
represent a Phase 3-dependent responsibility as implemented]  
**Expected Deliverables:** [`bonsai/start.md`; `bonsai/prompts/implementation.md`; `bonsai/skills/menu.md`]

## Execution Constraints

* **Implementation Scope:** The staged `bonsai/` distribution and agent-owned Phase 2 execution memory only.
* **Approved Boundaries:** Keep `.bonsai/` as the running Bonsai 1.4 runtime; keep `bonsai/` independently
  shippable and free of generated output; keep bootstrap limited to identity resolution; keep the implementation
  prompt a minimum-state router; keep reusable presentation mechanics in `skills/menu.md`; preserve natural-language
  startup requests and session-local project selection; use v2 `agent_` execution-memory identities inside staged
  artifacts without creating bootstrap-period copies for `bonsai-dev`.
* **Public Contracts:** None established or changed. This phase implements the already-approved Phase 1 artifact
  contracts only to the extent supported by the Phase 2 scope. Remaining approved responsibilities stay binding
  and visibly deferred to Phase 3; partial implementation must not be described as full contract satisfaction.
  Stop if implementation would require changing a contract or `bonsai/specification.md`.
* **Human Review Focus:** Confirm the phase boundary, single-pass mode, artifact order, and deferral of broader
  Phase 3 workflows before implementation begins.

## Ordered Work

### Implementation

* **Step 1 Repository bootstrap:** Implement the small local bootstrap that resolves repository home, prefers a
  valid `BONSAI_HOME` with embedded fallback, resolves the active project deterministically and session-locally,
  preserves an appended natural-language request, and hands control to the resolved implementation prompt. |
  **Status:** Completed |
  **Files:** [`bonsai/start.md`] | **Done:** The implemented Phase 2 behavior satisfies the applicable `start.md`
  responsibilities without loading project knowledge eagerly; requests requiring Phase 3 workflows remain
  preserved and visibly deferred rather than handled by stubs or reported as working.
* **Step 2 Core menu behavior:** Implement reusable primary-menu, contextual **See more options**, host free-form,
  and subordinate-workflow return rules. | **Status:** Completed | **Files:** [`bonsai/skills/menu.md`] | **Done:** The artifact preserves
  decision ownership in invoking workflows; menu scenarios whose subordinate workflows do not exist until later
  phases remain explicit deferred validation obligations and are not reported as passing in Phase 2.
* **Step 3 Implementation router:** Implement the stable post-bootstrap kernel for minimum-state readiness
  assessment, lazy context/skill loading, startup summaries and gates, exact-next-step scope, deviations,
  agent-owned memory routing, and handoff-before-completion discipline. Limit project behavior to the identity and
  routing needed by the Phase 2 spine; broader lifecycle workflows remain deferred to Phase 3. | **Status:** Completed |
  **Files:** [`bonsai/prompts/implementation.md`] | **Done:** The artifact satisfies the Phase 2 portion of its
  approved contract, identifies later-phase workflow dependencies without providing placeholder implementations,
  and does not absorb bootstrap or menu ownership. Its remaining approved responsibilities are not represented as
  implemented or satisfied.
* **Step 4 Integrated conformance review:** Check the three staged artifacts together against their approved
  contracts, governing specification sections, README promises, staging boundary, canonical paths, lazy-loading
  rules, gates, and v2 execution-memory names. | **Status:** Completed | **Files:** [`bonsai/start.md`, `bonsai/prompts/implementation.md`,
  `bonsai/skills/menu.md`] | **Done:** Cross-references resolve within the intended final distribution, no v1.4
  control-path or duplicate bootstrap execution-memory convention leaks into the staged artifacts, no generated
  output exists under `bonsai/`, and every unimplemented approved responsibility is accounted for under either the
  later-phase dependency list below or intentionally deferred Phase 5 validation without being represented as completed.

## Deferred Approved Contract Obligations

These obligations remain approved and binding. Phase 2 may create their owning artifacts, but it does not implement,
stub, satisfy, or close obligations that require Phase 3 workflow artifacts or behavior.

* **`start.md`:** Preserve and route explicit startup requests, including Create Bonsai Home and Manage Code Maps,
  but do not claim the requested workflow works before its owning later-phase skill exists. When no project memory
  exists, surface creation or design as required without implementing project-memory synthesis.
* **`prompts/implementation.md`:** Keep approved delegation points and routing rules visible. The small inline
  List/Switch/Create Project Management behavior is implemented in Phase 2; broader project-memory/design lifecycle
  behavior and the phase-execution, final-truth, dry-run, handoff, agent-context, Bonsai-Home, and code-map
  workflows remain deferred to their owning later phases. Do not create placeholder skills or success paths for
  unavailable workflows.
* **`skills/menu.md`:** Define presentation and invoking-gate return semantics now, while deferring end-to-end
  validation involving unavailable subordinate workflows. Mentioning a contextual action is not evidence that its
  workflow has been implemented.
* **Validation:** Phase 2 validates only behavior executable from Phase 2 artifacts and performs static conformance
  review for later delegation. Scenario outcomes that require Phase 3 or the full Phase 5 operating-model harness
  remain explicitly unpassed until those phases execute them.

At Phase 2 completion, carry this still-current deferred-obligation set into Phase 3 activation state or its phase
plan and onward to each subsequent owning phase as applicable. Do not erase it merely because the owning artifact
now exists.

## Validation & Done Criteria

* **Validation Strategy:** Perform focused static conformance checks after each artifact, then an integrated
  contract/specification/README review. Exercise the approved bootstrap and gate scenarios as explicit artifact
  walkthroughs only where all required behavior exists in Phase 2. For scenarios requiring a Phase 3 workflow,
  verify only correct preservation/delegation and retain the scenario as deferred—not passed. Do not introduce the
  general Phase 5 harness or generated output merely for this phase.
* **Architecture Validation:** Verify that `.bonsai/` remains untouched as the running runtime; all new standard
  artifacts live under `bonsai/`; bootstrap, router, and menu ownership remain separated; active project selection
  is session-local; `BONSAI_HOME` resolution follows the approved precedence; and staged artifacts use v2 names.
* **Definition of Done:** All three deliverables exist in the staged distribution; each satisfies the explicitly
  identified Phase 2 subset of its approved contract; integrated paths and delegations are coherent; focused
  Phase 2 checks pass; no placeholder implementation stands in for a deferred responsibility; every remaining
  approved obligation and validation scenario is visibly carried into Phase 3 or Phase 5 as applicable; roadmap,
  phase plan, and state are reconciled for Phase 3 activation without claiming full artifact-contract completion.

## Context & Wrap-up

* **Dependencies:** [Approved complete Phase 1 artifact-contract layer; `bonsai/specification.md`;
  `bonsai/README.md`; temporary Bonsai 1.4 bootstrap runtime]
* **Risks:** [Duplicating bootstrap logic in the implementation router; eagerly loading context; letting menu
  presentation own authorization; accidentally specifying Phase 3 behavior incompletely; using v1.4 paths in the
  staged v2 artifacts; treating walkthrough validation as the later full operating-model validation]
* **Open Questions:** [None blocking plan review. If an artifact cannot satisfy its approved contract without
  pulling a broader Phase 3 workflow into scope, stop for phase-plan correction rather than inventing a stub or
  silently broadening the phase.]
* **Completion Summary:** **Outcome:** [`bonsai/start.md`, `bonsai/skills/menu.md`, and
  `bonsai/prompts/implementation.md` implement the approved Phase 2 bootstrap and core execution spine; focused
  and integrated static checks passed; missing later workflow skills are explicitly guarded and remain unvalidated;
  no v1.4 control path, duplicate execution-memory convention, placeholder implementation, generated output, or
  staging-only path leaked into the candidate artifacts] | **Unlocked:** [Phase 3 context and project workflows]

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
* When a review gate, blocker state, phase status, or plan approval state changes, verify whether `state.md` and
  `plan.md` require corresponding updates.
* If this phase plan becomes incomplete, stale, or inconsistent with current approved project direction,
  correct it before substantive phase execution continues.
* Set `Plan Status: Approved` only after explicit human approval.
* Compress completed phase detail when it no longer helps execution, while preserving enough summary
  to explain the outcome and what it unlocked.
