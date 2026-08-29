# Artifact Contracts — Code Maps

**Project:** `bonsai-dev`  
**Status:** Phase 1 mapping archaeology complete; contract batch approved

> **Identity and placement:** Standard-artifact identities are relative to the Bonsai standard root. During this
> refactor, candidate standard artifacts are staged at `repo/bonsai/<artifact-identity>`. Runtime map data is not
> staged distribution content: it lives under the active Bonsai map store at `$BONSAI_HOME/maps/<source>/` or,
> for Embedded Bonsai, `repo/.bonsai/maps/<source>/`.

## Mapping Preservation Stance

The v1.4 mapping subsystem contains mature navigation and compression behavior worth retaining. Bonsai v2 changes
its standalone control plane, map-store placement, and source/project/context identity model; those changes do not
justify redesigning useful map data for neatness.

Actual source remains authoritative. Project memory and optional human-owned `map_repo.md` calibration influence
attention but do not become source evidence or map identity.

Code-map creation and maintenance remain user-directed or contextually offered workflows. Bonsai does not perform
continuous map revision checking, silently rewrite maps after ordinary code changes, or treat every implementation
session as map maintenance.

## Archaeological Identity Decisions

### `repo_prompt.md` is stale, not an artifact

Observed evidence:

- `.bonsai/maps/repo_session.md` exists and contains the complete Web UI repository-calibration workflow.
- `.bonsai/maps/README.md` consistently directs humans to `repo_session.md`.
- `.bonsai/maps/repo_prompt.md` does not exist.
- `.bonsai/maps/map_system.md` refers to `repo_prompt.md` only in its Pass 0 instructions and update-trigger heading.

**Decision:** Drop `repo_prompt.md` as a filename and compatibility identity. Adapt the actual `repo_session.md`
behavior into v2 `prompts/create_map_repo.md`. No v2 artifact may reference or provide `repo_prompt.md`.

### `templates/map_repo_template.md` is stale, not missing behavior

Observed evidence:

- `.bonsai/maps/templates/map_repo_template.md` does not exist.
- `.bonsai/maps/repo_session.md` contains the full inline `map_repo.md` synthesis structure and output protocol.
- `.bonsai/maps/README.md` explicitly says the inline structure means no separate repository template is required.
- Only `.bonsai/maps/map_system.md` lists or instructs use of the nonexistent template.

**Decision:** Drop the separate `map_repo_template.md` identity. Keep and adapt its intended structural behavior
inside `prompts/create_map_repo.md`. Do not create a v2 template to make the stale v1 reference consistent.

### The symbol-index template has one v2 identity

Observed evidence:

- The actual file is `.bonsai/maps/templates/symbol_index.tsv`.
- `.bonsai/maps/map_system.md` and `.bonsai/maps/README.md` consistently describe and consume
  `symbol_index_template.tsv`.
- No `symbol_index_template.tsv` file exists, and no executable consumer establishes the shorter template filename
  as a contract.
- The actual TSV content has the documented output columns and is clearly template content, not generated map data.

**Decision:** Keep the optional selective `symbol_index.tsv` behavior and Adapt the template identity to the
standard-root-relative `templates/symbol_index_template.tsv`. Do not retain `templates/symbol_index.tsv` as a
compatibility artifact or second identity.

---

## Archaeological Evidence and Classification

The evidence records below close the material behavior in all twelve Batch 4 artifacts. Repeated rules are
consolidated rather than classified as wording.

### Repository calibration

| Evidence | Source evidence | Specification rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `MAP-CAL-01` | `repo_session.md` — Purpose, Session Behavior, Synthesis Priorities | **Code Maps / Mapping inputs / Web UI mapping calibration** | Adapt | Preserve facts, owner weighting, priorities, caveats, and practical evidence in `prompts/create_map_repo.md`; source identity and v2 placement change. | Calibration output distinguishes observed facts, owner weighting, and qualified uncertainty. |
| `MAP-CAL-02` | `repo_session.md` — Do not invent repository details | **Maps and source must agree**; **Archaeological Work** | Keep | Unknown repository detail stays unknown; owner conversation is not proof. Owned by `prompts/create_map_repo.md`. | An underspecified conversation produces explicit open questions rather than invented roots, modules, or seams. |
| `MAP-CAL-03` | `repo_session.md` — Mapping-Scope Discipline | **Integrated Mapping Workflow** | Keep | In-scope, calibration-only, and out-of-scope distinctions prevent accidental expansion. Owned by the calibration prompt and enforced by the code-map skill. | Calibration-only and excluded areas do not receive map artifacts unless the human expands scope. |
| `MAP-CAL-04` | `repo_session.md` — When to Generate; Final Output Protocol | `prompts/create_map_repo.md` | Adapt | Preserve user-controlled synthesis and one complete `map_repo.md` output; v2 prompt identity and storage guidance change. | The prompt remains conversational until synthesis is requested and then emits one complete artifact without filler. |
| `MAP-CAL-05` | `repo_session.md` — Inline Output Template; `README.md` — `repo_session.md` role | **Framework Templates** | Adapt + Drop | Preserve the structural fields inline in the v2 prompt; drop nonexistent `map_repo_template.md`. | The prompt can produce conforming calibration without any separate repository template. |

### Integrated control plane and gates

| Evidence | Source evidence | Specification rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `MAP-CONTROL-01` | `map_prompt.md` — Startup Sequence and Startup Gate | **Integrated Mapping Workflow**; **Human Gates and Menus** | Adapt | Preserve a concise proposal and explicit human proceed/redirect gate inside `skills/code_maps.md`; drop the standalone startup entry point. | Explicit Manage/Startup entry reports source, operation, scope, next step, and waits before substantive mapping. |
| `MAP-CONTROL-02` | `map_prompt.md` — Mapping Workspace Initialization | **Agent Execution Memory**; **Lazy Loading** | Adapt | Preserve short map-local resume state, but create/read it only for an active mapping workflow. | A new map initializes concise state from its template; an existing map resumes without replaying history. |
| `MAP-CONTROL-03` | `map_prompt.md` — After the Human Proceeds | **Integrated Mapping Workflow** | Adapt | Preserve bounded source/artifact reads and writes within the approved mapping action. Project/menu routing now invokes the skill. | An approved subsystem update does not expand into unrelated map creation. |
| `MAP-CONTROL-04` | `map_prompt.md` — When Current Mapping Scope Appears Complete | **Human control should not require constant babysitting** | Keep | Do not invent work solely to continue a mapping session. | A complete scope reports completion and offers human-directed actions without selecting new scope automatically. |
| `MAP-CONTROL-05` | `map_prompt.md` — System-Control Files; `map_system.md` — Control Responsibilities | **Integrated Mapping Workflow**; **Framework Skills** | Adapt + Drop | Durable edit rules move to `skills/code_maps.md`; standalone `map_prompt.md` and `map_system.md` are dropped as v2 runtime artifacts. Human-owned `map_repo.md` remains protected. | Ordinary map operations cannot silently edit human-owned calibration or standard workflow files. |
| `MAP-CONTROL-06` | `map_prompt.md` and `README.md` — standalone entry/cadence | **Integrated Mapping Workflow** | Drop | Drop `Read .bonsai/maps/map_prompt.md` and parallel mapping-system startup. v2 enters through `start.md`, Manage Code Maps, or explicit startup request. | Staged v2 guidance contains no standalone map-prompt entry instruction. |

### Map data, evidence, and layering

| Evidence | Source evidence | Specification rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `MAP-DATA-01` | `map_system.md` — Layer Responsibilities; all Markdown templates | **Code Maps / Map entry document** | Keep + Adapt | Preserve entry → subsystem → optional API layering under each named source map; add source identity to the entry. | A normal consumer can load `code_map.md` first and drill down without loading all map data. |
| `MAP-DATA-02` | `map_system.md` — `code_map.md`; `code_map_template.md` | **Code Maps / Map entry document** | Adapt | Preserve compact repository compass and routing; v2 requires trustworthy source identity and map-store-relative links. | Entry identifies source sufficiently for alignment and remains compact rather than a project/session guide. |
| `MAP-DATA-03` | `map_system.md` — `namespace_router.tsv`; its template | **Deterministic discovery should be cheap**; retain useful indexes | Keep | Retain optional lazy-loaded fuller namespace routing when it materially reduces navigation cost. | It is absent for small maps and strict/compact when created; `code_map.md` does not duplicate it wholesale. |
| `MAP-DATA-04` | `map_system.md` — subsystem responsibilities; `subsystem_map_template.md` | retain useful mature map structures | Keep | Preserve architectural-domain maps, not automatic folder/module mirrors. | Each subsystem has a demonstrated durable responsibility and source-backed owning paths. |
| `MAP-DATA-05` | `map_system.md` — `api_pub.md` / `api_ext.md`; API templates | retain useful mature map structures | Keep | Preserve optional decision-ready caller and extension mechanics only when they earn their maintenance cost. | A subsystem can omit either API map; generated API maps contain non-obvious reusable mechanics, not API dumps. |
| `MAP-DATA-06` | `map_system.md` — `manifest.tsv`; its template | **Design Boundaries / Map manifest detail** | Keep, bounded | Retain the optional compact subsystem registry as navigation/process support, but do not make it the required source-identity manifest or expand its fixed role while v2 identity metadata remains deliberately minimal. | Map creation does not require `manifest.tsv`; if present it remains a strict subsystem/path registry and cannot be the sole alignment proof. |
| `MAP-DATA-07` | `map_system.md` — `symbol_index.tsv`; actual `templates/symbol_index.tsv` | retain useful source-navigation structures | Keep + Adapt | Preserve optional selective high-value symbol routing; normalize only the template identity. | The index is not created by default, remains non-exhaustive TSV, and its template has one canonical name. |
| `MAP-DATA-08` | `map_system.md` — `map_state.md`; `map_state_template.md` | **Agent Execution Memory** principles | Adapt | Preserve concise agent-owned mapping baton state inside the named source map; remove standalone-session history and obsolete AI-product coupling. | State contains current objective/focus/next step/uncertainty only and is not loaded during ordinary map consumption. |
| `MAP-DATA-09` | `map_system.md` — Evidence Discipline | **Maps and source must agree**; **Archaeological Work** | Keep | Preserve Observed/Inferred/Uncertain distinctions for non-obvious claims; calibration remains bias, not proof. | Source disagreement corrects the map or blocks reliance; uncertainty is explicit. |
| `MAP-DATA-10` | `map_system.md` — Repository Maps vs Project Memory; `code_map_template.md` | **Maps describe source, not projects** | Adapt | Preserve separation from active phase/state; v2 may use relevant project truth only as calibration input. | Map content contains no active project status, requirements trace, or planned-but-absent source claims. |
| `MAP-DATA-11` | `map_system.md` — Lookup Artifact Formatting; TSV templates | retain useful mature structures | Keep | Preserve literal tabs, fixed columns, one-line rows, terse notes, and structural checks. | Automated fixture validation detects wrong separators, column drift, multiline cells, and prose rows. |
| `MAP-DATA-12` | `map_system.md` — Naming Rules | **Map identity follows source identity** | Keep + Adapt | Preserve stable subsystem and standard per-subsystem names; source directory naming now follows v2 source identity. | Folder names are source/domain identities, not consuming project names or incidental build units. |

### Mapping method, maintenance, and restraint

| Evidence | Source evidence | Specification rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `MAP-FLOW-01` | `map_system.md` — Recommended Build Order; `README.md` — Full Usage Guide | **Integrated Mapping Workflow** | Adapt | Preserve orientation-before-depth and calibration/subsystem/maintenance/cleanup modes; calibration is optional, not mandatory Pass 0. | Creation can proceed from source/project memory without `map_repo.md`; deeper mapping follows an approved bounded order. |
| `MAP-FLOW-02` | `README.md` / `map_system.md` — one subsystem per clean session | **AI sessions are the primary interaction model**; **Session Boundaries** | Adapt | Preserve one-active-subsystem discipline and fresh-session advice when context is heavy, without making session reset a mandatory artifact rule. | State supports a clean continuation; changing subsystem requires an explicit next scope rather than silent carryover. |
| `MAP-FLOW-03` | `map_system.md` — finish subsystem then evaluate API maps | retain mature mapping internals | Keep | Avoid leaving high-value subsystem mechanics indefinitely unevaluated while expanding breadth. | Completion records whether caller/extension maps were created or deliberately unnecessary. |
| `MAP-FLOW-04` | `map_system.md` — Calibration | **Mapping inputs**; source authority | Keep | Validate abstractions against representative production code, tests, examples, and observed call sites. | At least one representative-use check is required when apparent design and actual usage may diverge. |
| `MAP-FLOW-05` | `map_system.md` — Maintenance After Code Changes and Update Triggers; `README.md` — Stage 6 | **File Maintenance Discipline / Maps** | Adapt | Preserve material-change thresholds, but maintenance is user-directed or contextually offered—not continuous, automatic, or triggered by routine churn. | Routine fixes do not prompt or mutate maps; a known material structural change can surface a bounded maintenance action once. |
| `MAP-FLOW-06` | `map_system.md` — Compression Discipline and Done Criteria | **Context should be loaded when useful** | Keep | Preserve per-artifact compression and completion criteria. | Fixtures reject top-level encyclopedias, map-state histories, API dumps, and redundant lookup content. |
| `MAP-FLOW-07` | `map_system.md` — Prioritization and Drift Prevention | **Code Maps**; **Lazy Loading** | Keep | Preserve value-weighted selection, anti-sprawl rules, optionality, and source-over-calibration discipline. | Large/obvious low-value areas do not outrank owner-weighted or architecturally useful areas without evidence. |
| `MAP-FLOW-08` | `map_system.md` — Template Responsibilities; all templates | **Framework Templates** | Adapt | Retain templates only where `skills/code_maps.md` explicitly consumes them; template presence never forces output creation. | Every referenced standard template exists at one canonical path; optional outputs remain absent unless justified. |

### v2 integration and missing v1 behavior

| Evidence | Source evidence | Specification rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `MAP-V2-01` | No adequate v1 behavior | **Map store and source names**; **Map identity follows source identity** | Missing | `skills/code_maps.md` must resolve active store and name maps for source universes rather than projects. | Shared and Embedded fixtures store the same logical map under the correct active store and source name. |
| `MAP-V2-02` | v1 fixed `.bonsai/maps/` layout | **Mapping context and map storage are separate** | Adapt | Source inspection/context follows the mapped source; durable output follows the active map store. | Mapping external source from another working directory does not write map data into that source by assumption. |
| `MAP-V2-03` | `repo_session.md` supports conversation-only calibration | **External source without Bonsai project memory** | Adapt | Combine actual external source with optional calibration; project memory is not required. | External-source fixture creates a reusable named map without `.bonsai/projects/`. |
| `MAP-V2-04` | v1 repository-local single map system | **Multi-Repository Source Universes** | Missing | Reuse one source map across several projects and select several relevant source maps for one project. | `investment-app`, `barcache`, and `tickerview` fixture proves reuse without per-project duplication. |
| `MAP-V2-05` | No adequate v1 behavior | **Agent Context / scopes** | Missing | Stable source locations and project-relevant map selection may be preserved through `skills/agent_context.md` at the narrowest reusable scope. | A rediscovered stable source location is reused later; active project selection is not stored as context. |
| `MAP-V2-06` | v1 only create/update session flow | **Manage Code Maps** | Missing | The code-map skill owns Create, Inspect, Update/Rebuild, Remove, and Inspect Map/Source Identity actions. | Each lifecycle action is selectable; read-only inspection does not mutate; destructive removal/rebuild requires explicit authority. |
| `MAP-V2-07` | No adequate v1 behavior | **Manage Code Maps / First-use behavior** | Missing | Substantial unmapped existing source may receive one contextual creation action; declined creation moves to secondary options; greenfield stays quiet. | Decline is not repeatedly surfaced; greenfield fixture receives no map pressure. |
| `MAP-V2-08` | No adequate v1 behavior | **Human Gates / Subordinate workflows**; **Integrated Mapping Workflow** | Missing | Mapping returns to its invoking gate after state/context reconciliation. | Completion of Manage Code Maps resumes the refreshed parent menu or implementation gate. |
| `MAP-V2-09` | v1 says source is truth but lacks snapshot alignment | **Maps and source must agree**; **Map and source identity** | Missing | `code_map.md` carries the smallest useful source identity; mismatch blocks silent reliance and routes to inspect/update/rebuild/alternate source. | Version/revision mismatch is detected and explicitly resolved before non-obvious map claims are trusted. |

### Defect-specific closure and user guidance

| Evidence | Source evidence | Specification rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `MAP-DEFECT-01` | `map_system.md` Pass 0 and Update Triggers reference absent `repo_prompt.md`; actual `repo_session.md` and guide agree | `prompts/create_map_repo.md`; **Migration** out of scope | Drop | No alias or compatibility artifact. The actual behavior adapts directly to the specified v2 prompt. | Repository-wide staged-standard reference scan finds no `repo_prompt.md`; every workflow reference resolves. |
| `MAP-DEFECT-02` | `map_system.md` lists absent `map_repo_template.md`; `repo_session.md` embeds shape; guide says separate template unnecessary | **Framework Templates** | Drop | No v2 template; prompt owns its output structure. | Reference scan finds no `map_repo_template.md`; calibration validation succeeds without one. |
| `MAP-DEFECT-03` | actual `templates/symbol_index.tsv`; documented consumers expect `symbol_index_template.tsv` | **Framework Templates** | Adapt | One canonical v2 template identity: `templates/symbol_index_template.tsv`. | Distribution contains and references only that template identity; output remains `symbol_index.tsv`. |
| `MAP-GUIDE-01` | `.bonsai/maps/README.md` | v2 `README.md` Code Maps guidance | Adapt + Drop | Preserve integrated user concepts and examples in root `README.md`; drop a standalone mapping guide/runtime entry model. | v2 guide routes through `start.md`/Manage Code Maps and contains no stale v1 control filenames. |

---

## Artifact: `prompts/create_map_repo.md`

**Classification:** Adapt from `.bonsai/maps/repo_session.md`

### Role

Optional Web UI workflow for creating or refining human-owned, source-specific mapping calibration.

### Loaded when

The human explicitly opens the prompt to calibrate a source repository, especially when project memory is absent
or additional owner emphasis is useful.

### Inputs

- the human conversation;
- repository facts and reference material explicitly supplied for the session;
- source identity when already known.

### Responsibilities

- help distinguish facts, owner weighting, hypotheses, and uncertainty;
- elicit only questions that materially improve mapping scope or evidence quality;
- distinguish in-scope, calibration-only, and out-of-scope source areas;
- synthesize one complete `map_repo.md` only on explicit human cue;
- use an inline stable output shape covering identity, source/build/runtime shape, owner weighting, scope,
  practical evidence, conventions, biases, oddities, ignore paths, evidence hierarchy, optional lookup guidance,
  and material open questions;
- guide the human to place the output under the applicable named source map.

### Must not

- invent repository details;
- elevate tentative claims into observed facts;
- treat calibration as product truth, architecture truth, source proof, or map identity;
- force calibration before code-map creation;
- write into source or the map store automatically from a Web UI conversation;
- depend on `repo_prompt.md` or a separate `map_repo_template.md`.

### Reads

Conversation and explicitly supplied references only.

### Writes

Produces the complete content of one human-owned `map_repo.md` for human review/placement. It does not mutate
the repository or map store itself.

### Delegates to

None. Later code-map creation is performed through `skills/code_maps.md`.

### Human gates

- the human decides when enough calibration exists;
- the human explicitly requests synthesis;
- the human reviews and places the output.

### Preserve from existing version

Focused questioning; fact/weight/uncertainty distinctions; strict no-invention rule; scope boundaries;
representative evidence; compact output; material open questions; optional lookup guidance.

### v2 changes

- canonical identity is `prompts/create_map_repo.md`;
- the prompt targets a named source map in the active store;
- project memory may complement it but is not required;
- no separate repository template exists;
- no `repo_prompt.md` compatibility identity exists.

### Validation cases

- external source with no project memory;
- source with project memory plus extra owner weighting;
- uncertain user claims remain qualified;
- explicit scope exclusions survive synthesis;
- generation works without any repository template file;
- no calibration needed.

---

## Artifact: `skills/code_maps.md`

**Classification:** Major Adapt from `.bonsai/maps/map_prompt.md`, `.bonsai/maps/map_system.md`, and applicable
user guidance from `.bonsai/maps/README.md`; includes Missing v2 integration behavior.

### Role

Lazy-loaded skill that integrates code-map creation, inspection, maintenance, removal, identity checking, and
map-guided navigation with Bonsai startup, menus, context, and source identity.

### Loaded when

- the human selects **Manage Code Maps**;
- an explicit startup request asks for a code-map action;
- the current implementation facet requires map-guided navigation or map/source alignment;
- Bonsai contextually offers first-use creation for a substantial existing source and the human proceeds;
- a material structural source change makes bounded map maintenance contextually relevant and the human proceeds.

Ordinary source edits and routine map consumption do not load the full editing procedure.

### Inputs

- active Bonsai Home or Embedded map store;
- source identity and actual source location/snapshot;
- selected lifecycle action and human-approved scope;
- relevant project final truth or archaeological analysis when available;
- optional source-local calibration `map_repo.md`;
- applicable developer/agent context;
- existing named map data;
- standard templates only for artifacts being created.

### Responsibilities

Provide these lifecycle actions:

- Create Code Map;
- Inspect Code Maps;
- Update or Rebuild Code Map;
- Remove Code Map;
- Inspect Map/Source Identity.

For all actions:

- resolve the map store independently from the source being mapped;
- identify the source independently from the active project;
- make the action, source, map identity, bounded scope, and proposed next step visible;
- obtain human proceed/redirection before substantive mapping or destructive mutation;
- use actual source as authority;
- treat project memory and `map_repo.md` as calibration, not proof;
- preserve explicit uncertainty;
- keep reads and writes bounded to the approved action;
- reconcile map state and qualifying agent context;
- return to the invoking Bonsai gate.

For creation/update/rebuild:

- build orientation before deep mapping;
- preserve source identity in the entry document using the smallest metadata sufficient for alignment;
- create deeper subsystem/API/lookup artifacts only when justified;
- keep one active subsystem scope at a time;
- evaluate warranted caller/extension maps before moving past that subsystem;
- calibrate against representative real usage when design and usage might differ;
- apply evidence, strict TSV, compression, done, and drift-prevention rules in this contract;
- maintain short map-local `map_state.md` only while it improves continuation.

For inspection/consumption:

- load `code_map.md` first;
- load deeper artifacts only for the current facet;
- verify map/source alignment before relying on non-obvious claims;
- route to source inspection rather than treating map assertions as authority.

For contextual first use and maintenance:

- offer creation once when a substantial existing source lacks a useful map;
- leave declined creation under secondary options rather than repeatedly interrupting;
- defer greenfield mapping;
- surface maintenance only for known material structural changes or explicit human request;
- never continuously scan for map drift or automatically revise maps after routine code changes.

### Must not

- name a map after a consuming project when source identity differs;
- create duplicate maps per project for one source universe;
- require source project memory;
- assume a development checkout matches a released dependency;
- silently use an incompatible map snapshot;
- replace source inspection with maps or calibration;
- broaden mapping scope without human direction;
- create optional artifacts because templates exist;
- make `manifest.tsv` mandatory or its subsystem registry the sole identity record;
- turn `code_map.md` into project state, a package registry, or an encyclopedia;
- turn subsystem/API maps into source replicas or exhaustive reference manuals;
- turn lookup TSVs into prose or exhaustive indexes;
- turn `map_state.md` into history;
- automatically check/revise maps continuously;
- expose v1 standalone control identities in v2.

### Reads

- actual selected source and its build/tests/examples as needed;
- relevant project final truth and archaeological analysis;
- optional source map `map_repo.md`;
- scoped developer/agent context;
- named map `code_map.md`, `map_state.md`, deeper artifacts, and optional lookup data;
- standard templates for new artifacts.

### Writes

Within the named source directory in the active map store:

```text
<map-store>/<source>/
    map_repo.md                       # Human-owned; never silently rewritten
    code_map.md
    map_state.md                      # When useful for active mapping continuation
    namespace_router.tsv              # Optional
    manifest.tsv                      # Optional subsystem registry
    symbol_index.tsv                  # Optional selective index
    subsystems/<subsystem>/map.md
    subsystems/<subsystem>/api_pub.md # Optional
    subsystems/<subsystem>/api_ext.md # Optional
```

It may maintain qualifying source locations or selection rules only through `skills/agent_context.md` at the
narrowest reusable scope.

### Delegates to

- `skills/menu.md` for menu/gate presentation and invoking-gate return;
- `skills/agent_context.md` for durable source/map operational knowledge;
- normal final-truth or observation handling only if the mapping action independently triggers those workflows.

### Human gates

- lifecycle action selection;
- source/map identity ambiguity;
- mapping scope and proceed/redirect;
- destructive remove or rebuild;
- explicit choice to expand scope or create optional high-cost map data;
- mismatch resolution when the selected source and map do not align.

### Preserve from existing version

Bounded mapping state; orientation-before-depth; layered selective maps; architectural subsystem selection;
optional API and lookup data; actual-source authority; evidence labels; representative-use calibration; strict TSV
shape; one-active-subsystem discipline; prioritization; compression; done criteria; drift prevention; state pruning;
no invented next objective.

### v2 changes

- entry is integrated with normal startup and menus;
- store resolution supports Bonsai Home and Embedded modes;
- map identity follows source, not project;
- mapping context and output storage are separate;
- external source needs no Bonsai project memory;
- several projects may reuse a map and one project may use several maps;
- source-location/selection knowledge integrates with scoped agent context;
- source snapshot alignment is required;
- lifecycle includes inspect/remove/identity actions;
- subordinate work returns to the invoking gate;
- creation and maintenance are user-directed/contextual, not automatic;
- standalone `map_prompt.md`, `map_system.md`, and mapping README are not v2 runtime artifacts.

### Validation cases

- shared-home and Embedded current-repository mapping;
- external source without project memory;
- project memory only, `map_repo.md` only, and both together;
- one source map reused by several projects;
- one project uses `investment-app`, `barcache`, and `tickerview` maps;
- released-source and active-checkout identities do not silently cross;
- identity mismatch routes to an explicit choice;
- inspect is read-only; remove/rebuild is gated;
- declined first-use creation does not recur as a primary interruption;
- greenfield source receives no map pressure;
- routine fixes do not trigger maintenance;
- a material structural change can produce one bounded contextual maintenance action;
- completed subordinate work returns to the refreshed invoking gate.

---

## Runtime Map Data Contract

### Ownership and location

| Runtime artifact | Ownership | Required | Role |
| --- | --- | --- | --- |
| `map_repo.md` | Human-owned | No | Optional source-specific calibration and scope guidance |
| `code_map.md` | Agent-owned | Yes for a usable map | Normal entry, source identity, compact repository compass, drill-down routing |
| `map_state.md` | Agent-owned | Only when active continuation benefits | Current mapping objective/focus/uncertainty/next step; no history |
| `namespace_router.tsv` | Agent-owned | No | Lazy fuller namespace/package ownership routing |
| `manifest.tsv` | Agent-owned | No | Compact subsystem-to-owning-path registry; not required identity metadata |
| `symbol_index.tsv` | Agent-owned | No | Selective high-value symbol-to-source routing |
| `subsystems/<subsystem>/map.md` | Agent-owned | Per justified mapped subsystem | Architectural-domain scope, ownership, workflows, seams, risks |
| `subsystems/<subsystem>/api_pub.md` | Agent-owned | No | Non-obvious reusable caller mechanics |
| `subsystems/<subsystem>/api_ext.md` | Agent-owned | No | Non-obvious reusable extension mechanics |

All artifacts live under one named source directory in the active map store. Generated map data is not part of
the shipped Bonsai standard and is never written into the staged `bonsai/` distribution.

### Entry and identity

`code_map.md` is the required normal entry document. It must include:

- logical source name;
- source type/location information only when it materially supports selection;
- version, Git revision, artifact coordinate, or equivalent snapshot identity when needed to prevent mismatch;
- compact repository orientation and high-value routing;
- relative links to deeper artifacts;
- an explicit reminder that source is authoritative.

The identity representation remains deliberately minimal and evidence-driven. This contract does not introduce a
mandatory registry, universal manifest schema, or automatic dependency-to-map resolver while those mechanisms are
still being validated by the specification.

### Layering and loading

```text
code_map.md
    → namespace_router.tsv when fuller routing is needed
    → subsystems/<subsystem>/map.md for relevant architecture
        → api_pub.md for caller mechanics when present
        → api_ext.md for extension mechanics when present
    → manifest.tsv or symbol_index.tsv only for their narrow lookup roles
```

`map_repo.md` and `map_state.md` are mapping-workflow inputs, not ordinary implementation startup dependencies.
Implementation loads only the entry and the deeper facet needed for the current task.

### Structural rules

- subsystem boundaries represent architectural responsibility, not folders by default;
- maps preserve navigation and decision-ready mechanics, not exhaustive source extraction;
- `code_map.md` may hold only a small high-value namespace router;
- optional artifacts exist only when demonstrated navigation value exceeds maintenance cost;
- every non-obvious claim is source-backed or visibly Inferred/Uncertain;
- source/project execution state never leaks into map data;
- Markdown layers do not duplicate one another;
- TSV files preserve their canonical headers, literal tabs, fixed columns, one logical row per line, and concise
  cells;
- update related artifacts together only when the approved map change affects them;
- state is pruned whenever the active objective, uncertainty, or next step changes.

### Completion and maintenance

A mapping scope is complete when the entry routes correctly, every approved subsystem has sufficient architecture
memory, each active subsystem's API-map need is resolved, identity is trustworthy enough for intended use,
uncertainty is explicit, and current mapping state either names a real next step or says the scope is complete.

Maintenance is justified by material changes to source identity, public structure, extension mechanics, lifecycle,
architectural relationships, subsystem ownership, or reusable routing. Routine bug fixes, private refactors,
tests, cosmetic cleanup, and ordinary source churn do not justify map work by themselves.

---

## Standard Template Set

These standard-root-relative templates are consumed explicitly by `skills/code_maps.md` when creating the
corresponding runtime artifact:

| Canonical template identity | Runtime output | Classification |
| --- | --- | --- |
| `templates/code_map_template.md` | `code_map.md` | Keep + Adapt for v2 source identity and map-store-relative routing |
| `templates/map_state_template.md` | `map_state.md` | Adapt for integrated workflow and concise state semantics |
| `templates/subsystem_map_template.md` | `subsystems/<subsystem>/map.md` | Keep |
| `templates/api_pub_template.md` | `subsystems/<subsystem>/api_pub.md` | Keep; optional output |
| `templates/api_ext_template.md` | `subsystems/<subsystem>/api_ext.md` | Keep; optional output |
| `templates/namespace_router_template.tsv` | `namespace_router.tsv` | Keep; optional output |
| `templates/manifest_template.tsv` | `manifest.tsv` | Keep, bounded to optional subsystem registry |
| `templates/symbol_index_template.tsv` | `symbol_index.tsv` | Keep behavior + Adapt filename from actual v1 file |

There is no `templates/map_repo_template.md`. Its intended output structure is owned inline by
`prompts/create_map_repo.md`.

Template presence does not authorize artifact creation. Existing runtime map files are improved in place unless an
explicit normalization/rebuild action is approved.

### Grouped Template Contract Schema

The eight identities above share one complete behavioral schema while retaining their distinct runtime outputs and
classification rows.

- **Role:** Provide canonical starting structure for the corresponding map-data artifact without making that
  artifact mandatory.
- **Loaded when:** `skills/code_maps.md` is creating the corresponding justified runtime artifact. No template is a
  routine startup or map-consumption read.
- **Inputs:** The approved mapping action, actual source evidence, trustworthy source identity, relevant optional
  calibration/project context, and the corresponding runtime-data role defined above.
- **Responsibilities:** Encode the stable fields and formatting constraints for only its named output; preserve
  relative map-store routing, evidence discipline, compression, optionality, and strict TSV shape where applicable.
- **Must not:** Force output creation, introduce project/session state into map data, become an exhaustive source
  dump, duplicate another layer, or expose stale/compatibility template identities.
- **Reads:** None directly. The code-map skill supplies the loaded source/context needed for instantiation.
- **Writes / Output:** Only the one runtime artifact named by its Standard Template Set row, under the selected
  named-source map. Template instantiation never writes into the staged standard.
- **Delegates to:** None. `skills/code_maps.md` owns creation, maintenance, gates, and map/source alignment.
- **Human gates:** No independent template gate. The selected map lifecycle action and any high-cost optional output
  remain governed by the code-map skill's human gates.
- **Preserve from existing version:** Preserve each row's useful v1 structure, selective/layered role, and strict
  formatting; the symbol-index behavior survives under one corrected template identity.
- **v2 changes:** Add v2 source-identity/store semantics where applicable, remove obsolete standalone-control
  assumptions, and retain no `map_repo_template.md` or `templates/symbol_index.tsv` compatibility artifact.
- **Validation cases:** Every identity exists once in the candidate; every standard reference resolves; each
  instantiated output matches its runtime role and structural constraints; optional outputs remain absent when not
  justified; stale v1 names are absent.

---

## Cross-Artifact Validation Obligations

Later implementation and validation must prove:

1. **Reference integrity:** every standard-artifact reference resolves; no v2 file/path/reference named
   `repo_prompt.md`, `map_repo_template.md`, or `templates/symbol_index.tsv` survives.
2. **Single identity:** the only symbol-index template identity is `templates/symbol_index_template.tsv`; the
   runtime output remains `symbol_index.tsv`.
3. **Calibration without invented template:** `prompts/create_map_repo.md` produces a complete `map_repo.md`
   without loading a separate map-repository template.
4. **Integrated entry:** human-facing and agent-facing workflows route through `start.md`, explicit startup
   requests, or **Manage Code Maps**, never a parallel mapping bootstrap.
5. **User direction:** create/update/rebuild/remove operations require an explicit or contextually accepted action;
   no continuous map revision checker or automatic maintenance loop exists.
6. **Store/source separation:** selected source may be outside the active repository while output goes only to the
   active named map store.
7. **Identity trust:** a mismatched version/revision/source type cannot be silently treated as aligned.
8. **Topology:** standalone, Bonsai Home, large monorepository, multi-repository, external-source, and greenfield
   cases behave as required by the specification.
9. **Reuse:** several projects can consume one source map and one project can select several source maps without
   duplication by project name.
10. **Optionality:** `map_repo.md`, API maps, namespace router, manifest, symbol index, and active state are omitted
    when their criteria are not met.
11. **Layer restraint:** entry, subsystem, API, lookup, calibration, and state content remain in their contracted
    layers.
12. **TSV validity:** canonical headers, literal tabs, consistent column counts, and one-line rows are validated for
    every optional TSV output.
13. **Evidence authority:** map/project-calibration conflicts resolve in favor of observed source, with unresolved
    mismatch visible.
14. **State discipline:** map state survives fresh-session continuation without accumulating history or becoming a
    normal implementation startup read.
15. **Gate return:** subordinate mapping completes by reconciling state/context and returning to the refreshed
    invoking gate.

## Explicitly Unresolved Implementation Detail

The specification intentionally leaves the exact minimal source-identity metadata shape and automatic
dependency-to-map resolution mechanics to real multi-repository validation. The owning seam is established:
`skills/code_maps.md` plus `code_map.md` entry identity. Phase 1 does not invent a registry, schema, helper script,
or compatibility file to close that implementation detail.
