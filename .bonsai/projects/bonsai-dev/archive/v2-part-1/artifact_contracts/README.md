# Bonsai v2 Artifact Contracts

**Project:** `bonsai-dev`  
**Ownership:** Human-owned project design  
**Purpose:** Durable behavioral contracts for the Bonsai standard artifacts and self-hosting transition
**Status:** Approved complete Phase 1 contract layer; implementation authority for later phases

## Bootstrap Context

These contracts are being extracted while Bonsai 1.4 is the active runtime.

The running v1.4 standard under `.bonsai/` is archaeological evidence and temporary execution machinery.

During this bootstrap refactor, the candidate v2 standard is staged under:

```text
repo/bonsai/
```

The staged tree is temporary. After successful promotion and fresh-session proof, it is removed and
`repo/.bonsai/` again becomes the single shipped/self-hosting Bonsai tree.

## Artifact Identity and Placement

Durable standard-artifact identities in this contract layer are relative to the Bonsai standard root. For
example:

```text
specification.md
README.md
prompts/implementation.md
skills/menu.md
```

Placement is a separate concern:

- during this Bonsai 1.4 bootstrap refactor, candidate standard artifacts are staged at
  `repo/bonsai/<artifact-identity>`;
- at runtime, shared standard artifacts live at `<bonsai-home>/<artifact-identity>`;
- in Embedded Bonsai, the standard root is `repo/.bonsai/`;
- `start.md` is the repository-local bootstrap at `repo/.bonsai/start.md`, even when the remaining shared standard
  resolves from a separate Bonsai Home.

Concrete `.bonsai/...` paths remain in archaeological-source citations and repository-memory contracts because
those references identify real v1.4 or repository-local files. Promotion contracts use `repo/bonsai/` and
`repo/.bonsai/` explicitly because staging and live placement are the behavior being contracted.

## Why This Layer Exists

The existing Bonsai implementation contains accumulated workflow knowledge that is more detailed than the new v2 specification.

The contracts prevent that knowledge from being lost while also preventing old implementation structure from becoming accidental authority.

```text
existing implementation
    ↓
learned behavior
    ↓
Keep / Adapt / Drop / Missing
    ↓
artifact contract
    ↓
v2 staged implementation
    ↓
validation
    ↓
promotion
```

## Contract Schema

Each implemented standard artifact should eventually have a contract covering:

| Field | Purpose |
| --- | --- |
| Artifact | Exact standard-root-relative artifact identity |
| Role | Why the artifact exists |
| Loaded when | Bootstrap / workflow / facet trigger |
| Inputs | Context/state assumed available |
| Responsibilities | Behavior the artifact must provide |
| Must not | Important boundaries and prohibited behavior |
| Reads | Durable artifacts it may consume |
| Writes | Durable artifacts it may maintain |
| Delegates to | Prompts/skills/workflows it invokes |
| Human gates | Approval boundaries it owns |
| Preserve from existing version | Learned behavior that should survive |
| v2 changes | Behavior intentionally changed for v2 |
| Validation cases | How the implementation will be tested |

If v2 requires behavior but Phase 1 has not established the correct artifact seam, record it as an unresolved responsibility rather than inventing a permanent file merely to complete the table.

## Classification Meanings

- **Keep:** behavior remains correct with little conceptual change.
- **Adapt:** behavior is valuable, but v2 changes its surrounding model, path, ownership, trigger, or integration.
- **Drop:** behavior belongs to a deliberately removed v1 assumption.
- **Missing:** v2 requires behavior not represented adequately in the old standard.

## Contract Groups

```text
core_workflows.md
    startup, implementation routing, menus, phase execution,
    final truth, dry runs, handoff, operational agent memory

project_workflows.md
    project-memory synthesis, project lifecycle, Bonsai Home,
    templates and context/project workflow seams

code_maps.md
    mapping calibration, mapping workflow, map data structures,
    evidence discipline, navigation, maintenance, source identity

promotion_validation.md
    test artifact boundaries, staged-distribution purity,
    rollback archive, candidate construction, promotion,
    execution-memory conversion, fresh-session self-hosting proof
```

These groups are for review convenience, not runtime modules.

## Human-Owned Standard Artifact Contracts

The two human-owned standard artifacts are already present in the staged distribution. They remain part of the
contract inventory even though Phase 1 does not rewrite them.

### Artifact: `../../../../../specification.md`

**Classification:** Missing as a v1.4 framework-authoring authority; approved v2 final truth

**Role:** Define the authoritative Bonsai operating model that every prompt, skill, template, guide, helper, and
workflow behavior implements.

**Loaded when:** Framework design or revision is being considered, a standard artifact is being created or checked,
or Bonsai behavior requires final-truth reconciliation. It is not routine implementation-session context.

**Inputs:** Human-approved Bonsai product, ownership, environment, workflow, context, mapping, maintenance, and
validation decisions.

**Responsibilities:** State durable framework behavior and boundaries; distinguish authority from implementation;
identify deliberately unresolved design mechanisms; provide the basis for standard-artifact and README
conformance.

**Must not:** Become routine startup context, defer authority to a prompt/skill/template, encode transient execution
state, or change durable Bonsai meaning without explicit human approval.

**Reads:** No other standard artifact as a peer authority. Approved self-hosting final truth may inform an explicitly
authorized specification update.

**Writes:** None during normal Bonsai workflows. Approved human changes update `../../../../../specification.md` itself.

**Delegates to:** Prompts, skills, templates, and optional helpers for procedural implementation.

**Human gates:** Any clarification or revision of durable Bonsai behavior requires explicit human review and
authorization.

**Preserve from existing version:** Preserve valuable v1.4 behavior only after archaeology and reconciliation;
v1.4 files themselves are not authority.

**v2 changes:** Introduce one explicit framework-authoring truth for the environment, identity, ownership, lazy
loading, project, mapping, menu, and execution models.

**Validation cases:** Every candidate standard artifact and user-facing promise conforms to the specification;
deliberately unresolved mechanisms remain bounded; routine implementation startup does not load the specification
without a relevant trigger.

### Artifact: `README.md`

**Classification:** Adapt useful human guidance from `.bonsai/README.md` to the v2 operating model

**Role:** Explain how a human enables, starts, designs, implements, maps, and resumes Bonsai work without becoming a
second source of framework truth.

**Loaded when:** A human needs setup or workflow guidance, or standard implementation/validation checks user-facing
promises. It is not a mandatory implementation-startup read.

**Inputs:** `../../../../../specification.md` plus the canonical identities and externally visible behavior of approved standard
artifact contracts.

**Responsibilities:** Present the canonical startup pointer; explain Embedded and Bonsai Home topologies, projects,
ownership/context, project-memory creation, gates/readiness, maps, sessions, and optional helpers; keep examples
consistent with actual contracted workflows.

**Must not:** Override the specification, promise behavior without an owning contract, reintroduce obsolete v1.4
entry points or identities, require optional helpers, or become routine agent context.

**Reads:** `../../../../../specification.md` and the approved artifact-contract layer when being maintained or validated.

**Writes:** None during normal workflows. Human-reviewed guide updates modify `README.md` itself.

**Delegates to:** The canonical `start.md`, project-memory prompt, map-calibration prompt, and named menu workflows
described by the guide.

**Human gates:** A guide change that alters durable Bonsai meaning must first reconcile with and, when necessary,
revise `../../../../../specification.md`; ordinary wording corrections remain human-reviewed standard maintenance.

**Preserve from existing version:** Preserve practical setup, project-memory, implementation, and mapping guidance
that remains useful after v2 identity and workflow changes.

**v2 changes:** Replace the v1.4 direct implementation/mapping entry model and repository-only assumptions with
`start.md`, Bonsai Home/Embedded identity, contextual menus, layered context, named-source maps, and v2 execution
memory.

**Validation cases:** All referenced standard identities resolve; examples match the contract layer; no stale v1.4
entry/name survives; the guide conforms to the specification and remains unnecessary for routine startup.

## Archaeological Evidence Method

Phase 1 records material behavior in the owning contract group. A behavior is material when losing or changing
it could alter a workflow outcome, ownership boundary, load trigger, human gate, durable write, protected edge
case, or later validation result.

Each evidence record contains:

| Field | Required content |
| --- | --- |
| Evidence ID | Stable batch-local identifier, such as `CORE-IMPLEMENTATION-01` |
| Source evidence | Exact v1.4 artifact and heading or line range, plus a concise statement of the protected behavior; `None` for genuinely missing behavior |
| Specification rule | Applicable active Bonsai `../../../../../specification.md` section and the authoritative v2 rule |
| Classification | One of `Keep`, `Adapt`, `Drop`, or `Missing`; split a mixed source into separate records when its behaviors classify differently |
| Rationale | Why the classification follows from the evidence and specification; every `Drop` requires an explicit specification-based reason |
| Owning contract | Exact contract-group file and artifact/responsibility heading that owns the v2 behavior |
| Validation obligation | Observable scenario, artifact assertion, or gate/state result that later proves the behavior |

Evidence rules:

- Read an existing artifact before closing classifications derived from it.
- Treat source text as archaeological evidence, never as authority over the specification.
- Consolidate repeated rules from several artifacts into one behavioral record with all relevant sources.
- Do not classify wording, formatting, or historical explanation unless it protects material behavior.
- Record `Missing` only when the specification requires behavior that has no adequate v1.4 source.
- Keep unresolved ownership or packaging explicit; do not invent a permanent artifact to close the inventory.
- A source artifact is accounted for only when all material behavior has been classified or deliberately excluded
  as non-behavioral/obsolete with rationale.
- A target artifact is contract-ready only when every contract-schema field and its validation obligations are
  complete. Inventory routing alone does not make a seed contract implementation authority.

## Closed v1.4 Standard Inventory

The current running distribution contains 23 standard artifacts. Every one is routed below to a primary Phase 1
batch. Cross-batch evidence may be cited where behavior is distributed, but the primary batch owns closure.

### Batch 2 — Core execution (6 artifacts)

| Existing artifact | v2 destination or responsibility | Closed classification / evidence | Owning contract |
| --- | --- | --- | --- |
| `.bonsai/implementation_prompt.md` | `prompts/implementation.md`; bootstrap behavior moves to `start.md`, menu behavior to `skills/menu.md` | Adapt + deliberate Drops; closed in `CORE-START-*`, `CORE-IMPL-*`, `CORE-MENU-*`, `CORE-TRUTH-01`, and handoff records | `core_workflows.md` |
| `.bonsai/skills/phase_execution.md` | `skills/phase_execution.md` | Keep + Adapt; closed in `CORE-PHASE-01`–`08` | `core_workflows.md` |
| `.bonsai/skills/final_truth_update.md` | `skills/final_truth_update.md` | Keep + Adapt; closed in `CORE-TRUTH-01`–`04` | `core_workflows.md` |
| `.bonsai/skills/dry_run.md` | `skills/dry_run.md` | Keep + Adapt; closed in `CORE-DRY-01`–`04` | `core_workflows.md` |
| `.bonsai/skills/handoff.md` | `skills/handoff.md` | Keep + Adapt; closed in `CORE-HANDOFF-01`–`06` | `core_workflows.md` |
| `.bonsai/skills/tooling_memory.md` | broader `skills/agent_context.md` | Keep + Adapt + deliberate Drop; closed in `CORE-CONTEXT-01`–`06` | `core_workflows.md` |

Primary specification evidence: **Startup Bootstrap**, **Implementation Workflow**, **Execution Readiness**,
**Human Gates and Menus**, **Contract-First Two-Pass Execution**, **Dry Runs**, **Out-of-Scope Observations and
`icebox.md`**, **Framework Prompts**, **Framework Skills**, **Session Boundaries**, and **File Maintenance Discipline**.

### Batch 3 — Project, context, and templates (5 artifacts)

| Existing artifact | v2 destination or responsibility | Closed classification / evidence | Owning contract |
| --- | --- | --- | --- |
| `.bonsai/README.md` | archaeological user-guide evidence; reconcile standard `README.md` across contracts in Step 6 | Project/context behavior Keep + Adapt + deliberate Drops; closed in `PROJECT-*`; remaining mapping/cross-guide evidence stays routed to Steps 4 and 6 | `project_workflows.md` primary; all groups may cite distributed behavior |
| `.bonsai/design_session.md` | `prompts/create_project_memory.md` | Keep + Adapt; closed in `PROJECT-MEMORY-01`–`14` | `project_workflows.md` |
| `.bonsai/developer_context.example.md` | guidance moves to `README.md` and lazy router/context contracts; no v2 example artifact | Keep + Adapt + deliberate Drop; closed in `PROJECT-DEVELOPER-01`–`06` | `project_workflows.md` |
| `.bonsai/templates/plan_phase_template.md` | `templates/plan_phase_template.md` | Keep + Adapt; closed in `PROJECT-PHASE-TEMPLATE-01`–`04` | `project_workflows.md` |
| `.bonsai/templates/icebox_template.md` | `templates/icebox_template.md` | Keep + Adapt; closed in `PROJECT-ICEBOX-TEMPLATE-01`–`04` | `project_workflows.md` |

Primary specification evidence: **Bonsai Environment Model**, **Projects**, **Artifact Ownership**, **Project Final
Truth**, **Agent Execution Memory**, **Developer Context**, **Agent Context**, **Context Layering**, **Lazy Loading**,
**Project-Memory Creation Workflow**, **Framework Templates**, and **Enabling Bonsai in a New Repository**.

### Batch 4 — Integrated code maps (12 artifacts)

| Existing artifact | v2 destination or responsibility | Closed classification / evidence | Owning contract |
| --- | --- | --- | --- |
| `.bonsai/maps/repo_session.md` | `prompts/create_map_repo.md`; no separate `map_repo` template | Adapt + deliberate stale-name/template Drops; `MAP-CAL-*`, `MAP-DEFECT-01`–`02` | `code_maps.md` |
| `.bonsai/maps/map_prompt.md` | integrated `skills/code_maps.md` control behavior; standalone entry dropped | Adapt + deliberate Drop; `MAP-CONTROL-*` | `code_maps.md` |
| `.bonsai/maps/map_system.md` | integrated lifecycle plus retained data/template rules; no v2 `map_system.md` | Keep + Adapt + deliberate Drops; `MAP-DATA-*`, `MAP-FLOW-*`, `MAP-DEFECT-*` | `code_maps.md` |
| `.bonsai/maps/README.md` | integrated root `README.md` guidance; standalone map guide dropped | Adapt + deliberate Drop; `MAP-FLOW-*`, `MAP-GUIDE-01` | `code_maps.md` |
| `.bonsai/maps/templates/code_map_template.md` | `templates/code_map_template.md` → map `code_map.md` | Keep + Adapt; `MAP-DATA-01`–`02`, `MAP-FLOW-08` | `code_maps.md` |
| `.bonsai/maps/templates/namespace_router_template.tsv` | `templates/namespace_router_template.tsv` → optional `namespace_router.tsv` | Keep; `MAP-DATA-03`, `MAP-DATA-11`, `MAP-FLOW-08` | `code_maps.md` |
| `.bonsai/maps/templates/subsystem_map_template.md` | `templates/subsystem_map_template.md` → subsystem `map.md` | Keep; `MAP-DATA-04`, `MAP-FLOW-08` | `code_maps.md` |
| `.bonsai/maps/templates/api_pub_template.md` | `templates/api_pub_template.md` → optional `api_pub.md` | Keep; `MAP-DATA-05`, `MAP-FLOW-08` | `code_maps.md` |
| `.bonsai/maps/templates/api_ext_template.md` | `templates/api_ext_template.md` → optional `api_ext.md` | Keep; `MAP-DATA-05`, `MAP-FLOW-08` | `code_maps.md` |
| `.bonsai/maps/templates/manifest_template.tsv` | `templates/manifest_template.tsv` → optional subsystem registry `manifest.tsv` | Keep with bounded non-identity role; `MAP-DATA-06`, `MAP-DATA-11`, `MAP-FLOW-08` | `code_maps.md` |
| `.bonsai/maps/templates/symbol_index.tsv` | canonical `templates/symbol_index_template.tsv` → optional `symbol_index.tsv`; no compatibility copy | Keep behavior + Adapt filename; `MAP-DATA-07`, `MAP-DEFECT-03` | `code_maps.md` |
| `.bonsai/maps/templates/map_state_template.md` | `templates/map_state_template.md` → map-local `map_state.md` | Adapt; `MAP-CONTROL-02`, `MAP-DATA-08`, `MAP-FLOW-08` | `code_maps.md` |

Primary specification evidence: **Code Maps**, **Integrated Mapping Workflow**, **Manage Code Maps**,
**Multi-Repository Source Universes**, **Archaeological Work**, `prompts/create_map_repo.md`, and map maintenance
under **File Maintenance Discipline**.

## Deliberate Exclusions from the Standard Inventory

| Existing path | Treatment | Rationale / later route |
| --- | --- | --- |
| `.bonsai/developer_context.md` | Excluded: repository-specific human context | Context for this implementation, not a shipped standard artifact or archaeological source to rewrite |
| `.bonsai/projects/bonsai-dev/` | Excluded: active repository project memory | Human-owned project truth, execution memory, phase plan, and contract design; preserved through promotion rather than shipped as standard |
| `.bonsai/projects/task-tracker/` | Excluded: possible validation fixture | Not a standard artifact; its eventual fixture role is decided in Batch 5 and it is not converted automatically |

The candidate files currently placed at `repo/bonsai/specification.md` and `repo/bonsai/README.md` are also not
v1.4 archaeological artifacts. Their durable identities are `../../../../../specification.md` and `README.md`.
`../../../../../specification.md` is governing human-owned final truth. The README is the current v2 human-facing guide and is
checked for cross-contract conformance in Step 6. Both are candidate distribution inputs and remain read-only in
Phase 1.

## v2 Target Artifact and Responsibility Routing

| Target artifact or responsibility | Provenance | Batch / owner | Inventory state |
| --- | --- | --- | --- |
| `../../../../../specification.md` | Approved v2 final truth | Governs all batches; Step 6 conformance | Present; not derived from archaeology |
| `README.md` | Approved human-facing v2 guidance | All groups; Step 6 cross-contract review | Present; read-only in Phase 1 |
| `start.md` | Specification-only bootstrap boundary | Batch 2 / `core_workflows.md` | Missing artifact; contract approved |
| `prompts/implementation.md` | Adapt v1.4 implementation kernel | Batch 2 / `core_workflows.md` | Missing staged artifact; contract approved |
| `skills/menu.md` | Extract distributed v1.4 menu rules | Batch 2 / `core_workflows.md` | Missing staged artifact; contract approved |
| `skills/phase_execution.md` | Adapt v1.4 skill | Batch 2 / `core_workflows.md` | Missing staged artifact; contract approved |
| `skills/final_truth_update.md` | Adapt v1.4 skill | Batch 2 / `core_workflows.md` | Missing staged artifact; contract approved |
| `skills/dry_run.md` | Adapt v1.4 skill | Batch 2 / `core_workflows.md` | Missing staged artifact; contract approved |
| `skills/handoff.md` | Adapt v1.4 skill | Batch 2 / `core_workflows.md` | Missing staged artifact; contract approved |
| `skills/agent_context.md` | Broaden v1.4 tooling-memory behavior | Batch 2 / `core_workflows.md`; layering cross-check in Batch 3 | Missing staged artifact; core contract approved; developer/agent boundary cross-check complete |
| `prompts/create_project_memory.md` | Adapt v1.4 design workflow | Batch 3 / `project_workflows.md` | Missing staged artifact; contract approved |
| `templates/plan_phase_template.md` | Adapt v1.4 template | Batch 3 / `project_workflows.md` | Missing staged artifact; contract approved |
| `templates/icebox_template.md` | Adapt v1.4 template | Batch 3 / `project_workflows.md` | Missing staged artifact; contract approved |
| Project Management | Specification-only workflow | Batch 3 / `project_workflows.md`; implemented by `prompts/implementation.md` + `skills/menu.md` | Responsibility complete; no separate artifact justified |
| `skills/bonsai_home.md` | Specification-only Create Bonsai Home workflow | Batch 3 / `project_workflows.md` | Missing staged artifact; new lazy workflow contract approved |
| developer-context loading and layering | Adapt repository-only v1.4 context behavior | Batch 3 / `project_workflows.md`; implemented by `prompts/implementation.md` | Responsibility complete; no separate skill/example artifact justified |
| `prompts/create_map_repo.md` | Adapt v1.4 repository calibration | Batch 4 / `code_maps.md` | Missing staged artifact; contract approved |
| `skills/code_maps.md` | Integrate v1.4 map control plane | Batch 4 / `code_maps.md` | Missing staged artifact; contract approved |
| map-data templates/procedures | Preserve useful v1.4 map structures under the v2 named-source store | Batch 4 / `code_maps.md` | Eight canonical template identities assigned; runtime ownership, optionality, layering, and validation complete |
| validation definitions and output boundaries | Requirements/architecture/specification-only | Batch 5 / `../archive/v2/artifact_contracts/promotion_validation.md` | Contract approved; implementation seam intentionally deferred |
| promotion, rollback, preservation, and execution-memory conversion | Self-hosting requirements/architecture-only | Batch 5 / `../archive/v2/artifact_contracts/promotion_validation.md` | Contract approved; exact host swap/helper packaging remains bounded |
| fresh-session self-hosting proof and staging removal | Self-hosting requirements/architecture-only | Batch 5 / `../archive/v2/artifact_contracts/promotion_validation.md` | Contract approved |
| optional helper scripts | Specification leaves packaging open | Batch 5 / `../archive/v2/artifact_contracts/promotion_validation.md` | Explicit bounded implementation decision; no required artifact inferred |

## Cross-Contract Schema Closure

Every required v2 standard identity has a complete direct or grouped contract. Grouping below is organizational;
it does not create runtime modules or allow one artifact to inherit unmentioned behavior from another.

| Standard artifact identity | Complete contract location | Validation trace |
| --- | --- | --- |
| `../../../../../specification.md` | This file — **Human-Owned Standard Artifact Contracts** | Authority/conformance checks below; `PROMO-VAL-03` |
| `README.md` | This file — **Human-Owned Standard Artifact Contracts** | Guide cross-check below; `MAP-GUIDE-01`; `PROMO-VAL-03` |
| `start.md` | `core_workflows.md` — `start.md` | `CORE-START-01`–`04` |
| `prompts/implementation.md` | `core_workflows.md` — implementation prompt | `CORE-IMPL-01`–`10` plus delegated ownership rows below |
| `prompts/create_project_memory.md` | `project_workflows.md` — project-memory prompt | `PROJECT-MEMORY-01`–`14` |
| `prompts/create_map_repo.md` | `code_maps.md` — map-calibration prompt | `MAP-CAL-01`–`05`; `MAP-DEFECT-01`–`02` |
| `skills/menu.md` | `core_workflows.md` — menu skill | `CORE-MENU-01`–`04` |
| `skills/phase_execution.md` | `core_workflows.md` — phase-execution skill | `CORE-PHASE-01`–`08` |
| `skills/final_truth_update.md` | `core_workflows.md` — final-truth skill | `CORE-TRUTH-01`–`04` |
| `skills/dry_run.md` | `core_workflows.md` — dry-run skill | `CORE-DRY-01`–`04` |
| `skills/handoff.md` | `core_workflows.md` — handoff skill | `CORE-HANDOFF-01`–`06` |
| `skills/agent_context.md` | `core_workflows.md` — agent-context skill; developer boundary in `project_workflows.md` | `CORE-CONTEXT-01`–`06`; `PROJECT-DEVELOPER-06` |
| `skills/bonsai_home.md` | `project_workflows.md` — Bonsai Home skill | `PROJECT-HOME-01`–`04` |
| `skills/code_maps.md` | `code_maps.md` — integrated map skill | `MAP-CONTROL-*`, `MAP-DATA-*`, `MAP-FLOW-*`, `MAP-V2-*` |
| `templates/plan_phase_template.md` | `project_workflows.md` — phase-plan template | `PROJECT-PHASE-TEMPLATE-01`–`04` |
| `templates/icebox_template.md` | `project_workflows.md` — icebox template | `PROJECT-ICEBOX-TEMPLATE-01`–`04` |
| Eight code-map templates | `code_maps.md` — **Standard Template Set** and **Grouped Template Contract Schema** | `MAP-DATA-01`–`08`, `MAP-DATA-11`; `MAP-FLOW-08`; `MAP-DEFECT-03` |

The grouped code-map row covers these exact identities and no implicit extras:

```text
templates/code_map_template.md
templates/map_state_template.md
templates/subsystem_map_template.md
templates/api_pub_template.md
templates/api_ext_template.md
templates/namespace_router_template.tsv
templates/manifest_template.tsv
templates/symbol_index_template.tsv
```

### Required responsibility seams

| Responsibility | Decision owner | Collaborators / boundary | Closure |
| --- | --- | --- | --- |
| Bootstrap and environment identity | `start.md` | Implementation receives resolved identity and does not rediscover it | One owner; closed |
| Minimum-state startup and exact-step routing | `prompts/implementation.md` | Triggered skills own detailed procedure | One router; closed |
| Gate/menu presentation | `skills/menu.md` | Invoking workflow retains authorization and writes | Presentation separated from decision authority; closed |
| Phase planning and contract-first execution | `skills/phase_execution.md` | Menu, final-truth, and handoff skills at their boundaries | No duplicate pass/plan owner; closed |
| Final-truth reconciliation | `skills/final_truth_update.md` | Returns to the invoking workflow after state reconciliation | One impact/update workflow; closed |
| Completion and resume state | `skills/handoff.md` | Phase skill updates detailed phase truth; implementation enforces completion use | No competing completion owner; closed |
| Developer-context loading | `prompts/implementation.md` | `skills/agent_context.md` owns learned context only | Human/agent context ownership separated; closed |
| Project listing/switching/creation | `prompts/implementation.md` | `start.md` owns initial selection; menu owns presentation | No unnecessary project-management artifact; closed |
| Create Bonsai Home | `skills/bonsai_home.md` | `start.md` re-resolves identity after creation | Side-effecting workflow isolated; closed |
| Code-map lifecycle and source alignment | `skills/code_maps.md` | Map prompt supplies optional human calibration; agent context stores reusable locations/selections | Control/data/context roles separated; closed |
| Runtime map-data structure | `code_maps.md` grouped runtime contract | Map skill maintains; source remains authority | Canonical required/optional artifacts explicit; closed |
| Validation and distribution purity | `../archive/v2/artifact_contracts/promotion_validation.md` staged-boundary contract | Approved artifact contracts define expected behavior | No runtime artifact inferred prematurely; closed |
| Candidate, backup, promotion, proof, and cleanup | `../archive/v2/artifact_contracts/promotion_validation.md` state-machine contracts | Exact host driver/package deferred to Phase 5 | Behavior fixed; implementation seam bounded |

No required responsibility has competing durable owners. Shared references above are delegation or boundary checks,
not duplicated authority.

## User-Guide Conformance and Later-Phase Validation Trace

The staged `README.md` promises only behavior owned by the contract layer:

| User-facing area | Owning contract/evidence | Result |
| --- | --- | --- |
| Canonical startup and identity | `start.md`; `CORE-START-*` | Conforms |
| Embedded and reusable Bonsai Home | `start.md`; `skills/bonsai_home.md`; `PROJECT-HOME-*` | Conforms |
| Default, named, and managed projects | Project Management responsibility; `PROJECT-MANAGE-*` | Conforms |
| Project-memory zip and Phase 1 boundary | `prompts/create_project_memory.md`; `PROJECT-MEMORY-*` | Conforms |
| Developer/agent context scopes | Developer Context Layering; `skills/agent_context.md` | Conforms |
| Startup, readiness, planning, final truth, and contracts | Core workflow contracts | Conforms |
| Dry runs, observations, and session continuation | Core workflow contracts | Conforms |
| Map creation, reuse, source alignment, and external-source operation | Map contracts; `MAP-*` | Conforms |
| Optional helper scripts | Specification and promotion bounded decisions | Conforms; no helper is required or inferred |

Later phases inherit this validation trace:

| Phase | Required contract proof before completion |
| --- | --- |
| Phase 2 | Canonical identities/references; bootstrap resolution; minimum-state startup; readiness and primary/secondary menu behavior |
| Phase 3 | Project-memory artifacts; project management; Bonsai Home creation; layered context; phase/final-truth/dry-run/handoff/icebox workflows |
| Phase 4 | Named-source map store, optional calibration/templates, map/source alignment, lifecycle gates, reuse, external source, and map-state discipline |
| Phase 5 | Whole-tree purity/reference checks; six topology scenarios; candidate conversion; backup/restore; failure-tested swap; fresh-session proof; single-tree collapse |

Exact scenarios and failure expectations remain in each owning contract's validation cases and in
`../archive/v2/artifact_contracts/promotion_validation.md` **Cross-Contract Validation Matrix**. This trace assigns later validation without choosing
a test framework, helper package, source-identity registry, or host-specific swap mechanism in Phase 1.

## Known Missing v2 Behavior

All known specification-required behavior without an adequate v1.4 owner is routed:

| Missing responsibility | Owner |
| --- | --- |
| repository-local bootstrap and Bonsai Home resolution | `core_workflows.md` — `start.md` contract |
| reusable human-gate/menu semantics | `core_workflows.md` — `skills/menu.md` contract |
| session-local project selection and project management | `project_workflows.md` — Project Management responsibility owned by `prompts/implementation.md` + `skills/menu.md` |
| Create Bonsai Home | `project_workflows.md` — `skills/bonsai_home.md` |
| developer/repository/project agent-context scopes and precedence | `core_workflows.md` — agent-context skill; `project_workflows.md` — context layering |
| integrated Manage Code Maps routing | `code_maps.md` — code-maps skill |
| source-based map identity and map/source alignment | `code_maps.md` — code-maps skill and map-data candidates |
| project-level relevant-map selection without project-owned map identity | `code_maps.md` — code-maps skill; agent-context integration in `core_workflows.md` |
| staged validation, transactional promotion, rollback, memory conversion, and fresh-session proof | `../archive/v2/artifact_contracts/promotion_validation.md` |

No known required responsibility remains unrouted. Remaining unresolved detail concerns specification-deliberate
minimal source-identity/discovery mechanics, host-specific promotion packaging, and the human disposition of the
v1.4 `task-tracker` example before promotion—not whether the required behavior exists.

## Inventory Closure Status

- v1.4 standard artifacts: **23 accounted for** — 6 Core, 5 Project/Context, 12 Mapping.
- repository-local context/project paths: **3 deliberately excluded categories** with later handling stated.
- known missing v2 responsibilities: **all assigned** to a contract group or explicit unresolved seam.
- evidence method: **defined** for source, specification, classification, rationale, owner, and validation trace.
- Batch 2 core execution: **archaeology complete; approved** — 46 material evidence records close all
  six v1.4 sources and the specification-only bootstrap/menu/context behavior; no core ownership seam remains
  unresolved.
- Batch 3 project/context: **archaeology complete; approved** — 35 material evidence records close the
  five primary v1.4 sources, assign Project Management to the kernel/menu, assign Create Bonsai Home to one
  lazy-loaded skill, keep developer-context layering in the kernel, and leave no project/context ownership seam
  unresolved.
- Batch 4 integrated code maps: **archaeology complete; approved** — 44 material evidence records
  close all twelve v1.4 mapping artifacts, resolve all three known stale-reference/naming defects without
  compatibility artifacts, preserve user-directed/contextual maintenance, and assign the v2 control/data/template
  seams. The exact minimal source-identity metadata and automatic dependency-to-map discovery mechanics remain
  deliberately implementation-level validation questions under the specification, not unowned behavior.
- Batch 5 promotion/validation: **archaeology complete; approved** — 38 material evidence records
  define staged purity, isolated validation, exact memory classification/conversion, verified backup/rollback,
  transactional swap invariants, fresh-session proof, and final single-tree collapse. Host-specific swap/helper
  packaging remains a bounded Phase 5 decision; `task-tracker` requires approved fixture relocation or retirement
  before live promotion.
- cross-contract schema and ownership closure: **complete** — every required standard identity and responsibility
  has a direct or grouped contract, guide conformance is traced, and later-phase validation obligations are routed.
- final-truth conformance: **contract-layer clarification only** — the closure makes standard-artifact schema and
  grouped template ownership explicit; approved requirements, architecture, `bonsai/specification.md`, and
  `bonsai/README.md` remain unchanged.
- Phase 1 final review: **approved** — the complete contract layer is implementation authority for later phases.
- staged v2 implementation authorization: **none yet**; Phase 2 activation planning must resolve execution mode and
  any required detailed phase plan before implementation begins.
