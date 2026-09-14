# Code Maps

## Purpose

Create, inspect, extend, refresh, rebuild, remove, and use selective generated source-navigation maps through
Bonsai's normal identity, menu, context, workspace, and human-gate model.

A **code map** is the primary user-facing mapping concept. A **map workspace** is the durable execution mechanism
used to create, extend, refresh, rebuild, and resume work on a code map. Normal code-map operations may create,
reuse, reactivate, resume, or update map workspace memory as needed; the human should not have to create a workspace first merely to
ask Bonsai to map the current source.

Generated maps describe actual source and are reusable navigation aids, not source authority, project truth,
workspace execution memory, or exhaustive documentation.

## When to Load

Load this skill only when:

- the human selects **Manage Code Maps**;
- an explicit startup request asks for a code-map action;
- current implementation needs map-guided navigation or map/source alignment checking;
- the human accepts a contextual first-use mapping action for substantial existing source;
- the human accepts a contextual recommendation to extend an existing map with newly valuable coverage; or
- the human accepts bounded refresh after a known material structural source change.

Do not load the editing workflow merely because a map exists, and do not treat routine source edits as map
maintenance. Ordinary map consumption reads `code_map.md` first and only the deeper artifact needed for the current
facet.

## Authority and Boundaries

Use these authorities in order:

1. actual selected source, including its build files, tests, examples, and representative uses;
2. approved project final truth and archaeological analysis as attention and interpretation context;
3. optional human-owned `map_calibration.md` as source-specific calibration;
4. existing map data as navigation memory that must remain aligned with source.

Project memory and `map_calibration.md` may guide where to look, but they do not prove source behavior or determine
map identity. When they disagree with observed source, source wins and the mismatch remains visible until corrected.

Do not require a Bonsai project or active project for source mapping. **Manage Code Maps** may be entered directly
from the repository entry gate before any project is selected. Do not create project memory merely to map source.
Do not put active project, phase, pass, approval, requirement-tracking, icebox, or session status into map workspace
memory or generated map data.

Normal user interaction should speak in code-map terms. Expose map-workspace lifecycle directly only when the
workspace itself is what the human intends to create, inspect, resume, or manage. Keep the workspace/output
distinction strict internally even when ordinary creation hides it.

## Map Workspace and Generated-Map Collections

Resolve two collections independently from the repository and Bonsai Home identity supplied by `start.md`:

- repository-local map workspaces: `<repository-home>/.bonsai/maps/`;
- reusable generated maps: the active map store described below.

Enumerate only immediate child directories of each collection, in stable lexical order. Keep the results as two
typed collections even when they contain the same name. A directory is a map-workspace candidate because it is an
immediate child of the repository-local workspace area; it is not valid until its workspace entry and required
execution memory pass validation. A directory is a usable generated map only when its agent-owned `code_map.md`
entry exists and is readable. The presence of one does not prove the presence or validity of the other.

In Embedded Bonsai, `<repository-home>/.bonsai/maps/<map>/` may be both the workspace directory and the generated-map
directory. Physical overlap does not merge ownership. Classify known files by role, not by their parent path:

```text
workspace.md                     # Repository-local workspace entry
agent_plan.md                    # Repository-local map roadmap
agent_state.md                   # Repository-local current resume state
map_calibration.md               # Optional human-owned workspace input
plan/agent_plan_<scope>.md       # Optional repository-local scoped plans
code_map.md                      # Generated-map entry
namespace_router.tsv             # Optional generated routing
manifest.tsv                     # Optional generated registry
symbol_index.tsv                 # Optional generated routing
subsystems/                      # Optional generated drill-down maps
```

Never treat workspace memory as generated output, generated output as execution memory, or an unknown colocated
file as owned merely because Embedded Bonsai makes the paths overlap.

## Active Generated-Map Store

Resolve the active map store from Bonsai Home and repository identity supplied by `start.md`; active project is
not required:

- when a configured Bonsai Home is active: `<bonsai-home>/maps/`;
- for Embedded Bonsai without a configured external home: `<repository-home>/.bonsai/maps/`.

Resolve that store independently from the source location. Mapping source in another repository, directory, or
archive does not place generated output beside that source by default.

Human-owned calibration is an input, not generated runtime map data. When the selected source is a repository
checkout, look for source-local calibration at:

```text
<source-repository>/.bonsai/maps/<source>/map_calibration.md
```

In Embedded Bonsai this source-local location may also be physically inside the active map store. Never move, copy,
normalize, or rewrite calibration merely because generated map artifacts are stored elsewhere.

Several projects may reuse one named source map, and one project may select several relevant source maps. Do not
duplicate a map per consuming project or treat the active project's name as the map identity.

Each named source map may contain:

```text
<map-store>/<source>/
    code_map.md                       # Required entry for a usable map
    namespace_router.tsv              # Optional fuller namespace routing
    manifest.tsv                      # Optional subsystem/path registry
    symbol_index.tsv                  # Optional selective symbol routing
    subsystems/<subsystem>/map.md
    subsystems/<subsystem>/api_pub.md # Optional caller mechanics
    subsystems/<subsystem>/api_ext.md # Optional extension mechanics
```

Write generated runtime map data only beneath the resolved active map store. Never instantiate a template back into
the Bonsai standard, write generated map data into a staged distribution, or treat a standard template as runtime
map state.

The named source directory is a storage boundary, not a blanket ownership boundary. Map lifecycle operations own
only agent-owned map artifacts they actually create or manage. They never own `map_calibration.md`, a supplied
source archive, source checkout, or another colocated file merely because it is under that directory.

## Manage Code Maps Entry

Retain the invoking Bonsai gate before doing anything else.

When the human enters **Manage Code Maps**, perform only cheap deterministic discovery needed to describe the
available choices:

- enumerate immediate repository-local map-workspace child directories;
- enumerate immediate active-map-store child directories;
- for generated-map discovery, check only whether each candidate has a readable `code_map.md`;
- do not read `code_map.md`, `workspace.md`, `agent_plan.md`, `agent_state.md`, calibration, source identity, or
  generated drill-down artifacts merely to render the menu.

Keep repository-local map-workspace candidates and reusable generated maps as two typed collections even when they
share names.

When useful, render a compact status summary such as:

```text
Available code maps: <stable lexical list or none>
Active project: <project or none>
Maps used by <project>: <selected usable maps or none>
Map workspaces: <count or stable lexical list when materially useful>
```

If available code-map names are already shown in status, do not offer a separate action whose only purpose is to
list those same names.

When no more specific action was requested, load `skills/menu.md` and present only applicable primary code-map
actions:

1. **Create Code Map**.
2. **Extend Code Map** when at least one usable generated map exists.
3. **Inspect Code Map** when at least one usable generated map exists.
4. **Refresh Code Map** when at least one usable generated map exists.
5. **Rebuild Code Map** when at least one usable generated map exists.
6. **Remove Code Map** when at least one usable generated map exists.
7. **Add a Code Map to the Active Project** when a valid active project exists and at least one usable generated
   map is not already selected by that project.
8. **Remove a Code Map from the Active Project** when a valid active project exists and at least one of its
   selections still identifies a usable generated map.
9. **Manage Map Workspaces**.
10. **Cancel and return to `<invoking gate>`**.

Omit unavailable actions rather than preserving fixed numbering.

The primary menu manages code maps. Map-workspace lifecycle is secondary and lives under **Manage Map Workspaces**.
Do not require the human to choose between **Create Map Workspace** and **Create Code Map** merely to map the
current source.

If an action needs source, identity, store, workspace, or project evidence that is not yet available, obtain that
evidence inside the selected action. Do not eagerly validate every candidate merely to annotate the menu.

### Manage Map Workspaces

This submenu exposes direct control of repository-local mapping execution memory for advanced, external-source,
calibration, inspection, and resume cases.

On entry, enumerate repository-local map-workspace candidates cheaply and show their names in stable lexical order.
Do not validate every candidate merely to render the submenu.

Present only applicable actions:

1. **Create Map Workspace**.
2. **Resume Map Workspace** when at least one repository-local candidate exists.
3. **Inspect Map Workspace** when at least one repository-local candidate exists.
4. **Cancel and return to Manage Code Maps**.

**Create Map Workspace** is explicit workspace lifecycle management. It is not a prerequisite for ordinary
**Create Code Map**.

For **Inspect Map Workspace**, select one candidate, validate only that candidate using the same workspace-entry,
plan, and state rules used by **Select or Resume a Map Workspace**, and report its source identity, current scope,
roadmap status, readiness, blocker, active scoped plan, and exact next step without mutation. Do not activate the
workspace merely because it was inspected.

After a non-mutating workspace inspection or cancellation, return to the refreshed **Manage Map Workspaces**
submenu. After explicit workspace creation, follow the creation rules below; after successful resume, the selected
map workspace becomes the active workspace for the session and replaces the prior parent gate.

### Add or Remove a Code Map from a Project

These actions manage a project's explicit selection of useful reusable maps. They are available only when the
invoking context supplies one active `project` workspace. Omit them at the repository entry gate and for an active
map workspace; do not ask the human to select or create a project merely to make an association action available.

Before offering either action:

1. Revalidate that the supplied project home is one immediate child of `<repository-home>/.bonsai/projects/` and
   that its readable `workspace.md` contains exactly one `Type: project` declaration and one
   `Route: Project workspace behavior` declaration.
2. Resolve the active generated-map store independently. A selectable map is one immediate child directory whose
   agent-owned `code_map.md` exists and is readable.
3. Load `skills/agent_context.md` and read only the selected project's `agent_context.md` when it exists. Treat its
   canonical `Useful code maps:` entries as project selections, not as proof that a generated map is currently
   usable.
4. For **Add**, list usable generated maps not already selected. For **Remove**, list only selected identities that
   are still usable generated maps. Keep choices in stable lexical order and accept the corresponding number.

Revalidate the selected project and map immediately before mutation. The map name must be one directory component,
and `<active-map-store>/<map>/code_map.md` must still be readable. A same-name repository-local map-workspace
candidate, its `workspace.md`, or its execution memory never establishes a valid association target. If the
project or generated-map identity is invalid, stale, ambiguous, or no longer usable, stop without changing context.

After the human selects the concrete add or remove operation, delegate only the canonical project-context mutation
to `skills/agent_context.md`. Report the project, generated-map identity, and exact project `agent_context.md`
target. The operation must not create, rebuild, move, rename, edit, or delete generated-map artifacts; modify a map
workspace; change project or map execution memory; or persist active workspace/session identity.

An already-present add and an already-absent remove are successful no-ops. After mutation or no-op, verify the
project selection and return to the refreshed **Manage Code Maps** entry through `skills/menu.md`. Association
maintenance does not activate the selected map, perform source inspection, or authorize another map lifecycle
action, except when the association was explicitly included in an approved **Create Code Map** action and is being
performed as that action's final post-creation step.

### Create Map Workspace

Runtime creation is an explicit map-workspace lifecycle action under **Manage Map Workspaces**, not the normal
prerequisite for **Create Code Map** and not the Web UI `prompts/create_map.md` design/calibration workflow.

Use this action when the human intentionally wants to establish mapping execution memory directly, including for an
external source or deliberately prepared mapping effort.

Require all of the following before proposing creation:

- a human-supplied, unused map-workspace name;
- the map-wide objective and an initial bounded mapping scope;
- the actual source's logical name, source type, exact location, and available snapshot evidence; and
- one safe initial exact next action, or the concrete missing evidence that must become a blocker.

The name must be one directory component. Reject an empty name, `.` or `..`, an absolute path, a drive prefix, path
separators, control characters, or any target outside `<repository-home>/.bonsai/maps/`. "Unused" means that no
valid or partial map workspace already owns that name; it does not mean that a same-name generated map cannot exist.

Preflight the exact target without mutation. If the target directory already exists, classify every existing item
needed for safety. Embedded overlap may make an existing same-name generated-map directory the correct physical
target. Permit creation there only when `workspace.md`, `agent_plan.md`, and `agent_state.md` are all absent and no
existing item makes ownership ambiguous. Preserve `code_map.md`, generated-map artifacts, `map_calibration.md`, and
every other colocated file unchanged. If any required workspace file already exists without a complete valid
workspace, classify the candidate as conflicting and stop; do not overwrite, complete, or repair it through
creation.

Before mutation, report the name, repository-local target, source identity, initial scope, exact three files to be
created, every known preserved colocated item, and whether the target overlaps the generated-map store. Load
`skills/menu.md`, offer creation of that exact workspace, revision, discussion, or cancellation, and stop for
explicit human confirmation.

After approval, create only:

```text
<repository-home>/.bonsai/maps/<map>/workspace.md
<repository-home>/.bonsai/maps/<map>/agent_plan.md
<repository-home>/.bonsai/maps/<map>/agent_state.md
```

Write `workspace.md` as the small declarative map entry with exactly one `Type: map` declaration and one
`Route: Map workspace behavior` declaration. Initialize `agent_plan.md` as a map-wide roadmap for the approved
objective and selected scope. Initialize `agent_state.md` as current map resume truth: current mapping scope,
source/map identity evidence, readiness, one exact next step or concrete blocker, success condition, and only
resume-critical files. Do not add project phases, passes, final-truth status, contract state, or an active-workspace
pointer. Set `Ready to execute` only when the recorded action has sufficient evidence and no independent gate;
otherwise record the concrete `Blocked` condition.

Do not create or modify `map_calibration.md`, `code_map.md`, generated lookup/drill-down artifacts, a scoped plan,
or a `plan/` directory as a side effect. If all three files cannot be created without changing a pre-existing item,
stop and report the partial result rather than claiming a valid workspace. Validate the completed workspace, then
activate it only in current-session context and follow **Select or Resume a Map Workspace** below.

### Select or Resume a Map Workspace

For **Resume Map Workspace**, list repository-local candidates in stable lexical order. When selection is required,
present numbered choices and accept the corresponding number. Inspect the selected candidate only; invalid
candidates remain visible but unavailable, with the concrete reason.

Validate the selected candidate in this order:

1. require a readable `workspace.md` containing exactly one unambiguous `Type: map` declaration and exactly one
   unambiguous `Route: Map workspace behavior` declaration;
2. require readable `agent_state.md` and `agent_plan.md`;
3. read state first and plan second, compare overlapping mapping scope, roadmap status, readiness, blocker,
   active scoped-plan identity, exact-next-step, and completion claims;
4. read one flat scoped plan under `plan/` only when state names it or it is required to establish the current
   mapping gate; reject an absent named plan or a path outside that workspace; and
5. classify a missing required file, conflicting common truth, unsafe exact step, or unsupported completion claim
   as `Blocked` rather than guessing or repairing it.

Do not read generated map output, project memory, or chat history to reconstruct missing workspace state. Load
`map_calibration.md`, actual source, generated output, developer context, or agent context only when the
reconstructed exact action requires that facet.

After validation, establish the selected name and home as the active `map` workspace in current-session context
only. Never persist an active-map pointer. Return the reconstructed condition to the implementation kernel as the
refreshed active-map gate; a compatible mapping action proceeds through this skill's active map behavior and shared
handoff, while a human gate or blocker stops there. A successful selection replaces the repository-entry gate for
this session. Cancellation, invalid selection, or non-mutating inspection returns to the retained invoking gate
through `skills/menu.md` unless it creates a concrete blocker that must be shown first.

## Active Map Workspace Execution

Use this path only after startup or **Resume Map Workspace** has established one valid active `map` workspace in
current-session context. The map workspace supplies continuation authority; the generated map does not.

### Derive one bounded action

1. Start from the already loaded repository-local `agent_state.md`, then `agent_plan.md`, and the one flat scoped
   plan named by state when applicable. Confirm that their overlapping mapping scope, roadmap status, active-plan
   identity and status, readiness, blockers, exact next step, and completion claims still agree.
2. Derive exactly one action from the narrowest applicable execution basis:
   - use the map-wide roadmap directly for a small bounded mapping unit;
   - use the active scoped plan for a larger mapping unit when state names it; or
   - make drafting or refining one scoped plan the exact action when the unit is too large to execute reliably
     from roadmap-level detail.
3. When the exact action is an executable mapping unit, require it to identify:
   - the current mapping scope;
   - the human-selected bounded mapping focus;
   - the source identity and location;
   - the normal generated-output envelope available to that mapping unit;
   - the observable success condition; and
   - any evidence, blocker, or independent human gate that must be resolved first.
4. Do not require the exact standard generated-map file set to be known before source discovery. Discovery is
   allowed to determine architectural ownership and the exact standard map layers needed to represent the selected
   focus.
5. Treat a missing or conflicting basis, an absent named plan, multiple plausible mapping focuses, a source/map
   identity mismatch, insufficient source evidence, or an ownership ambiguity that cannot safely be resolved from
   authoritative source as `Blocked`. Do not repair the gap from generated output, project memory, directory
   inference, or chat history.

A bounded mapping focus is the execution-authorization boundary for a mapping unit. It may be one architectural
subsystem, one caller or extension concern, a cross-cutting behavior, persistence, event handling, serialization,
lifecycle, tracking, or another bounded source-backed concern.

The selected focus does not have to correspond one-to-one with a generated subsystem.

For an ordinary non-destructive mapping unit, the normal generated-output envelope is:

```text
code_map.md
subsystems/<subsystem>/map.md
subsystems/<subsystem>/api_pub.md
subsystems/<subsystem>/api_ext.md
```

The mapping unit may ultimately require one subsystem, several existing subsystems, a newly justified subsystem,
or only part of that output set. The exact standard paths are discovery-resolved details inside the already
authorized focus.

Creating or materially expanding optional lookup or index artifacts such as `namespace_router.tsv`, `manifest.tsv`,
or `symbol_index.tsv` is not implicitly authorized by that standard envelope.

Map roadmap text is execution basis for a small unit only when state identifies one safe bounded mapping focus and
no independent decision gate remains. A scoped plan refines one map roadmap unit; it does not supersede the
map-wide roadmap or grant authority outside the selected focus or current mapping scope.

### Scoped map planning

Create or refine a scoped plan only when decomposition materially improves execution or resumption. Use one flat
file beneath the active workspace:

```text
plan/agent_plan_<scope>.md
```

The file records the bounded mapping objective, source/map identity relevant to that unit, selected mapping focus,
ordered mapping work, known or expected generated-output effects, validation, status, and the next useful
mapping-unit boundary. It does not need to predict the exact standard generated-map files that source discovery
will justify.

Keep `agent_plan.md` roadmap-level and make `agent_state.md` name the active scoped plan and its exact next action.
A still-larger later unit may use another flat peer plan; do not create nested plan directories or reinterpret a
scoped plan as a project phase.

Creating or refining agent-owned map planning does not automatically require project-style plan approval,
contract review, or final-truth review. Stop for human direction only when the planning work changes the selected
mapping focus or current mapping scope, requires a materially different source or map identity, proposes
destructive work, requires restructuring existing generated-map ownership, adds a costly optional artifact, or
reaches another decision that genuinely requires authorization.

When planning itself is the exact next action, its continuation authorization ends when that planning action is
complete. Once durable state instead establishes one executable bounded mapping unit, continuation authorization
for that action covers the complete mapping unit described below.

### Apply mapping gates

Before beginning an executable mapping unit, apply the **Mapping Proposal Gate** unless the selected bounded
mapping focus has already been explicitly established and the current-session or fresh-session continuation
authorizes that same reconstructed mapping unit.

For an ordinary bounded mapping unit, authorization is based on the selected focus, source identity, map identity,
current mapping scope, and normal generated-output envelope. It does not require advance approval of each exact
standard Markdown target that discovery may select inside that envelope.

A current-session or fresh-session continuation of an executable mapping unit authorizes the complete unit:

```text
selected bounded mapping focus
        ↓
inspect authoritative source
        ↓
determine architectural ownership
        ↓
determine justified standard map layers
        ↓
create or update those standard layers
        ↓
validate against source
        ↓
reconcile workspace execution memory
        ↓
stop at the next mapping-unit boundary
```

Do not introduce a routine human gate between source discovery and generated-map production.

Always stop for human direction when the work requires:

- material expansion of the selected mapping focus or current source scope;
- a materially different source or map identity;
- unresolved source/map alignment;
- a destructive rebuild or removal;
- restructuring existing generated-map ownership rather than ordinary representation of the selected focus;
- a genuinely unrelated new mapping objective;
- creation or material expansion of an optional lookup or index artifact;
- another costly optional artifact;
- insufficient source evidence to map the selected focus safely; or
- another material decision that genuinely requires human authorization.

Do not stop merely because discovery determines that:

- different standard map files are needed than could be predicted before inspection;
- one cross-cutting focus belongs in several existing subsystem maps;
- `api_pub.md` or `api_ext.md` is justified;
- a new subsystem map is justified by the selected focus; or
- no standalone subsystem corresponds to the selected focus.

A fresh-session auto-execute request still authorizes only the one exact action reconstructed from current
workspace memory. For executable mapping work, that exact action is the complete bounded mapping unit, not a
discovery-only substep. It never authorizes the next mapping unit or bypasses a real gate or blocker.

### Execute the authorized mapping unit

1. Resolve the repository-local workspace, authoritative source, and active generated-map store independently.
2. Inspect actual source as needed to answer the selected bounded mapping focus. Use build structure,
   representative implementation, tests, examples, and call sites only as needed for that focus.
3. Recheck source/map identity while inspecting. A mismatch or insufficient alignment evidence stops generated
   output changes until the applicable identity gate resolves it.
4. Determine from authoritative source where the durable knowledge belongs. Resolve the exact standard
   generated-map targets only after enough discovery exists to establish architectural ownership.
5. Create or update the justified standard targets inside the authorized output envelope:
   - `code_map.md` when source identity, top-level orientation, or routing is affected;
   - `subsystems/<subsystem>/map.md` for each architectural domain needed to represent the focus;
   - `api_pub.md` when the focus reveals reusable non-obvious caller mechanics;
   - `api_ext.md` when the focus reveals reusable non-obvious extension mechanics.
6. Preserve `workspace.md`, `agent_plan.md`, `agent_state.md`, `map_calibration.md`, `plan/`, supplied source, and
   unknown colocated files from generated-output mutation even when Embedded Bonsai makes workspace and output
   paths overlap.
7. Do not create or materially expand optional lookup or index artifacts without their required authorization.
   Existing optional lookup data may receive only bounded maintenance necessary to keep already-authorized,
   already-present routing correct.
8. Validate all changed generated output against the source evidence and the applicable completion checks below.
9. If discovery materially escapes the selected focus, source scope, map/source identity, or normal output
   envelope, stop at the applicable human gate. Do not reinterpret such an escape as part of the existing
   authorization.
10. When the complete mapping unit has been generated and validated, delegate reconciliation to
    `skills/handoff.md`.

Do not delegate to handoff merely because discovery has finished and the exact standard target files have become
known. Discovery, ownership resolution, standard generated-map mutation, and validation normally remain one
authorized mapping unit.

### Reconcile mapping-unit completion and reactivation

Through the map branch of `skills/handoff.md`, reconcile the completed mapping unit against the map-wide roadmap,
active scoped plan when present, `agent_state.md`, actual source/map identity, changed generated output, and
performed checks.

- Mark the completed mapping focus and its generated-output effects accurately in the applicable roadmap or scoped
  plan.
- If the current mapping scope still contains useful work but no next bounded focus has yet been selected, present
  concrete next-focus choices and stop for human direction. Do not silently choose and execute another focus.
- When the human selects the next bounded focus, reconcile that selection into `agent_plan.md`, `agent_state.md`,
  and the active scoped plan when applicable. Leave generated output unchanged while doing so.
- Once the selected focus has become one safe exact mapping unit with an observable success condition and no
  independent gate, record it as ready and offer current-session continuation, fresh-session continuation,
  review/change, and **Exit for now** through the shared handoff behavior.
- When a scoped plan is exhausted, mark it complete and return control to the map-wide roadmap without turning
  scoped-plan completion into a project phase transition.
- Set `Execution Readiness: Complete` only when the current selected mapping scope has no unfinished roadmap or
  scoped-plan work and generated output is sufficiently reconciled with the selected source identity for that
  scope.
- A later observed source change, explicit maintenance request, expanded mapping scope, or newly discovered map
  need may reactivate the same workspace. Leave prior generated output in place until a newly authorized mapping
  unit changes it.

Map reconciliation never writes project phases, passes, contract state, project final-truth status, project
icebox state, active-workspace identity, or session history into map memory.

## Resolve the Mapping Context

Before proposing substantive mapping work, resolve only enough context to make the selected action and gate
trustworthy:

1. Retain the invoking Bonsai workflow or gate so this subordinate workflow can return to it. The invoking gate
   may be the repository entry gate with no active project.
2. Resolve the active map store without creating or modifying it.
3. Resolve the requested generated-map lifecycle action. If none was supplied, return to the **Manage Code Maps**
   entry menu above.
4. Identify the actual source independently from the active project:
   - logical source name;
   - source type, such as repository checkout, released source archive, or supplied source tree;
   - exact source location;
   - version, Git revision, artifact coordinate, checksum, or other smallest useful snapshot evidence.
5. For **Create Code Map**, **Extend Code Map**, and **Refresh Code Map**, prefer established current-session
   context over asking the human to restate it:
   - when the current repository is the intended source, default the source location to `<repository-home>`;
   - when repository identity is unambiguous, derive the logical source name from that repository/source identity;
   - when the active project clearly supplies useful mapping calibration, use it without making the project the map
     identity;
   - when a known structural source change already establishes a bounded refresh concern, carry that evidence into
     the refresh proposal rather than rediscovering the whole source merely to name the focus;
   - when project association is obviously intended for a newly created map, propose it as a post-creation
     association rather than making it a map-identity requirement.
6. Resolve the proposed map identity from the source universe, not the consuming project. Never silently choose
   among several plausible source identities or snapshots.
7. Inspect only the named map entry or directory metadata needed to determine whether the generated map exists,
   whether its identity aligns, and which known files are map-owned. A colocated non-map file does not prove a map
   exists.
8. Resolve or identify the corresponding repository-local map workspace independently. A same-name generated map
   does not prove workspace validity, and a same-name workspace does not prove a usable generated map.
9. Resolve source-specific calibration only when it can materially improve the selected action. For a repository
   checkout, check `<source-repository>/.bonsai/maps/<source>/map_calibration.md`. Use another calibration location
   only when the human explicitly supplied it for the selected source.
10. Read relevant project memory only when an active project exists and that memory can materially calibrate the
    selected action. Absence of active project is not an ambiguity or blocker for mapping.
11. Load `skills/agent_context.md` only when stable source locations, relevant map selection, or another qualifying
    operational rule may need to be applied or maintained.

If the source location, map store, map identity, source snapshot, or ownership boundary remains materially
ambiguous, stop and ask the human to resolve only that ambiguity. Do not invent a source resolver, downloader,
registry, manifest schema, dependency-to-map matcher, or source-location convention.

If **Create Code Map** resolves to an existing usable `code_map.md`, do not overwrite it as creation. Offer
**Extend Code Map**, **Refresh Code Map**, a separately gated **Rebuild Code Map**, or a distinct source identity as
appropriate.

## Lifecycle Intent Boundaries

Treat create, extend, refresh, and rebuild as distinct lifecycle intents even though their executable source-backed
work ultimately uses the same bounded mapping-unit model.

- **Create** establishes a suitable reusable map for a source identity that does not yet have one.
- **Extend** broadens the useful mapping scope of an existing map. The human may name a subsystem, a cross-cutting
  concern, a caller or extension surface, or another bounded source-backed concern. A requested subsystem is a
  mapping focus, not a command to create a same-named generated subsystem.
- **Refresh** reconciles existing mapped knowledge after represented source changes materially. It preserves the
  intended map identity and existing coverage where possible and targets the bounded mapped concern made stale by
  the change.
- **Rebuild** replaces substantial generated representation or performs broad ownership restructuring. It remains
  separately and explicitly gated because it is materially more destructive than extension or refresh.

A completed map is complete only for its current mapping scope and represented source state. Completion does not
prevent later extension or refresh from reactivating the same compatible map workspace.

Do not disguise scope expansion as refresh. When new reusable coverage is desired beyond the map's prior intended
scope, use **Extend Code Map**. Do not disguise broad replacement or ownership restructuring as extension or
refresh; use the separately gated rebuild path.

## Mapping Proposal Gate

Whenever **Active Map Workspace Execution** requires this gate, and for any generated-map lifecycle action not
already validly authorized through continuation of one selected mapping unit, present this information before
substantive source inspection or mutation:

- **Action:** selected lifecycle action or bounded mapping unit;
- **Source:** logical name, type, location, and available snapshot identity;
- **Map identity:** selected named source map;
- **Map workspace:** existing compatible workspace to reuse, exact new repository-local workspace to create, or
  `Not required` for a read-only/non-workspace action;
- **Map store:** resolved generated-map store;
- **Mapping focus:** the bounded source-backed concern being authorized;
- **Generated-output envelope:** the standard Markdown map layers available to represent that focus, plus any
  separately proposed optional or destructive targets;
- **Project association:** active project to add after a usable map exists, `None`, or `Not applicable`;
- **Alignment:** `Aligned`, `Mismatch`, `Insufficient evidence`, or `Not applicable for new map`;
- **Inputs:** actual source plus any project or human calibration that will be consulted;
- **Success condition:** the observable condition that completes this mapping unit;
- **Risks / uncertainties:** only those that can change the proposed unit or require another human decision.

Known likely standard targets may be shown when useful, but they are not a required pre-discovery contract.

Load `skills/menu.md` and offer concrete choices to select or revise the mapping focus, discuss a material
ambiguity, cancel, or otherwise resolve the applicable gate. Wait for explicit human direction.

Approval establishes the displayed source, map identity, workspace disposition, project-association choice,
mapping focus, current source/mapping scope, and normal generated-output envelope. When **Create Code Map** shows
creation of the corresponding map workspace, that workspace creation is part of the approved code-map action and
must not trigger a second standalone workspace-creation gate.

Approval does not authorize a later destructive rebuild, removal, material scope expansion, materially different
source/map identity, generated-map ownership restructuring, source mutation, costly optional artifact, or creation
or material expansion of an optional lookup/index artifact.

When the current mapping scope is already complete, say so and do not invent another objective merely to continue.

## Map and Source Alignment

`code_map.md` is the normal identity and routing entry. Use the smallest available evidence that prevents an
incompatible snapshot from being silently trusted.

Classify alignment as:

- **Aligned:** the map identity and selected source snapshot agree sufficiently for the intended use;
- **Mismatch:** available evidence shows a different version, revision, coordinate, source type, or artifact;
- **Insufficient evidence:** alignment cannot be established for a non-obvious claim;
- **Not applicable for new map:** no prior entry exists and creation will record identity from observed source.

On mismatch or insufficient evidence, do not rely on non-obvious map claims. Present concrete choices to inspect
the source, update the existing map, request a gated rebuild, select another map, select another source, or stop.
Do not assume an active development checkout matches a released dependency.

## Action: Create Code Map

**Create Code Map** is the normal user-facing creation path.

After the proposal is approved:

1. Resolve the approved corresponding map workspace before generated output:
   - when a compatible same-name workspace already exists, validate and reuse it;
   - when no workspace files exist at the approved repository-local target, create the workspace automatically;
   - when a partial, invalid, incompatible, or ownership-ambiguous workspace exists, stop without generated-output
     mutation.
2. Automatic workspace creation writes only:

   ```text
   <repository-home>/.bonsai/maps/<map>/workspace.md
   <repository-home>/.bonsai/maps/<map>/agent_plan.md
   <repository-home>/.bonsai/maps/<map>/agent_state.md
   ```

   Preserve every existing colocated generated artifact, calibration file, source input, and unknown file. Use the
   same ownership and overlap safety rules as **Create Map Workspace**, but do not require a separate human-supplied
   workspace objective, scope, or source identity when the approved code-map proposal already establishes them.
3. Initialize the automatically created workspace from the approved code-map proposal:
   - map objective: create and maintain reusable navigation knowledge for the selected source;
   - current mapping scope: the approved bounded creation scope;
   - selected mapping focus: the approved initial bounded focus;
   - source identity: the approved logical source, type, exact location, and available snapshot evidence;
   - roadmap: one bounded active initial mapping unit plus only justified pending work;
   - state: one safe exact next mapping unit, success condition, blockers, and `Ready to execute` only when evidence
     is sufficient.
   Do not create `map_calibration.md`, a scoped plan, or `plan/` as a side effect.
4. Establish the validated or newly created map workspace as the active `map` workspace in current-session context
   only. Do not persist an active-map pointer.
5. Treat the approved initial mapping focus as the authorization boundary. Do not require its exact standard
   generated-map targets to be known before discovery.
6. Inspect actual source for orientation and then for the selected focus. Use build structure, representative
   source, tests, examples, and call sites only as needed for that mapping unit.
7. Treat relevant project truth and applicable `map_calibration.md` as calibration, not source proof. Preserve
   material disagreements as uncertainty.
8. Preserve every pre-existing human-owned or otherwise unowned file, including calibration or supplied source
   physically colocated with the target map. Treat source-local calibration outside the active map store as
   read-only input.
9. Use discovery to determine the exact standard generated-map layers needed to represent the approved initial
   focus.
10. Instantiate or update only justified standard Markdown artifacts from `<bonsai-home>/templates/`:
    - `code_map_template.md` for the required entry when needed;
    - `subsystem_map_template.md` for each architectural subsystem justified by the focus;
    - `api_pub_template.md` and `api_ext_template.md` when non-obvious reusable mechanics discovered within the
      focus justify them.
11. Do not create `namespace_router.tsv`, `manifest.tsv`, or `symbol_index.tsv` merely because discovery suggests
    they could be useful. Creating or materially expanding optional lookup/index output requires its applicable
    explicit authorization.
12. Record the logical source and the smallest useful snapshot identity in `code_map.md`. Keep drill-down links
    relative to the named source map.
13. Complete all standard map effects of the selected initial focus before selecting another mapping focus. The
    focus may legitimately affect one subsystem, several subsystems, or no standalone subsystem of the same name.
14. When apparent design and actual use may differ, check at least one representative production use, test,
    example, call site, or extension before recording the mechanic as durable.
15. Validate the completed mapping unit under the structural and completion rules below.
16. If the approved proposal included adding the completed map to an active project, perform that association only
    after `<active-map-store>/<map>/code_map.md` is usable. Delegate the canonical project-context mutation to
    `skills/agent_context.md`; do not make association a condition for map identity or workspace validity.
17. Reconcile the completed bounded mapping unit through `skills/handoff.md`. Do not continue into another mapping
    unit under the same authorization.

Creating a map store or named source directory after approval does not transfer ownership of existing contents.
Template presence never authorizes optional output.

Before creating a costly optional artifact or materially expanding an optional index, show why its repeated
navigation value exceeds its maintenance cost, identify the exact output and scope, and stop for explicit human
approval.

## Action: Extend Code Map

Use **Extend Code Map** when the human wants useful new coverage in an existing compatible map.

1. Select or resolve the usable generated map and its corresponding repository-local map workspace independently.
2. Validate map/source alignment before relying on non-obvious existing map claims. A materially incompatible
   source identity stops extension until the identity issue is resolved.
3. Reuse and reactivate the existing compatible map workspace. Do not create a duplicate map merely because new
   coverage is requested.
4. Establish one bounded extension focus. The human may:
   - name an architectural subsystem;
   - name a cross-cutting concern such as persistence, event handling, serialization, lifecycle, or tracking;
   - name a reusable caller or extension concern; or
   - explicitly ask Bonsai to review current map coverage and suggest valuable additions.
5. When the human asks for suggestions, inspect the existing map only enough to understand current coverage, then
   inspect authoritative source only as needed to identify a small number of high-value missing concerns. Prefer
   foundational, reused, cross-boundary, risky, or repeatedly non-obvious knowledge. Do not turn suggestion mode
   into an exhaustive source survey.
6. Present the selected or proposed bounded focus through the **Mapping Proposal Gate**. Existing generated output
   remains unchanged until the focus is authorized.
7. After authorization, treat the selected focus as the mapping-unit boundary. Discovery may determine that the
   durable result belongs in one subsystem, several existing subsystems, a newly justified subsystem, or no
   standalone subsystem with the focus's name.
8. Preserve existing generated output outside the authorized focus. Ordinary extension may add or update justified
   standard Markdown layers, but it does not authorize destructive replacement, broad ownership restructuring, or
   optional-index creation or material expansion.
9. Validate the complete mapping unit and reconcile the reactivated map workspace through `skills/handoff.md`.
   Do not select another extension focus under the same authorization.

A contextual implementation recommendation to preserve newly discovered reusable knowledge enters this same
action when a compatible map already exists. The recommendation supplies evidence for a candidate focus; it does
not bypass the mapping proposal or map/source alignment rules.

## Action: Inspect Code Map

Inspection is read-only.

1. When no map was named by the human, present the already-discovered usable code-map names in stable lexical
   order only as the selection for this inspection; do not rescan or pre-read every map.
2. Load the selected map's `code_map.md` first.
3. When source-dependent claims or identity matter, resolve the selected source and classify map/source alignment.
4. Load only the subsystem, API, namespace, manifest, symbol, or identity facet needed for the inspection question.
5. Use actual source to verify non-obvious behavior; report map claims as navigation, not authority.
6. Report missing, stale, mismatched, uncertain, or malformed data without changing it.

Inspection does not normalize existing files, update identity metadata, or preserve context unless the human
separately authorizes the applicable action. An explicit **Inspect Map/Source Identity** request is handled as this
same read-only inspection path with identity/alignment as the selected facet.

## Action: Refresh Code Map

Use **Refresh Code Map** when represented source changed materially and existing mapped knowledge needs to be
reconciled without broad destructive replacement.

A refresh may be requested directly by the human or may originate from a contextual maintenance recommendation
after authorized project work changed source represented by a known relevant map.

1. Select or resolve the usable generated map, represented source, and corresponding repository-local map workspace.
2. Establish the bounded mapped concern affected by the source change. Reuse concrete change evidence already
   available from the invoking implementation workflow when trustworthy; do not rescan unrelated source merely to
   rediscover why maintenance was proposed.
3. Verify map/source identity and classify alignment. Expected source drift caused by the known change is the reason
   to refresh, not permission to trust unrelated stale map claims.
4. Reuse and reactivate the compatible existing map workspace and present the bounded refresh focus through the
   **Mapping Proposal Gate** unless that same focus has already been explicitly established and authorized through
   normal active-map continuation.
5. Treat the refresh focus as the authorization boundary. Discovery may determine which standard Markdown map
   layers inside that focus require changes.
6. Improve justified existing artifacts in place and update standard map-owned artifacts whose durable content
   changed. Preserve established ownership and structure unless restructuring was separately authorized.
7. Update already-present dependent lookup artifacts only when bounded maintenance is necessary to keep their
   contracted routing correct. Do not create or materially expand optional lookup/index artifacts without their
   separate gate.
8. Re-check representative usage when caller, extension, lifecycle, ownership, persistence, serialization, event,
   tracking, or similar reusable mechanics changed.
9. Validate and reconcile the complete refresh mapping unit before selecting another focus.

Routine bug fixes, private refactors, tests, cosmetic cleanup, and ordinary churn do not justify refresh by
themselves. Bonsai does not continuously scan for drift or silently refresh maps after source changes.

If the required work materially broadens useful coverage beyond the prior map scope, stop and route that portion
through **Extend Code Map**. If safe reconciliation requires substantial replacement, destructive removal, or broad
generated-map ownership restructuring, stop and route through **Rebuild Code Map**.

## Action: Rebuild Code Map

A rebuild intentionally replaces substantial generated representation and always requires its own explicit gate.
Selecting **Rebuild Code Map** or arriving there from another lifecycle action does not itself authorize mutation.

Before that gate:

1. resolve and display every existing agent-owned target that would be replaced or removed;
2. display every known preserved item in the target map, including `map_calibration.md`, supplied source inputs, and
   other unowned files;
3. show the source snapshot, map identity, rebuild scope, proposed replacement artifacts, ownership changes when
   any, and validation plan; and
4. stop for explicit approval, revision, discussion, or cancellation.

After approval, replace only the displayed agent-owned targets. Never delete the named source directory as a
shortcut. Never move, rename, modify, or delete a supplied source artifact. If safe replacement cannot be completed
within the approved target set, stop with the existing unowned content preserved.

## Action: Remove Code Map

Removal is destructive and always requires its own explicit gate.

Before the gate:

1. inspect the selected named map without mutation;
2. resolve the exact agent-owned artifact paths proposed for removal;
3. distinguish and list preserved human-owned calibration, supplied source inputs, and other unowned files;
4. report ambiguity rather than claiming ownership from directory location; and
5. show the exact verification that will confirm preserved files remain unchanged.

Load `skills/menu.md` and offer approval of the exact removal target set, revision of that set, discussion, or
cancellation and return. Stop for explicit approval.

After approval, remove only the displayed map-owned artifacts. Do not recursively delete the named source
directory. Verify the preserved target set still exists and that no transient inspection data entered the durable
map store. Report the map removed only when no usable agent-owned `code_map.md` remains for that selected map.

## Action: Inspect Map/Source Identity

This action is read-only.

1. read the selected map's identity from `code_map.md`;
2. inspect the selected source only enough to establish its logical and snapshot identity;
3. keep source location, source identity, map identity, consuming project, and map-store location distinct;
4. classify alignment using this skill's alignment states; and
5. report the evidence, uncertainty, and safe follow-up choices.

Do not write identity metadata merely to make inspection conclusive. If richer universal metadata or automatic
resolution appears necessary, report that as a design question instead of inventing a registry or schema.

## Mapping and Editing Rules

### Layer responsibilities

- `code_map.md`: compact source identity, orientation, and drill-down routing.
- `subsystems/<subsystem>/map.md`: one durable architectural domain, not a folder or module inventory.
- `api_pub.md`: optional decision-ready caller mechanics.
- `api_ext.md`: optional decision-ready extension mechanics.
- `namespace_router.tsv`: optional fuller namespace ownership routing.
- `manifest.tsv`: optional compact subsystem/path registry, never the sole identity proof.
- `symbol_index.tsv`: optional selective high-value symbol routing, never an exhaustive index.

Repository-local `agent_plan.md`, `agent_state.md`, and scoped plans own mapping continuation. They are not another
generated-map layer.

Do not duplicate one layer in another. Prefer durable navigation and recurring non-obvious mechanics over source
extraction. Smaller reusable memory is better than a comprehensive-looking map.

### Mapping focus and subsystem ownership

A generated subsystem must represent a demonstrated architectural responsibility, ownership boundary, lifecycle,
data or execution concern, reusable API/extension surface, or other durable architectural domain. A directory,
module, source root, package group, or human-selected mapping focus is evidence, not automatically a subsystem.

A bounded mapping focus is a unit of work, not necessarily a generated-map ownership boundary.

A focus may concern:

- one architectural subsystem;
- one caller or extension surface;
- a cross-cutting behavior;
- persistence;
- event handling;
- serialization;
- lifecycle;
- tracking; or
- another bounded source-backed concern.

Discovery determines which generated architectural domains own the resulting durable knowledge. One focus may
therefore update one subsystem, several existing subsystems, or a newly justified subsystem, and may determine that
no standalone subsystem corresponding to the focus should exist.

Prioritize owner-weighted, foundational, developer-facing, cross-boundary, widely reused, risky, or repeatedly
misunderstood concerns. Deprioritize generated code, narrow helpers, leaf utilities, shallow inventories, obvious
details, and non-representative examples.

Complete the selected mapping focus, including all standard architecture and API-map effects directly justified by
that focus, before selecting another focus. Do not force unrelated caller or extension analysis merely because an
affected subsystem has other surfaces.

A new human-selected mapping focus or material scope expansion requires human direction. A newly justified
subsystem or API map discovered while representing the already-selected focus does not by itself require another
gate.

Fresh-session boundaries should normally occur between bounded mapping units. When a mapping unit accumulates
enough context to reduce confidence or compression quality, finish and reconcile that unit when practical before
moving to the next focus. Do not deliberately split discovery from standard generated-map production merely to
create a session boundary.

### Evidence discipline

Use these labels when a non-obvious claim's status matters:

- **Observed:** confirmed directly from source, tests, examples, build files, or representative use;
- **Inferred:** reasoned from observed structure but not directly established;
- **Uncertain:** requires verification before reliance.

Do not overstate confidence. Correct stale map content when authorized; otherwise make the mismatch or uncertainty
visible.

### TSV discipline

For `namespace_router.tsv`, `manifest.tsv`, and `symbol_index.tsv`:

1. preserve the canonical header and column order;
2. use literal tab characters between fixed columns;
3. keep one logical record per physical line;
4. use no multiline cells, ad hoc columns, prose blocks, or tabs/newlines inside cell values;
5. keep notes terse; and
6. validate the header, separators, and consistent column count after material edits.

Move detail that does not fit the fixed shape into the appropriate Markdown layer.

### Compression and drift prevention

When an artifact grows, cut before adding:

- keep `code_map.md` startup-sized and move fuller namespace routing to its optional TSV;
- keep subsystem maps architectural rather than exhaustive;
- keep API maps focused on mechanics that prevent recurring mistakes;
- keep lookup tables selective and structurally boring; and
- remove duplicated, stale, wrong-layer, obvious, or low-value content.

Do not structurally normalize an existing map during routine maintenance. Do not create optional artifacts because
a template exists. Do not turn maps into project/session guides, API manuals, filesystem mirrors, prose indexes,
or hand-maintained language-server databases.

## Agent Context During Mapping

Use `skills/agent_context.md` only for qualifying durable operational facts, such as a stable source checkout
location, an established source-selection rule, or a reusable project-to-map association.

Do not store active-project selection, active-map selection, transient extraction paths, one-run inspection
locations, speculative source identity, map workflow state, or map content in agent context. Context maintenance
grants no permission to broaden the mapping action.

## Contextual First Use, Extension, and Refresh

Project implementation may surface code-map work at a natural boundary, but it must not silently mutate reusable
maps or expand source inspection merely to search for mapping opportunities.

### First useful map

- A substantial existing source without a useful map may receive one contextual **Create Code Map** action.
- If the human declines, return that result to the invoking workflow so creation moves under **See more options**
  rather than interrupting again in the same context. Do not create a placeholder map or state file for a decline.
- Greenfield source with little stable structure receives no map pressure.

### Mapping opportunity discovered during project work

When authorized project work already required source inspection and that inspection established reusable,
non-obvious, architecturally significant knowledge that is not adequately represented by a useful map, Bonsai may
recommend preserving it as code-map coverage.

- If no suitable map exists, recommend **Create Code Map**.
- If a compatible map exists but lacks the concern, recommend **Extend Code Map** with one bounded candidate focus.
- Explain the implicated source or map, proposed focus, what reusable knowledge was costly or non-obvious to
  establish, and why it is useful beyond the current project.
- Base the recommendation only on evidence encountered for the authorized project work. Do not inspect unrelated
  source to manufacture recommendations.
- Closely related observations should become one recommendation rather than several interruptions.
- A recommendation does not create or mutate a map, reactivate a workspace, or change project execution scope until
  the human accepts it.
- If declined or deferred, return that disposition to the invoking workflow and do not repeatedly resurface the
  same recommendation during the same work merely because it remains possible.

### Known map maintenance after source change

When authorized project work materially changed source represented by a known relevant map and the existing map
coverage is now affected, Bonsai may recommend **Refresh Code Map**.

A known relevant map is one already selected for the project, already loaded or used by the current work, or cheaply
identifiable from the current source identity without surveying the entire map store.

- Carry the known source-change evidence and bounded affected concern into the refresh proposal.
- Do not enumerate and inspect every reusable map after routine source edits.
- Routine local edits, narrow bug fixes, private refactors, formatting, tests, and other changes that do not
  materially alter mapped knowledge do not trigger refresh.
- The recommendation itself does not authorize map mutation. Accepted maintenance enters the normal refresh action
  and bounded mapping-unit workflow.

Preserve a longer-lived source or selection rule only when it independently qualifies under
`skills/agent_context.md`.

## Transient Source Inspection

Inspect a supplied archive directly when practical. If extraction or another inspection area is needed:

- keep it outside the durable map store;
- treat it as disposable and non-authoritative working state;
- do not copy it into a project merely to enable mapping;
- do not preserve it in agent context or map data; and
- remove or abandon it without modifying the supplied source artifact.

The physical location of one supplied archive never establishes a general source-location convention. Create,
update, rebuild, and removal preserve that archive even when it is colocated with map artifacts.

## Completion Checks

Before reporting an authorized mapping unit or mapping scope complete:

1. verify `code_map.md` identifies the source sufficiently for intended alignment and remains compact;
2. verify entry, subsystem, API, calibration, state, and lookup content stays in its contracted layer;
3. verify every subsystem created or updated by the work has a demonstrated architectural responsibility and
   source-backed owning paths;
4. verify the standard architecture or API layers directly implicated by the selected mapping focus were created,
   updated, or deliberately found unnecessary;
5. verify non-obvious claims are source-backed or visibly inferred/uncertain;
6. verify relative links and optional-artifact references match files that actually exist;
7. validate every materially edited TSV header, literal-tab separator, fixed column count, and one-line row;
8. verify every generated-map mutation was either inside the selected focus's standard output envelope or
   separately authorized;
9. verify no destructive work, ownership restructuring, optional-index creation, or material optional-index
   expansion occurred without its required gate;
10. verify supplied source, every consulted `map_calibration.md`, and other unowned files remain unchanged;
11. verify no transient inspection became durable map data;
12. reconcile the map-wide roadmap, active scoped plan when present, and current resume state through shared
    handoff; and
13. maintain only qualifying agent context through `skills/agent_context.md`.

Completing source discovery alone does not complete an executable mapping unit when justified standard
generated-map updates remain.

If the current mapping scope has no real next focus or other required work, mark it complete rather than inventing
more mapping work.

## Completion and Invoking-Gate Return

At completion of substantive work for an active map workspace:

1. report the mapping unit, source, map identity, bounded result, changed map-owned files, checks actually
   performed, preserved unowned files, remaining uncertainty, and whether qualifying agent context changed;
2. reconcile repository-local `agent_plan.md`, `agent_state.md`, any active scoped plan, generated output, and
   source/map identity through `skills/handoff.md`; reconcile qualifying agent context when applicable;
3. do not silently revise human-owned `map_calibration.md`, project final truth, or project execution memory;
4. let shared handoff derive and present the refreshed active-map completion, blocker, next-focus selection, or
   continuation gate; and
5. do not also restore the older repository-entry or **Manage Code Maps** gate after active workspace execution.

For cancellation, a declined contextual offer, or non-mutating inspection that did not complete an active map
workspace exact action, return control to the retained invoking workflow. When an active project exists, let its
owning workflow reconcile project execution state; when none exists, do not manufacture project state. Load
`skills/menu.md` and re-present that refreshed invoking gate unless the mapping action created a new required
blocker, design, final-truth, or review gate.

Do not silently end the parent workflow because mapping completed or was cancelled. Do not silently select or
execute a new mapping focus. A completed unit may surface concrete next-focus choices, but the human selects the
next focus before another mapping unit becomes authorized.

## Output Style

Use concise wording, exact paths, stable headings, explicit uncertainty, and no filler. Distinguish observed facts
from inference. Do not claim a source, map, identity, mutation, removal, or check that was not actually inspected or
performed.
