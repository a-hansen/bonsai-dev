# AI Plan - Phase 4: Integrated Code Maps

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**  
**Project:** Bonsai Dev | **Parent:** `../../../../../../../../Users/Aaron/Desktop/.bonsai-old/projects/bonsai-dev/plan.md`  
**Phase Status:** Completed  
**Plan Status:** Approved  
**Mode:** Single-pass

## Objective & Scope

**Objective:** Implement the approved integrated code-map workflow and canonical mapping artifacts in the staged
Bonsai v2 distribution while preserving mature v1.4 navigation behavior, adopting v2 map-store/source identity,
context, and menu semantics, exercising one explicitly supplied released-source archive, and leaving automatic
source discovery and full operating-model topology validation to Phase 5 or later work.  
**Inputs:** [`requirements.md` REQ-2–REQ-8, REQ-10, REQ-16] | [`architecture.md` Distribution Purity,
Authority Chain During Bootstrap, Artifact Contract Layer, Mapping Architecture] |
[`artifact_contracts/code_maps.md`] | [`bonsai/specification.md` Mapping is part of Bonsai, Agent Context, Human
Gates and Menus, Code Maps, Integrated Mapping Workflow, Manage Code Maps, Multi-Repository Source Universes,
File Maintenance Discipline, and Bonsai 2.0 Validation Cases] | [`bonsai/README.md` Agent Context and Code Maps] |
[Completed Phase 2–3 startup, router, menu, agent-context, and handoff artifacts] | [v1.4 mapping artifacts as
implementation evidence only]  
**In Scope:** [`bonsai/prompts/create_map_repo.md`; `bonsai/skills/code_maps.md`; the eight canonical map templates
under `bonsai/templates/`; bounded integration corrections in `bonsai/start.md`, `bonsai/prompts/implementation.md`,
`bonsai/skills/menu.md`, `bonsai/skills/agent_context.md`, and `bonsai/skills/handoff.md` only where required by
the approved mapping contract; focused static and scenario conformance checks; a bounded released-source archive
scenario that reads the human-supplied `$BONSAI_HOME/maps/aon/aon-6.1.1-sources.jar` in place and writes only the
resulting reusable `aon` map to the active named map store, while permitting transient read-only inspection outside
the durable map store]  
**Out of Scope / Do Not Do Yet:** [Rewriting the running `.bonsai/` v1.4 runtime; converting active `bonsai-dev`
execution-memory filenames; changing `bonsai/specification.md`, `bonsai/README.md`, requirements, architecture, or
approved artifact contracts without the applicable final-truth gate; creating compatibility identities for
`repo_prompt.md`, `map_repo_template.md`, or `templates/symbol_index.tsv`; inventing a universal source-identity
schema, map registry, dependency resolver, helper script, or continuous drift checker; writing runtime map data or
generated output into `bonsai/`; inferring a source downloader, automatic source/dependency resolver, registry, or
universal source-location convention from the supplied archive scenario; the Phase 5 general validation harness,
complete six-topology proof, promotion, rollback, fresh-session self-hosting proof, or staging removal]  
**Expected Deliverables:** [`bonsai/prompts/create_map_repo.md`; `bonsai/skills/code_maps.md`;
`bonsai/templates/code_map_template.md`; `bonsai/templates/map_state_template.md`;
`bonsai/templates/subsystem_map_template.md`; `bonsai/templates/api_pub_template.md`;
`bonsai/templates/api_ext_template.md`; `bonsai/templates/namespace_router_template.tsv`;
`bonsai/templates/manifest_template.tsv`; `bonsai/templates/symbol_index_template.tsv`; any strictly necessary
bounded integration corrections; focused conformance evidence including the supplied released-source archive
scenario; a reusable runtime map identified as `aon` in the active named map store; an explicit Phase 5 deferral
record]

## Execution Constraints

* **Implementation Scope:** The staged `bonsai/` distribution and agent-owned Phase 4 execution memory, plus the
  bounded validation read of the explicitly supplied archive and write of the reusable `aon` map to the active map
  store. Inspect every applicable v1.4 mapping artifact before adapting it, but treat the approved v2 specification
  and artifact contract as authority. Modify completed Phase 2–3 artifacts only for concrete approved integration
  gaps. Bonsai may inspect the archive directly or use transient extraction outside the durable map store. It must
  not move, rename, modify, or treat the archive or transient extraction as durable map data.
* **Approved Boundaries:** Keep `.bonsai/` as the running v1.4 runtime; keep `bonsai/` independently shippable and
  free of runtime/generated map data; resolve the active map store independently from mapped source context; name
  maps for source universes rather than projects; keep actual source authoritative; keep `map_repo.md` human-owned
  and optional; keep mapping state agent-owned, concise, and lazy; preserve contextual entry, explicit mutation and
  destructive gates, scoped agent-context delegation, and return to the refreshed invoking gate.
  The archive's supplied location under `$BONSAI_HOME/maps/aon/` is a scenario precondition only: source input,
  source identity, map identity, and map output location remain separate concepts, and this colocation establishes
  no general Bonsai source-location convention. The archive is not owned by the `aon` map lifecycle; create,
  update/rebuild, and remove operations may mutate or remove only the map-owned artifacts they actually own and
  must preserve the archive and all other colocated non-map-owned files.
* **Public Contracts:** No new contract is established. The approved Phase 1 mapping contract now explicitly states
  its existing artifact-specific lifecycle ownership boundary: map operations preserve colocated non-map-owned source
  inputs, and transient inspection is not durable map data. The deliberately minimal source-identity representation
  may be chosen from evidence during implementation, but must not become a new universal registry/schema or
  materially revise the approved contract.
* **Human Review Focus:** Confirm single-pass mode, the six-step implementation order, the canonical artifact set,
  bounded edits to completed integration artifacts, the supplied archive scenario and its non-generalization
  boundary, and the boundary between focused Phase 4 conformance and full Phase 5 topology validation.

## Ordered Work

### Implementation

* **Step 1 Reconcile implementation evidence:** Inspect all applicable v1.4 mapping prompts, procedures, guide,
  and templates plus the existing staged startup/router/menu/context seams before modifying their v2 successors. |
  **Status:** Completed | **Files:** [`.bonsai/maps/repo_session.md`, `.bonsai/maps/map_prompt.md`,
  `.bonsai/maps/map_system.md`, `.bonsai/maps/README.md`, `.bonsai/maps/templates/*`, relevant staged integration
  artifacts] | **Done:** Each planned v2 artifact is tied back to its approved Keep/Adapt/Drop/Missing decisions;
  useful source behavior is understood, stale identities remain dropped, and no contract or final-truth conflict is
  unresolved.

  **Reconciled implementation basis:**
  - `prompts/create_map_repo.md` adapts `repo_session.md` under `MAP-CAL-*`, preserving its conversational
    fact/weight/uncertainty and scope discipline plus its complete inline output shape; `repo_prompt.md` and a
    separate `map_repo_template.md` remain dropped.
  - The eight canonical templates preserve the contracted layered map roles under `MAP-DATA-*` and `MAP-FLOW-08`;
    `code_map.md` gains minimal source identity and source-authority guidance, `map_state.md` loses standalone
    session/AI-product assumptions, optional Markdown/TSV layers remain selective, and the symbol-index template
    has only the corrected `symbol_index_template.tsv` identity.
  - `skills/code_maps.md` owns the adapted `map_prompt.md` gate/state behavior, durable `map_system.md` editing
    rules, and the Missing `MAP-V2-*` lifecycle/store/source/alignment/context/gate-return behavior. The standalone
    v1.4 mapping bootstrap and control-document identities remain dropped.
  - Existing staged seams already preserve explicit startup requests, lazy workflow delegation, contextual menu
    presentation, scoped source/map operational context, and generic subordinate gate return. Their expected open
    integration seam is the not-yet-created `skills/code_maps.md`; Step 5 will change completed Phase 2-3 artifacts
    only if implementing Steps 2-4 exposes a concrete contract gap.
  - No approved contract, specification, README, requirements, or architecture conflict was found.
* **Step 2 Repository calibration prompt:** Implement the optional Web UI calibration workflow with its complete
  inline output shape. | **Status:** Completed | **Files:** [`bonsai/prompts/create_map_repo.md`] | **Done:** The
  prompt distinguishes observed facts, owner weighting, hypotheses, uncertainty, and scope; synthesizes one complete
  `map_repo.md` only on explicit request; requires neither project memory nor a separate template; and never writes
  to the source or map store automatically.
* **Step 3 Canonical map templates:** Adapt the eight approved templates into the staged distribution, including
  the corrected single symbol-index template identity. | **Status:** Completed | **Files:**
  [`bonsai/templates/code_map_template.md`, `bonsai/templates/map_state_template.md`,
  `bonsai/templates/subsystem_map_template.md`, `bonsai/templates/api_pub_template.md`,
  `bonsai/templates/api_ext_template.md`, `bonsai/templates/namespace_router_template.tsv`,
  `bonsai/templates/manifest_template.tsv`, `bonsai/templates/symbol_index_template.tsv`] | **Done:** Every
  template expresses only its contracted layer, preserves evidence/compression/relative-routing rules, keeps
  optional outputs optional, uses literal-tab fixed-column TSV where applicable, and exposes no stale v1 identity
  or project/session state.
* **Step 4 Integrated code-map skill:** Implement the lazy lifecycle workflow for Create, Inspect, Update/Rebuild,
  Remove, and Inspect Map/Source Identity. | **Status:** Completed | **Files:** [`bonsai/skills/code_maps.md`] |
  **Done:** The skill resolves store/source/project identity separately; gates action, scope, ambiguity, mismatch,
  optional high-cost output, and destructive work; uses source and calibration with correct authority; preserves
  layered selective mapping, source alignment, strict TSV, concise state, contextual first-use/maintenance
  restraint, agent-context routing, and invoking-gate return; and does not invent automatic resolution machinery.
  Lifecycle operations identify their exact owned targets and never equate ownership with every file beneath the
  named map directory; update/rebuild and especially Remove preserve colocated supplied source artifacts.
* **Step 5 Core workflow integration:** Close only approved mapping gaps in the existing startup, implementation,
  menu, context, and handoff graph. | **Status:** Completed | **Files:** [`bonsai/start.md`,
  `bonsai/prompts/implementation.md`, `bonsai/skills/menu.md`, `bonsai/skills/agent_context.md`,
  `bonsai/skills/handoff.md`, `bonsai/skills/code_maps.md`] | **Done:** Explicit startup requests, contextual
  first use, **Manage Code Maps**, map-guided implementation facets, durable source/map operational context, and
  completion/cancellation all route lazily to the skill and back to the refreshed invoking gate without duplicating
  ownership or making mapping routine startup context.
* **Step 6 Focused Phase 4 conformance:** Validate the complete mapping artifact graph and record the remaining
  Phase 5 obligations without claiming the full operating-model proof. | **Status:** Completed | **Files:** [All
  Phase 4 deliverables and modified integration dependencies] | **Done:** Standard references resolve; only the
  canonical artifact identities exist; the staged tree contains no runtime/generated map data; Markdown/TSV
  structures conform; contract walkthroughs cover lifecycle gates, calibration, source authority, store/source
  separation, alignment mismatch, optionality, layered loading, contextual restraint, agent-context delegation,
  and gate return; the supplied released-source archive scenario below produces the reusable `aon` map without
  project memory or Git metadata; automatic discovery and real multi-topology/fresh-session cases remain explicitly
  deferred to Phase 5 or later work.

## Validation & Done Criteria

### Focused Supplied Released-Source Archive Scenario

* **Precondition:** The human supplies `$BONSAI_HOME/maps/aon/aon-6.1.1-sources.jar`. Treat that exact file as the
  explicit source input. It is not generated map data, and its placement beside map-store content is not a Bonsai
  convention or an input-discovery rule.
* **Inspection:** Select the supplied archive directly, without requiring a Bonsai project, project memory, a Git
  worktree, Git metadata, dependency metadata, source download, or a copy into any project. Treat the archive as
  the authoritative supplied source artifact and the actual source it contains as authoritative evidence. Bonsai
  may inspect it directly or use transient extraction or another read-only inspection area outside the durable map
  store when useful. Any transient extraction is disposable inspection state, not durable map data.
* **Walkthrough:** Use the explicitly supplied map identity `aon`, create the reusable map under
  `$BONSAI_HOME/maps/aon/`, record enough archive/source identity in `code_map.md` to keep the input distinguishable
  from the `aon` map identity, and leave the supplied archive at its original path. For Create, Update/Rebuild, and
  Remove Code Map, resolve the exact map-owned target set before mutation and verify that the archive is excluded.
  Update/rebuild and especially actual removal remain subject to their explicit human gates. If removal is
  authorized and exercised, remove only map-owned artifacts, verify the archive remains unchanged, and recreate the
  reusable map before Phase 4 completion.
* **Pass Conditions:** The map is identified as `aon` and written only to the resolved active named map store; its
  claims trace to source inside the supplied archive; no project memory is created; no source is copied into a
  project; archive location, source identity, map identity, and output location are not conflated despite this
  scenario's physical colocation; direct or transient inspection does not move, rename, or modify the archive; no
  transient extraction becomes durable map data; every lifecycle operation preserves the archive and any other
  colocated non-map-owned file; Remove cannot delete the named map directory wholesale merely because map artifacts
  live there; and no automatic dependency resolver, source downloader, registry, or universal source-location
  convention is introduced or implied.
* **Deferred:** Automatic dependency/source discovery and the complete multi-topology proof remain Phase 5 or later
  work.

* **Validation Strategy:** Perform focused artifact and cross-reference checks after each implementation step.
  Validate template structure, canonical names, literal-tab TSV headers/column counts, absence of stale identities,
  staged-tree purity, trigger/delegation closure, lifecycle authorization, identity mismatch handling, lazy loading,
  state ownership, and invoking-gate return through contract-based scenario walkthroughs. Do not create or claim the
  Phase 5 general harness. Execute the bounded supplied-archive walkthrough above when its precondition is present;
  classify automatic discovery, remaining isolated topology fixtures, and fresh-host-session cases as deferred.
* **Architecture Validation:** Verify the staged distribution contains only standard artifacts; runtime map data
  is always described under the active Bonsai Home or Embedded map store; source inspection context never implies
  output placement; map identity never follows a consuming project by default; project truth and `map_repo.md`
  remain calibration rather than source evidence; optional layers stay optional; mature map structures are adapted
  rather than redesigned without need; the supplied archive remains source input rather than map data or a location
  convention; transient inspection remains outside durable map storage; map lifecycle ownership is artifact-specific
  rather than directory-wide; the resulting `aon` runtime map remains outside the staged distribution; and completed
  core workflow ownership remains intact.
* **Definition of Done:** All ten new Phase 4 standard artifacts exist and satisfy their approved contracts; all
  required integration routes are coherent and no broader completed artifact was rewritten unnecessarily; focused
  conformance checks pass; stale identities and distribution debris are absent; unresolved minimal identity details
  remain bounded and evidence-driven; the supplied archive scenario passes and leaves a reusable `aon` map in the
  active named map store without project/Git requirements or invented discovery machinery; the original archive is
  unchanged after all exercised lifecycle operations and is never treated as map-owned; transient inspection leaves
  no durable map data; Phase 5 topology/promotion obligations are accurately preserved; roadmap, phase plan, and
  state are reconciled for Phase 5 activation without claiming promotion readiness.

### Step 6 Conformance Record

* **Standard artifact graph:** All executable standard references resolve; the calibration prompt, integrated
  lifecycle skill, and eight canonical templates exist under their sole approved identities. Stale
  `repo_prompt.md`, `map_repo_template.md`, and `templates/symbol_index.tsv` identities are absent.
* **Structure and workflow:** Canonical literal-tab TSV headers and fixed column counts pass. Static contract
  walkthroughs pass for calibration, lifecycle and destructive gates, source authority, store/source/project
  separation, mismatch handling, optional and layered loading, contextual restraint, agent-context delegation,
  artifact-specific ownership, and refreshed invoking-gate return.
* **Staged-tree purity:** No runtime `code_map.md`, mapping state, calibration, or lookup output exists under
  `bonsai/` after validation.
* **Released-source scenario:** Direct read-only inspection of
  `$BONSAI_HOME/maps/aon/aon-6.1.1-sources.jar` produced the reusable named `aon` map in the active Bonsai Home
  store. `code_map.md` records filename version `6.1.1` and SHA-256
  `16e4bfecd37b487b589261f287118d75f1151b678de004e1136ac0ef143e622f`; two source-backed subsystem maps cover
  the data model and codec pipeline. No project memory, Git metadata, copied source, retained extraction, active
  map state, API map, or lookup index was created.
* **Lifecycle ownership:** The exact map-owned set resolves to `code_map.md`,
  `subsystems/data-model/map.md`, and `subsystems/codec-pipeline/map.md`. Read-only update/rebuild/remove target
  walkthroughs exclude the supplied archive. Destructive rebuild and removal were not exercised because they were
  neither required nor separately authorized. The archive checksum remained unchanged, and the temporary candidate
  used for validation was removed after readback verification.
* **Phase 5 obligations:** Full workflow validation remains required for the six specified operating topologies,
  including shared/Embedded store behavior, external-source behavior, multi-repository reuse and selection,
  greenfield restraint, and any automatic source/map discovery claimed by the specification. Phase 5 must also
  validate artifact-producing workflows and a complete promotion candidate, preservation and execution-memory
  conversion, rollback archive creation, the safest host-supported promotion swap, promoted-result verification,
  fresh-session self-hosting, and final staging removal. Phase 4 claims none of those proofs.

## Context & Wrap-up

* **Dependencies:** [Approved Phase 1 code-map contract; completed Phase 2–3 startup/router/menu/context/handoff
  spine; staged `bonsai/specification.md` and `bonsai/README.md`; v1.4 mapping artifacts as implementation evidence;
  running Bonsai 1.4 bootstrap runtime; human-supplied
  `$BONSAI_HOME/maps/aon/aon-6.1.1-sources.jar` before the focused archive walkthrough]
* **Risks:** [Accidentally porting the standalone v1 control plane; treating project identity as source identity;
  writing reusable map output beside external source rather than to the active store; over-specifying snapshot
  metadata or dependency resolution before topology validation; creating optional map layers by default; silently
  mutating human-owned calibration; treating the supplied archive's test placement as map data or a source-location
  convention; deriving `aon` identity silently rather than recording the explicit selection and source evidence;
  deleting the named map directory wholesale and thereby deleting unowned colocated source; retaining transient
  extraction as durable map data; bloating the implementation router; claiming one archive walkthrough proves Phase
  5 cases]
* **Open Questions:** [No blocker to plan approval. The exact smallest useful `code_map.md` source-identity fields
  remain evidence-driven within the approved contract; stop for clarification or revision if implementation shows
  that a universal schema or resolver is required rather than inventing one.]
* **Completion Summary:** **Outcome:** [Phase 4 complete; all ten mapping artifacts and bounded integration routes
  pass focused conformance, and the supplied released-source scenario leaves a validated reusable `aon` map outside
  the staged distribution while preserving its source archive] | **Unlocked:** [Phase 5 execution-mode assessment
  and detailed validation/promotion planning]

## Maintenance Rules

* Treat this file as the authoritative detailed execution plan for this phase.
* Keep `plan.md` at roadmap level. Do not duplicate phase-level sequencing there.
* Keep `state.md` aligned with this file for phase-plan approval state, current pass, exact next step, review-gate
  status, blockers, and phase completion state.
* Preserve approved project architecture and contracts during execution.
* Do not introduce interfaces, abstraction layers, adapters, builders, dependency constraints, registries,
  schemas, resolvers, or helper scripts merely to satisfy Bonsai workflow.
* Implementation and validation style follow project conventions, approved project memory, developer context, and
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
