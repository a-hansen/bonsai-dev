# Code Maps

## Purpose

Create, inspect, update, rebuild, remove, and use selective generated source-navigation maps through Bonsai's normal
identity, menu, context, workspace, and human-gate model.

A **code map** is the primary user-facing mapping concept. A **map workspace** is the durable execution mechanism
used to create, maintain, rebuild, and resume work on a code map. Normal code-map operations may create, reuse,
resume, or update map workspace memory as needed; the human should not have to create a workspace first merely to
ask Bonsai to map the current source.

Generated maps describe actual source and are reusable navigation aids, not source authority, project truth,
workspace execution memory, or exhaustive documentation.

## When to Load

Load this skill only when:

- the human selects **Manage Code Maps**;
- an explicit startup request asks for a code-map action;
- current implementation needs map-guided navigation or map/source alignment checking;
- the human accepts a contextual first-use mapping action for substantial existing source; or
- the human accepts bounded maintenance after a known material structural source change.

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
2. **Inspect Code Map** when at least one usable generated map exists.
3. **Update or Rebuild Code Map** when at least one usable generated map exists.
4. **Remove Code Map** when at least one usable generated map exists.
5. **Add a Code Map to the Active Project** when a valid active project exists and at least one usable generated
   map is not already selected by that project.
6. **Remove a Code Map from the Active Project** when a valid active project exists and at least one of its
   selections still identifies a usable generated map.
7. **Manage Map Workspaces**.
8. **Cancel and return to `<invoking gate>`**.

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

Do not read `map_state.md`, generated map output, project memory, or chat history to reconstruct missing workspace
state. Load `map_calibration.md`, actual source, generated output, developer context, or agent context only when the
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
   - use the active scoped plan for a larger unit when state names it; or
   - make drafting or refining one scoped plan the exact action when the unit is too large to execute reliably
     from roadmap-level detail.
3. Require the exact action to identify its selected mapping scope, source identity and location, intended
   generated-map target set, observable success condition, and any evidence or gate that must be resolved first.
4. Treat a missing or conflicting basis, an absent named plan, multiple plausible next actions, a source/map
   identity mismatch, insufficient source evidence, or an ownership ambiguity as `Blocked`. Do not repair the
   gap from generated output, `map_state.md`, project memory, directory inference, or chat history.

Map roadmap text is execution basis for a small unit only when state identifies one safe exact next action and no
independent decision gate remains. A scoped plan refines one map roadmap unit; it does not supersede the map-wide
roadmap or grant authority outside the selected scope.

### Scoped map planning

Create or refine a scoped plan only when decomposition materially improves execution or resumption. Use one flat
file beneath the active workspace:

```text
plan/agent_plan_<scope>.md
```

The file records the bounded mapping objective, source/map identity relevant to that unit, ordered map work,
generated-output targets, validation, status, and the next useful boundary. Keep `agent_plan.md` roadmap-level and
make `agent_state.md` name the active scoped plan and its exact next step. A still-larger later unit may use another
flat peer plan; do not create nested plan directories or reinterpret a scoped plan as a project phase.

Creating or refining agent-owned map planning does not automatically require project-style plan approval,
contract review, or final-truth review. Stop for human direction only when the plan changes the selected mapping
scope, chooses among materially different identities or targets, proposes destructive work, adds a high-cost
optional artifact, or reaches another decision that genuinely requires authorization. After an agent-performable
planning action, reconcile the new exact step through shared handoff before executing it; one-step continuation
authorization does not carry forward.

### Apply mapping gates

Before substantive source inspection or generated-output mutation, apply the **Mapping Proposal Gate** to the
derived action unless either the current-session request already explicitly approved that same displayed action,
source, map identity, scope, and non-destructive target set, or a valid current-session/fresh-session continuation
explicitly authorizes the one reconstructed exact action and its execution basis already fixes those same fields.
Approval of one proposal or continuation does not authorize a later scope or target expansion.

Always stop separately for:

- a selected-scope change or materially different source/map identity;
- a destructive rebuild under **Destructive rebuild**;
- removal under **Action: Remove Code Map**; or
- a costly optional artifact or material optional-index expansion.

A fresh-session auto-execute request authorizes only the one exact action reconstructed from current workspace
memory. It never bypasses one of these unresolved gates, an identity or ownership blocker, or an unsupported
completion claim.

### Execute the approved action

1. Resolve the repository-local workspace, authoritative source, and active generated-map store independently.
2. Inspect actual source before making or preserving any non-obvious map claim. Use only the build structure,
   representative implementation, tests, examples, and call sites needed for the approved scope.
3. Recheck source/map identity against the intended action. A mismatch or insufficient evidence stops generated
   output changes until the applicable proposal or identity gate resolves it.
4. Resolve the exact generated-map files approved for the action. Treat `workspace.md`, `agent_plan.md`,
   `agent_state.md`, `map_calibration.md`, `plan/`, supplied source, and unknown colocated files as protected from
   generated-output mutation even when Embedded Bonsai makes workspace and output paths overlap.
5. Create or update only the approved generated targets. Preserve useful established generated-map layers and
   structure unless the approved action specifically requires their change; do not normalize for neatness.
6. Validate the changed output against the source evidence and the applicable completion checks below. If the
   evidence changes the approved scope, target set, or success condition materially, stop at the owning gate.
7. Delegate the completed exact action to `skills/handoff.md`. Do not begin the next derived action in the same
   authorization step.

### Reconcile completion and reactivation

Through the map branch of `skills/handoff.md`, reconcile the completed action against the map-wide roadmap, active
scoped plan when present, `agent_state.md`, actual source/map identity, changed generated output, and performed
checks.

- When selected-scope work remains, update the applicable roadmap or scoped-plan status, replace the completed
  step in state with one concrete safe next action, record its success condition and blockers, and set readiness
  from the real next gate.
- When a scoped plan is exhausted, mark it complete, return control to the map-wide roadmap, and either derive the
  next bounded roadmap action or evaluate selected-scope completion. Do not turn scoped-plan completion into a
  project phase transition.
- Set `Execution Readiness: Complete` only when the current selected mapping scope has no unfinished roadmap or
  scoped-plan work and generated output is sufficiently reconciled with the selected source identity for that
  scope. Remove obsolete next-step, active-plan, blocker, and reconciliation state rather than retaining history.
- A later observed source change, explicit maintenance request, expanded selected scope, or newly discovered map
  need may reactivate the same workspace. Reconcile the new scope and identity into `agent_plan.md` and
  `agent_state.md`, derive its actual proposal, planning, blocker, or execution gate, and leave prior generated
  output in place until an approved action changes it. Do not reactivate merely because time passed or because a
  broader map might be possible.

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
5. For **Create Code Map**, prefer established current-session context over asking the human to restate it:
   - when the current repository is the intended source, default the source location to `<repository-home>`;
   - when repository identity is unambiguous, derive the logical source name from that repository/source identity;
   - derive source snapshot evidence from the current checkout when cheaply available;
   - derive the proposed map identity from the source universe, normally the logical source name, not from the
     consuming project;
   - use repository orientation and initial subsystem identification as the default initial bounded mapping scope
     when no narrower source-backed scope is already established; and
   - when an active project invoked creation for the current repository, treat that project as a likely consumer
     and include project association in the proposal, while allowing the human to decline or change it.
6. Do not invent defaults when several source identities, snapshots, or map identities remain materially plausible.
   Ask only for the unresolved choice that changes the mapping action.
7. Inspect only the named map entry or directory metadata needed to determine whether the map exists, whether its
   identity aligns, and which files are map-owned. A colocated non-map file does not prove a map exists.
8. Resolve the corresponding repository-local map-workspace candidate independently:
   - direct **Create Code Map** normally uses the same name for the map workspace and generated map;
   - if a valid same-name map workspace exists and its source identity is compatible, plan to reuse it;
   - if no workspace files exist at the same-name repository-local target, plan to create the workspace
     automatically as part of the approved code-map action;
   - if a partial, invalid, or incompatible same-name workspace exists, stop with the concrete conflict rather
     than creating duplicate execution memory or silently choosing another workspace name.
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

If **Create Code Map** resolves to an existing usable `code_map.md`, do not overwrite it as creation. Offer a
bounded update, a separately gated rebuild, or a distinct source identity as appropriate.

## Mapping Proposal Gate

Whenever **Active Map Workspace Execution** requires this gate, and for any generated-map lifecycle action not
already validly authorized through one exact continuation action, present this information before substantive
source inspection or mutation:

- **Action:** selected lifecycle action;
- **Source:** logical name, type, location, and available snapshot identity;
- **Map identity:** selected named source map;
- **Map workspace:** existing compatible workspace to reuse, exact new repository-local workspace to create, or
  `Not required` for a read-only/non-workspace action;
- **Map store / target:** resolved store and proposed map-owned target set;
- **Project association:** active project to add after a usable map exists, `None`, or `Not applicable`;
- **Scope:** repository orientation, one named subsystem, API mechanics, maintenance, cleanup, or another
  concrete bound;
- **Alignment:** `Aligned`, `Mismatch`, `Insufficient evidence`, or `Not applicable for new map`;
- **Inputs:** actual source plus any project or human calibration that will be consulted;
- **Proposed next step:** one concrete action and why it is next;
- **Risks / uncertainties:** only those that can change the proposed action.

Load `skills/menu.md` and offer concrete choices to proceed, redirect scope or identity, discuss a material
ambiguity, or cancel and return to the invoking gate. Wait for explicit human direction.

Approval covers only the displayed action, source, map identity, workspace disposition, project-association
choice, scope, and non-destructive target set. When **Create Code Map** shows creation of the corresponding map
workspace, that workspace creation is part of the approved code-map action and must not trigger a second,
standalone workspace-creation gate.

Approval does not authorize a later destructive rebuild, removal, scope expansion, source mutation, or high-cost
optional index.

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
   - source identity: the approved logical source, type, exact location, and available snapshot evidence;
   - roadmap: one bounded active initial mapping unit plus only justified pending work;
   - state: one safe exact next step, success condition, blockers, and `Ready to execute` only when evidence is
     sufficient.
   Do not create `map_calibration.md`, a scoped plan, or `plan/` as a side effect.
4. Establish the validated or newly created map workspace as the active `map` workspace in current-session context
   only. Do not persist an active-map pointer.
5. Inspect actual source for orientation before deep mapping. Use build structure, representative source, tests,
   examples, and call sites only as needed for the approved scope.
6. Treat relevant project truth and applicable `map_calibration.md` as calibration, not source proof. Preserve
   material disagreements as uncertainty.
7. Resolve the exact map-owned files to create. Preserve every pre-existing human-owned or otherwise unowned file,
   including any calibration or supplied source artifact physically colocated with the target map. Treat
   source-local calibration outside the active map store as read-only input.
8. Instantiate only justified artifacts from `<bonsai-home>/templates/`:
   - `code_map_template.md` for the required entry;
   - `subsystem_map_template.md` for each approved architectural subsystem;
   - `api_pub_template.md` and `api_ext_template.md` only when non-obvious reusable mechanics justify them;
   - `namespace_router_template.tsv`, `manifest_template.tsv`, and `symbol_index_template.tsv` only when their
     narrow lookup value exceeds maintenance cost.
9. Record the logical source and the smallest useful snapshot identity in `code_map.md`. Keep all drill-down links
   relative to the named source map.
10. Build one active subsystem at a time. Complete its architecture map and evaluate both API-map needs before
    moving to another subsystem.
11. When apparent design and actual use may differ, check at least one representative production use, test,
    example, call site, or extension before recording the mechanic as durable.
12. Update related routing and lookup artifacts together only when their contracted role is affected.
13. Validate the created artifacts under the structural and completion rules below.
14. If the approved proposal included adding the completed map to an active project, perform that association only
    after `<active-map-store>/<map>/code_map.md` is usable. Delegate the canonical project-context mutation to
    `skills/agent_context.md`; do not make association a condition for map identity or workspace validity.
15. Reconcile the completed bounded mapping action through `skills/handoff.md`. Do not continue into another
    mapping unit under the same authorization.

Creating a map store or named source directory after approval does not transfer ownership of existing contents.
Template presence never authorizes optional output.

Before creating a costly optional artifact or materially expanding an optional index, show why its repeated
navigation value exceeds its maintenance cost, identify the exact output and scope, and stop for explicit human
approval.

## Action: Inspect Code Map

Inspection is read-only.

1. When no map was named by the human, present the already-discovered usable code-map names in stable lexical
   order only as the selection for this inspection; do not rescan or pre-read every map.
2. Load the selected map's `code_map.md` first.
3. When source-dependent claims or identity matter, resolve the selected source and classify map/source alignment.
4. Load only the subsystem, API, namespace, manifest, symbol, or identity facet needed for the inspection question.
5. Use actual source to verify non-obvious behavior; report map claims as navigation, not authority.
6. Report missing, stale, mismatched, uncertain, or malformed data without changing it.

Inspection does not create `map_state.md`, normalize existing files, update identity metadata, or preserve context
unless the human separately authorizes the applicable action. An explicit **Inspect Map/Source Identity** request is
handled as this same read-only inspection path with identity/alignment as the selected facet.

## Action: Update or Rebuild Code Map

First determine whether the requested work is a bounded update or a destructive rebuild.

### Bounded update

Use an update for known material changes to source identity, public structure, extension mechanics, lifecycle,
architectural relationships, subsystem ownership, rebuild-relevant behavior, or reusable routing.

1. Verify map/source alignment and the approved scope.
2. Improve existing artifacts in place. Preserve their established structure unless normalization was explicitly
   included in the approved scope.
3. Update only map-owned artifacts whose durable content changed.
4. Update dependent entry, subsystem, API, and lookup artifacts together when their narrow generated-output roles
   are affected. Reconcile repository-local workspace plan/state separately through shared handoff.
5. Re-check representative usage when a caller or extension mechanic changed.

Routine bug fixes, private refactors, tests, cosmetic cleanup, and ordinary churn do not justify map updates by
themselves. Bonsai does not continuously scan for drift or silently update maps after implementation work.

### Destructive rebuild

A rebuild requires a separate explicit gate after inspection, even when the broader **Update or Rebuild Code Map**
action was previously selected.

Before that gate:

1. resolve and display every existing agent-owned target that would be replaced or removed;
2. display every known preserved item in the target map, including `map_calibration.md`, supplied source inputs, and
   other unowned files;
3. show the source snapshot, map identity, rebuild scope, proposed replacement artifacts, and validation plan; and
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

### Subsystem selection and order

A subsystem must represent a demonstrated architectural responsibility, ownership boundary, lifecycle, data or
execution concern, reusable API/extension surface, or cross-boundary behavior. A directory, module, source root,
or package group is evidence, not automatically a subsystem.

Prioritize owner-weighted, foundational, developer-facing, cross-boundary, widely reused, risky, or repeatedly
misunderstood areas. Deprioritize generated code, narrow helpers, leaf utilities, shallow inventories, obvious
details, and non-representative examples.

Finish the approved active subsystem and decide whether each API map is justified before selecting a new one. A
new subsystem or expanded scope requires human direction.

When subsystem mapping has accumulated enough context to reduce confidence or compression quality, stop at a
bounded action boundary, reconcile the active map workspace through `skills/handoff.md`, and offer current-session
and fresh-session continuation as peer choices when one safe exact next action exists. Bonsai does not control the
host session.

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
- keep lookup tables selective and structurally boring;
- keep repository-local map plan/state current rather than historical; and
- remove duplicated, stale, wrong-layer, obvious, or low-value content.

Do not structurally normalize an existing map during routine maintenance. Do not create optional artifacts because
a template exists. Do not turn maps into project/session guides, API manuals, filesystem mirrors, prose indexes,
or hand-maintained language-server databases.

## Agent Context

When mapping establishes or disproves a stable source location, project-relevant map selection, or another durable
operational rule, load `skills/agent_context.md` and apply its qualification and narrowest-scope rules.

Do not store active-project selection, transient extraction paths, one-run inspection locations, speculative source
identity, map workflow state, or map content in agent context. Context maintenance grants no permission to broaden
the mapping action.

## Contextual First Use and Maintenance

- A substantial existing source without a useful map may receive one contextual **Create Code Map** action.
- If the human declines, return that result to the invoking workflow so creation moves under **See more options**
  rather than interrupting again in the same context. Do not create a placeholder map or state file for a decline.
- Greenfield source with little stable structure receives no map pressure.
- Surface maintenance only for an explicit request or a known material structural change.
- Do not continuously discover drift, repeatedly offer declined work, or update maps after routine changes.

Preserve a longer-lived source or selection rule only when it independently qualifies under `skills/agent_context.md`.

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

Before reporting an approved mapping scope complete:

1. verify `code_map.md` identifies the source sufficiently for intended alignment and remains compact;
2. verify entry, subsystem, API, calibration, state, and lookup content stays in its contracted layer;
3. verify each mapped subsystem has a demonstrated responsibility and source-backed owning paths;
4. verify each active subsystem's caller and extension map needs were created or deliberately found unnecessary;
5. verify non-obvious claims are source-backed or visibly inferred/uncertain;
6. verify relative links and optional-artifact references match files that actually exist;
7. validate every materially edited TSV header, literal-tab separator, fixed column count, and one-line row;
8. verify only approved map-owned targets changed;
9. verify supplied source, every consulted `map_calibration.md`, and other unowned files remain unchanged;
10. verify no transient inspection became durable map data;
11. reconcile the map-wide roadmap, active scoped plan when present, and current resume state through shared
    handoff; and
12. maintain only qualifying agent context through `skills/agent_context.md`.

If the current scope has no real next step, mark it complete rather than inventing more mapping work.

## Completion and Invoking-Gate Return

At completion of substantive work for an active map workspace:

1. report the action, source, map identity, bounded result, changed map-owned files, checks actually performed,
   preserved unowned files, remaining uncertainty, and whether qualifying agent context changed;
2. reconcile repository-local `agent_plan.md`, `agent_state.md`, any active scoped plan, generated output, and
   source/map identity through `skills/handoff.md`; reconcile qualifying agent context when applicable;
3. do not silently revise human-owned `map_calibration.md`, project final truth, or project execution memory;
4. let shared handoff derive and present the refreshed active-map completion, blocker, or continuation gate; and
5. do not also restore the older repository-entry or **Manage Code Maps** gate after active workspace execution.

For cancellation, a declined contextual offer, or non-mutating inspection that did not complete an active map
workspace exact action, return control to the retained invoking workflow. When an active project exists, let its
owning workflow reconcile project execution state; when none exists, do not manufacture project state. Load
`skills/menu.md` and re-present that refreshed invoking gate unless the mapping action created a new required
blocker, design, final-truth, or review gate.

Do not silently end the parent workflow because mapping completed or was cancelled. Do not select a new mapping
scope automatically. Stop at the refreshed gate for the human's direction.

## Output Style

Use concise wording, exact paths, stable headings, explicit uncertainty, and no filler. Distinguish observed facts
from inference. Do not claim a source, map, identity, mutation, removal, or check that was not actually inspected or
performed.
