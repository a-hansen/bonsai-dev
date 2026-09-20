# Code Maps

## Purpose

Create, inspect, extend, refresh, rebuild, remove, and use selective generated source-navigation maps through Bonsai's normal identity, menu, context, workspace, and human-gate model.

A **code map** is the user-facing mapping concept. A **map workspace** is durable execution memory used to create, extend, refresh, rebuild, and resume a code map. Normal code-map actions may create, reuse, reactivate, resume, or update workspace memory as needed; ordinary mapping must not require the human to create a workspace first.

Generated maps describe observed source and are reusable navigation aids. They are not source authority, project truth, workspace execution memory, or exhaustive documentation.

Source mapping requires no Bonsai project or active project. **Manage Code Maps** may start directly from the repository-entry gate. Never create project memory merely to enable mapping. Normal user interaction speaks in code-map terms; expose workspace lifecycle directly only when the human intends to create, inspect, resume, or manage the workspace itself.

## Global Invariants

These rules apply throughout this skill unless a narrower section explicitly adds a stricter rule.

### Authority

Use evidence in this order:

1. selected actual source, including build files, tests, examples, and representative uses;
2. approved project final truth and archaeological analysis as attention/interpretation context;
3. optional human-owned `map_calibration.md` as source-specific calibration;
4. existing generated map data as navigation memory that must remain source-aligned.

Source wins over project memory, calibration, and map content. Preserve disagreement as visible mismatch or uncertainty until corrected.

### Ownership and mutation

Keep these concepts distinct even when Embedded Bonsai colocates them physically:

| Role | Owned content |
| --- | --- |
| Map workspace | `agent_plan.md`, `agent_state.md`, optional `plan/agent_plan_<scope>.md` |
| Human calibration | `map_calibration.md` |
| Generated map | `code_map.md`, subsystem/API maps, optional generated lookup/index artifacts |
| Source/input | repository checkout, source tree/archive, supplied artifacts |

A named map directory is a storage boundary, not blanket ownership. Never treat unknown colocated files as agent-owned merely because of location. Never mutate human calibration, supplied source, project truth, or project execution memory through map-output operations.

Generated runtime map data may be written only under the resolved active map store. Never write runtime map state into Bonsai standards, staged distributions, or template locations.

### Workspace/session separation

Map workspaces contain mapping continuation only. Do not store active-project selection, project phase/pass state, approvals, requirement tracking, contract/final-truth status, icebox state, active-workspace pointers, or session history in workspace or generated-map data.

Active workspace identity exists only in current-session context. Never persist an active-map pointer.

Do not reconstruct missing workspace state from generated output, project memory, directory inference, chat history, or speculation. Missing/conflicting required state is `Blocked`.

### Mapping-unit authorization

A human-selected **bounded mapping focus** is the execution-authorization boundary. It may cover one subsystem, caller/extension concern, cross-cutting behavior, persistence, event handling, serialization, lifecycle, tracking, or another bounded source-backed concern. It need not correspond one-to-one with a generated subsystem.

For ordinary non-destructive mapping, the normal generated-output envelope is:

```text
code_map.md
subsystems/<subsystem>/map.md
subsystems/<subsystem>/api_pub.md
subsystems/<subsystem>/api_ext.md
```

Source discovery may determine architectural ownership, whether one or several subsystem maps are affected, whether a new subsystem is justified, whether no same-named subsystem should exist, and which standard files in that envelope are required. These are discovery-resolved details within an already authorized focus and do not create a routine second gate.

Creating or materially expanding optional lookup/index artifacts such as `namespace_router.tsv`, `manifest.tsv`, or `symbol_index.tsv` is outside that implicit envelope and requires explicit authorization. Existing optional lookup data may receive only bounded maintenance needed to keep already-authorized routing correct.

Always stop for human direction before:

- material expansion of mapping focus or current source scope;
- materially different source or map identity;
- unresolved source/map alignment;
- destructive rebuild or removal;
- generated-map ownership restructuring beyond ordinary representation of the selected focus;
- a genuinely unrelated mapping objective;
- optional lookup/index creation or material expansion;
- another costly optional artifact;
- insufficient source evidence; or
- another material decision requiring authorization.

Do **not** stop merely because source discovery selects different standard Markdown targets than predicted, spans several existing subsystems, justifies `api_pub.md` or `api_ext.md`, justifies a new subsystem, or finds no standalone subsystem matching the focus.

### Lifecycle and completion

Create, extend, refresh, rebuild, inspect, and remove remain distinct lifecycle intents. Completion is only for the current mapping scope and represented source state; later source change or new coverage may reactivate the same compatible workspace.

Complete and validate the full authorized mapping unit before selecting another focus. Discovery alone is not completion when justified generated-map mutation remains.

## When to Load

Load this skill only when:

- the human selects **Manage Code Maps**;
- startup explicitly requests a code-map action;
- implementation needs map-guided navigation or map/source alignment checking;
- the human accepts contextual first-use mapping for substantial existing source;
- the human accepts a contextual extension recommendation; or
- the human accepts bounded refresh after a known material structural source change.

Do not load editing workflow merely because a map exists. Routine source edits are not map maintenance. Ordinary consumption reads `code_map.md` first, then only the deeper artifact needed for the current facet.

## Collections and Identity

Resolve these independently from repository and Bonsai Home identity supplied by `start.md`:

- repository-local map workspaces: `<repository-home>/.bonsai/maps/`;
- reusable generated maps: active map store below.

Enumerate only immediate child directories, in stable lexical order, and retain separate typed collections even when names coincide.

A repository-local child is only a **workspace candidate** until workspace entry and required execution memory validate. A generated-map child is **usable** only when its agent-owned `code_map.md` exists and is readable. One never proves the other.

In Embedded Bonsai, `<repository-home>/.bonsai/maps/<map>/` may physically hold both workspace and generated output. Classify by role:

```text
agent_plan.md                    # map-wide roadmap
agent_state.md                   # current resume state
map_calibration.md               # optional human-owned input
plan/agent_plan_<scope>.md       # optional scoped plan
code_map.md                      # generated-map entry
namespace_router.tsv             # optional generated routing
manifest.tsv                     # optional generated registry
symbol_index.tsv                 # optional generated routing
subsystems/                      # optional generated drill-down maps
```

## Active Generated-Map Store

Resolve independently from source location and active project:

- configured Bonsai Home: `<bonsai-home>/maps/`;
- Embedded Bonsai with no configured external home: `<repository-home>/.bonsai/maps/`.

Mapping source in another repository, directory, or archive does not relocate generated output beside that source.

For a repository checkout, source-local calibration is:

```text
<source-repository>/.bonsai/maps/<source>/map_calibration.md
```

Calibration is human-owned input. Never move, copy, normalize, or rewrite it because generated output lives elsewhere. Embedded Bonsai may colocate calibration and output physically without merging ownership.

Several projects may reuse one named source map; one project may select several maps. Map identity comes from the source universe, never the consuming project.

A named generated map may contain:

```text
<map-store>/<source>/
    code_map.md                       # required for usability
    namespace_router.tsv              # optional
    manifest.tsv                      # optional
    symbol_index.tsv                  # optional
    subsystems/<subsystem>/map.md
    subsystems/<subsystem>/api_pub.md # optional
    subsystems/<subsystem>/api_ext.md # optional
```

## Manage Code Maps Entry

Retain the invoking Bonsai gate.

On **Manage Code Maps**, do only cheap deterministic discovery needed for the menu:

- enumerate immediate repository-local workspace children;
- enumerate immediate active-map-store children;
- for generated maps, check only readable `code_map.md` presence;
- do not read map/workspace/state/plan/calibration/source/drill-down content merely to render the menu.

Keep workspace candidates and usable generated maps as separate typed collections.

When useful, show compact status:

```text
Available code maps: <stable lexical list or none>
Active project: <project or none>
Maps used by <project>: <selected usable maps or none>
Map workspaces: <count or stable lexical list when materially useful>
```

If status already names available maps, do not add a redundant list-only action.

If no specific action was requested, load `skills/menu.md` and show only applicable actions:

1. **Create Code Map**.
2. **Extend Code Map** if a usable map exists.
3. **Inspect Code Map** if a usable map exists.
4. **Refresh Code Map** if a usable map exists.
5. **Rebuild Code Map** if a usable map exists.
6. **Remove Code Map** if a usable map exists.
7. **Add a Code Map to the Active Project** if a valid active project exists and at least one usable map is unselected.
8. **Remove a Code Map from the Active Project** if a valid active project exists and at least one selected identity remains usable.
9. **Manage Map Workspaces**.
10. **Cancel and return to `<invoking gate>`**.

Omit unavailable actions rather than preserving fixed numbering.

Primary UX manages code maps. Workspace lifecycle is secondary under **Manage Map Workspaces**. Do not require a workspace choice merely to map current source. Resolve missing evidence inside the chosen action instead of eagerly validating every candidate.

### Manage Map Workspaces

This submenu provides direct repository-local execution-memory control for advanced, external-source, calibration, inspection, and resume cases.

On entry, cheaply enumerate workspace candidates in stable lexical order. Do not validate all candidates just to render the submenu.

Show only applicable actions:

1. **Create Map Workspace**.
2. **Resume Map Workspace** if candidates exist.
3. **Inspect Map Workspace** if candidates exist.
4. **Cancel and return to Manage Code Maps**.

**Create Map Workspace** is explicit lifecycle management, not a prerequisite for **Create Code Map**.

For **Inspect Map Workspace**, select one candidate, validate only it using the same entry/plan/state rules as resume, and report source identity, current scope, roadmap status, readiness, blocker, active scoped plan, and exact next step without mutation or activation.

After inspection/cancellation, return to refreshed **Manage Map Workspaces**. After explicit creation, follow creation rules below. After successful resume, the selected map workspace becomes the active session workspace and replaces the prior parent gate.

### Project Map Associations

Available only when the invoking context supplies one active `project` workspace. Omit at repository entry and while an active map workspace owns the session. Do not ask the human to select/create a project merely to expose association actions.

Before offering Add/Remove:

1. Revalidate project home as one immediate child of `<repository-home>/.bonsai/projects/` with readable `agent_plan.md` and `agent_state.md`; the structural path establishes project type.
2. Resolve active generated-map store independently. A selectable map is one immediate child with readable agent-owned `code_map.md`.
3. Load `skills/agent_context.md`; read only the selected project's `agent_context.md` if present. Canonical `Useful code maps:` entries are project selections, not usability proof.
4. **Add:** list usable, unselected maps. **Remove:** list only selected identities still usable. Stable lexical order; accept corresponding number.

Immediately before mutation, revalidate project and chosen map. Map name must be one directory component and `<active-map-store>/<map>/code_map.md` must still be readable. Same-name workspace/state does not prove a valid target. If project/map identity is invalid, stale, ambiguous, or unusable, stop without changing context.

After concrete human selection, delegate only canonical project-context mutation to `skills/agent_context.md`. Report project, map identity, and exact project `agent_context.md` target. The association operation must not create/rebuild/move/rename/edit/delete generated maps; mutate map workspace or project/map execution memory; or persist active session/workspace identity.

Already-present Add and already-absent Remove are successful no-ops. Verify selection afterward and return to refreshed **Manage Code Maps** via `skills/menu.md`.

Association maintenance does not activate a map, inspect source, or authorize another lifecycle action. Exception: an association explicitly approved as part of **Create Code Map** may run as that action's final post-creation step.

## Create, Select, and Resume Map Workspaces

### Create Map Workspace

This explicit submenu action creates execution memory directly. It is not ordinary **Create Code Map** setup and not the Web UI `prompts/create_map.md` design/calibration workflow.

Before proposing creation require:

- a human-supplied unused workspace name;
- map-wide objective and initial bounded mapping scope;
- source logical name, type, exact location, and available snapshot evidence;
- one safe exact initial action, or concrete missing evidence recorded as blocker.

The name must be one directory component. Reject empty, `.`, `..`, absolute paths, drive prefixes, separators, control characters, or targets outside `<repository-home>/.bonsai/maps/`.

"Unused" means no valid or partial workspace already owns that name; a same-name generated map may exist.

Preflight exact target without mutation. If it exists, inspect enough items for safety. Embedded overlap may make an existing same-name generated directory correct. Permit creation there only when `agent_plan.md` and `agent_state.md` are both absent and nothing makes ownership ambiguous. Preserve `code_map.md`, generated artifacts, `map_calibration.md`, and all other colocated files unchanged. If either required workspace file already exists without a complete valid workspace, stop as conflicting; creation does not overwrite, complete, or repair it.

Before mutation, report name, repository-local target, source identity, initial scope, the exact two files to create, every known preserved colocated item, and whether target overlaps generated-map store. Load `skills/menu.md`; offer creation of exactly that workspace, revision, discussion, or cancellation; wait for explicit confirmation.

After approval, create only:

```text
<repository-home>/.bonsai/maps/<map>/agent_plan.md
<repository-home>/.bonsai/maps/<map>/agent_state.md
```

The containing `maps/` path establishes map type. `agent_plan.md` is the map-wide roadmap for approved objective/scope. `agent_state.md` records current scope, source/map identity evidence, readiness, one exact next step or concrete blocker, success condition, and only resume-critical files.

Do not add project phases/passes/final-truth/contract state or active-workspace pointers. Set `Ready to execute` only when the action has sufficient evidence and no independent gate; otherwise record the concrete `Blocked` condition.

Do not create/modify `map_calibration.md`, generated-map output, scoped plans, or `plan/` as a side effect. If both required files cannot be created without changing a pre-existing item, stop and report the partial result rather than claiming a valid workspace.

Validate the completed workspace, activate it only in current-session context, then use **Select or Resume a Map Workspace** behavior below.

### Select or Resume a Map Workspace

For resume, list candidates in stable lexical order. When selection is needed, use numbered choices. Inspect only the selected candidate; invalid candidates remain visible but unavailable with a concrete reason.

Validate in this order:

1. confirm the selected directory is one immediate child of `<repository-home>/.bonsai/maps/`; the structural path establishes map type;
2. require readable `agent_state.md` and `agent_plan.md`;
3. read state first, plan second; compare overlapping mapping scope, roadmap status, readiness, blocker, active scoped-plan identity, exact next step, and completion claims;
4. read one flat `plan/agent_plan_<scope>.md` only when state names it or it is required to establish the current gate; reject missing named plan or any path outside the workspace;
5. classify missing required files, conflicting common truth, unsafe exact step, or unsupported completion as `Blocked` rather than guessing/repairing.

Do not read generated output, project memory, or chat history to reconstruct missing state. Load calibration, actual source, generated output, developer context, or agent context only when the reconstructed exact action requires that facet.

After validation, establish name/home as active `map` workspace in current-session context only. Return reconstructed condition to the implementation kernel as the refreshed active-map gate. Compatible mapping proceeds through this skill and shared handoff; human gate/blocker stops there.

Successful selection replaces repository-entry gate for this session. Cancellation, invalid selection, or non-mutating inspection returns to retained invoking gate through `skills/menu.md`, unless a concrete blocker must be shown first.

## Active Map Workspace Execution

Use only after startup or resume establishes one valid active `map` workspace. Workspace memory supplies continuation authority; generated map content does not.

### Derive one bounded action

1. Start from loaded `agent_state.md`, then `agent_plan.md`, plus the one named flat scoped plan when applicable. Confirm overlapping scope, roadmap status, active-plan identity/status, readiness, blockers, exact next step, and completion claims agree.
2. Derive exactly one action from the narrowest applicable basis:
   - map-wide roadmap for a small bounded unit;
   - active scoped plan for a larger unit named by state;
   - drafting/refining one scoped plan when roadmap detail is insufficient.
3. An executable mapping unit must identify current mapping scope, human-selected bounded focus, source identity/location, normal output envelope, observable success condition, and any unresolved evidence/blocker/independent gate.
4. Exact standard generated files need not be known before discovery.
5. `Blocked`: missing/conflicting basis, missing named plan, multiple plausible focuses, source/map identity mismatch, insufficient source evidence, or ownership ambiguity not safely resolvable from authoritative source.

A roadmap directly authorizes a small unit only when state identifies one safe bounded focus and no independent gate remains. A scoped plan refines one roadmap unit; it never supersedes the map-wide roadmap or grants authority outside current scope/focus.

### Scoped map planning

Create/refine a scoped plan only when decomposition materially improves execution or resumption:

```text
plan/agent_plan_<scope>.md
```

Record bounded objective, relevant source/map identity, selected focus, ordered work, known/expected generated-output effects, validation, status, and next useful mapping-unit boundary. Exact standard target files may remain discovery-resolved.

Keep `agent_plan.md` roadmap-level. `agent_state.md` names the active scoped plan and exact next action. Larger later units may use flat peer plans; never nest plan directories or treat scoped plans as project phases.

Agent-owned mapping-plan work does not automatically require project-style plan approval, contract review, or final-truth review. Stop only if planning changes selected focus/current scope, needs materially different source/map identity, proposes destructive work, restructures generated ownership, adds a costly optional artifact, or reaches another real authorization decision.

Planning continuation authority ends when the planning action completes. Once durable state establishes one executable bounded unit, continuation authority covers that full mapping unit.

### Apply mapping gates

Before executable mapping, apply the **Mapping Proposal Gate** unless the same bounded unit was already explicitly established and current-session or fresh-session continuation authorizes it.

Authorization is based on focus, source identity, map identity, current scope, and normal output envelope, not preapproval of every standard Markdown path.

Continuation of one executable unit covers:

```text
selected bounded mapping focus
        ↓
inspect authoritative source
        ↓
determine architectural ownership
        ↓
determine justified standard map layers
        ↓
create/update those standard layers
        ↓
validate against source
        ↓
reconcile workspace execution memory
        ↓
stop at next mapping-unit boundary
```

Do not insert a routine human gate between discovery and standard generated-map production.

A fresh-session auto-execute request authorizes only the one exact action reconstructed from workspace memory. For executable mapping, that action is the full bounded unit above, not discovery alone. It never authorizes the next unit or bypasses a real gate/blocker.

### Execute the authorized mapping unit

1. Resolve workspace, authoritative source, and active map store independently.
2. Inspect actual source only as needed for the selected focus. Use build structure, representative implementation, tests, examples, and call sites as needed.
3. Recheck source/map identity while inspecting. Mismatch or insufficient alignment evidence blocks generated-output changes until resolved.
4. Determine architectural ownership from source before choosing exact standard targets.
5. Create/update justified standard targets within the authorized envelope:
   - `code_map.md` when source identity, orientation, or routing changes;
   - `subsystems/<subsystem>/map.md` for each architectural domain needed for the focus;
   - `api_pub.md` for reusable non-obvious caller mechanics;
   - `api_ext.md` for reusable non-obvious extension mechanics.
6. Preserve workspace memory, calibration, `plan/`, supplied source, and unknown colocated files from generated-output mutation.
7. Do not create/materially expand optional lookup/index artifacts without authorization; bounded maintenance of existing routing is allowed only as stated in Global Invariants.
8. Validate all changed generated output against source and completion rules.
9. If discovery materially escapes authorized focus, source scope, identity, or normal output envelope, stop at the applicable gate.
10. After full unit generation and validation, delegate reconciliation to `skills/handoff.md`.

Do not delegate merely because discovery finished and standard targets became known. Discovery, ownership resolution, standard mutation, and validation normally form one unit.

### Reconcile completion and reactivation

Through the map branch of `skills/handoff.md`, reconcile the completed unit against map-wide roadmap, active scoped plan if any, `agent_state.md`, actual source/map identity, changed generated output, and performed checks.

- Mark completed focus and output effects accurately in roadmap/scoped plan.
- If current scope still has useful work but no next focus is selected, present concrete next-focus choices and stop. Never silently choose/execute one.
- When the human selects next focus, reconcile it into `agent_plan.md`, `agent_state.md`, and active scoped plan if applicable; do not change generated output during selection reconciliation.
- Once that focus is one safe exact unit with success condition and no independent gate, record ready and offer current-session continuation, fresh-session continuation, review/change, and **Exit for now** through shared handoff.
- When a scoped plan is exhausted, mark it complete and return to the map-wide roadmap; this is not a project phase transition.
- Set `Execution Readiness: Complete` only when current selected mapping scope has no unfinished roadmap/scoped-plan work and output is sufficiently reconciled with selected source identity for that scope.
- Later source change, maintenance request, scope expansion, or new map need may reactivate the same workspace. Preserve prior generated output until newly authorized work changes it.

Never write project phases/passes, contract/final-truth/icebox state, active-workspace identity, or session history into map memory.

## Resolve the Mapping Context

Before substantive mapping proposals, resolve only enough context to make the chosen action/gate trustworthy:

1. Retain invoking Bonsai workflow/gate, including repository-entry with no project.
2. Resolve active map store without creating/modifying it.
3. Resolve requested lifecycle action; if none, return to **Manage Code Maps**.
4. Identify actual source independently from active project: logical name, source type, exact location, and smallest useful snapshot evidence such as version, Git revision, artifact coordinate, or checksum.
5. For Create/Extend/Refresh, prefer established current-session context over repetition:
   - current repository may default source location to `<repository-home>` when intended;
   - derive logical source name from unambiguous repository/source identity;
   - use clearly relevant active-project calibration without making project the map identity;
   - carry trustworthy known structural-change evidence into refresh rather than rediscovering unrelated source;
   - when project association is obviously intended for a new map, propose it as post-creation association, not map identity.
6. Resolve map identity from source universe. Never silently choose among plausible source identities/snapshots.
7. Inspect only named map entry/directory metadata needed for existence, alignment, and known map-owned files. Colocated non-map files do not prove a map exists.
8. Resolve corresponding repository-local workspace independently. Same-name map does not prove workspace validity; same-name workspace does not prove map usability.
9. Resolve source-specific calibration only when materially useful. For repository checkout use `<source-repository>/.bonsai/maps/<source>/map_calibration.md`; use other locations only when explicitly supplied for that source.
10. Read project memory only when an active project exists and materially calibrates the selected action. No active project is not a mapping ambiguity/blocker.
11. Load `skills/agent_context.md` only when stable source locations, relevant map selection, or another qualifying operational rule may need application/maintenance.

If source location, map store, map identity, source snapshot, or ownership boundary remains materially ambiguous, stop and ask the human to resolve only that ambiguity. Do not invent resolvers, downloaders, registries, manifest schemas, dependency-to-map matching, or source-location conventions.

If **Create Code Map** finds an existing usable `code_map.md`, do not overwrite it as creation. Offer Extend, Refresh, separately gated Rebuild, or a distinct source identity as appropriate.

## Lifecycle Intent Boundaries

| Intent | Meaning |
| --- | --- |
| **Create** | Establish a reusable map for a source identity with no usable map. |
| **Extend** | Add useful coverage beyond prior intended scope. Human may name subsystem, cross-cutting concern, caller/extension surface, or other bounded concern. A requested subsystem is a focus, not a command to create a same-named generated subsystem. |
| **Refresh** | Reconcile represented mapped knowledge after material source change, preserving identity and existing coverage where practical; target the bounded concern made stale. |
| **Rebuild** | Replace substantial generated representation or broadly restructure ownership; always separately gated as more destructive. |

Do not disguise scope expansion as Refresh. Do not disguise substantial replacement/ownership restructuring as Extend or Refresh.

## Mapping Proposal Gate

Use whenever Active Map Workspace Execution requires it and for any generated-map lifecycle action not already authorized by continuation of the same selected unit.

Before substantive source inspection or mutation, present:

- **Action:** lifecycle action or bounded unit;
- **Source:** logical name, type, location, available snapshot identity;
- **Map identity:** selected named source map;
- **Map workspace:** compatible workspace to reuse, exact new repository-local workspace, or `Not required` for read-only/non-workspace action;
- **Map store:** resolved store;
- **Mapping focus:** bounded concern;
- **Generated-output envelope:** standard Markdown layers available for that focus plus separately proposed optional/destructive targets;
- **Project association:** project to add after usability, `None`, or `Not applicable`;
- **Alignment:** `Aligned`, `Mismatch`, `Insufficient evidence`, or `Not applicable for new map`;
- **Inputs:** source plus project/human calibration to consult;
- **Success condition:** observable completion condition;
- **Risks / uncertainties:** only items that can change the unit or require another human decision.

Known likely standard targets may be shown but are not a required pre-discovery contract.

Load `skills/menu.md`; offer concrete choices to approve/select or revise focus, discuss material ambiguity, cancel, or resolve the applicable gate. Wait for explicit human direction.

Approval establishes displayed source, map identity, workspace disposition, project-association choice, mapping focus, current source/mapping scope, and normal output envelope. If **Create Code Map** includes corresponding workspace creation, that creation is part of the approved action and gets no second standalone workspace gate.

Approval does **not** authorize later destructive rebuild/removal, material scope expansion, materially different source/map identity, ownership restructuring, source mutation, costly optional artifacts, or optional lookup/index creation/material expansion.

If current mapping scope is complete, say so. Do not invent another objective.

## Map and Source Alignment

`code_map.md` is the normal identity/routing entry. Use the smallest evidence that prevents silently trusting an incompatible snapshot.

- **Aligned:** map identity and selected source snapshot agree sufficiently for intended use.
- **Mismatch:** evidence shows different version, revision, coordinate, source type, or artifact.
- **Insufficient evidence:** a non-obvious alignment claim cannot be established.
- **Not applicable for new map:** no prior entry; creation will record observed identity.

On Mismatch/Insufficient evidence, do not rely on non-obvious map claims. Offer concrete choices to inspect source, update map, request gated rebuild, select another map/source, or stop. Never assume a development checkout matches a released dependency.

## Action: Create Code Map

Normal user-facing creation path.

After proposal approval:

1. Resolve corresponding workspace before generated output:
   - validate/reuse compatible same-name workspace;
   - if approved repository-local target has no workspace files, create workspace automatically;
   - if partial, invalid, incompatible, or ownership-ambiguous, stop before generated-output mutation.
2. Automatic creation writes only:

   ```text
   <repository-home>/.bonsai/maps/<map>/agent_plan.md
   <repository-home>/.bonsai/maps/<map>/agent_state.md
   ```

   Preserve all colocated generated artifacts, calibration, source/input, and unknown files. Use explicit workspace-creation ownership/overlap safety rules, but the approved code-map proposal already supplies objective, scope, and source identity, so no second human workspace-definition gate is required.
3. Initialize workspace from approved proposal:
   - objective: create/maintain reusable navigation knowledge for selected source;
   - current mapping scope: approved bounded creation scope;
   - selected focus: approved initial bounded focus;
   - source identity: approved logical source/type/location/snapshot evidence;
   - roadmap: one bounded active initial unit plus only justified pending work;
   - state: one safe exact next unit, success condition, blockers, and `Ready to execute` only with sufficient evidence.
   Do not create calibration, scoped plan, or `plan/` as a side effect.
4. Activate validated/new workspace only in current-session context.
5. Treat approved initial focus as authorization boundary; exact standard output targets remain discovery-resolved.
6. Inspect actual source for orientation and selected focus only as needed.
7. Project truth/calibration guide interpretation but never prove behavior; preserve material disagreement as uncertainty.
8. Preserve all pre-existing human-owned/unowned files, including colocated calibration/source. Source-local calibration outside map store is read-only input.
9. Determine exact standard layers from source-backed ownership.
10. Instantiate/update only justified standard Markdown artifacts from `<bonsai-home>/templates/`:
    - `code_map_template.md` when entry is needed;
    - `subsystem_map_template.md` for justified architectural subsystems;
    - `api_pub_template.md` / `api_ext_template.md` when non-obvious reusable mechanics justify them.
11. Do not create `namespace_router.tsv`, `manifest.tsv`, or `symbol_index.tsv` merely because useful. Their creation/material expansion requires explicit authorization.
12. Record logical source and smallest useful snapshot identity in `code_map.md`; keep drill-down links relative to the named map.
13. Complete all standard map effects of the selected focus before another focus. One focus may affect one subsystem, several, or none of the same name.
14. Where apparent design and actual use may differ, check at least one representative production use, test, example, call site, or extension before recording durable mechanics.
15. Validate under mapping/completion rules below.
16. If approved proposal included active-project association, perform it only after `<active-map-store>/<map>/code_map.md` is usable. Delegate canonical context mutation to `skills/agent_context.md`; association is not map identity/workspace validity.
17. Reconcile through `skills/handoff.md`; do not continue into another mapping unit under the same authorization.

Creating the map store/directory after approval does not transfer ownership of existing contents. Template presence never authorizes optional output.

Before costly optional artifact creation/material expansion, explain expected repeated navigation value versus maintenance cost, identify exact output/scope, and stop for explicit approval.

## Action: Extend Code Map

Use for useful new coverage in an existing compatible map.

1. Resolve usable generated map and corresponding workspace independently.
2. Validate map/source alignment before relying on non-obvious map claims; material incompatibility blocks extension.
3. Reuse/reactivate compatible workspace. Do not duplicate the map for new coverage.
4. Establish one bounded extension focus: subsystem, cross-cutting concern, reusable caller/extension concern, or human-requested review for valuable additions.
5. In suggestion mode, inspect existing map only enough to understand coverage and source only enough to identify a small number of high-value missing concerns. Prefer foundational, reused, cross-boundary, risky, or repeatedly non-obvious knowledge; never turn suggestion mode into exhaustive survey.
6. Present selected/proposed focus through Mapping Proposal Gate. Existing generated output stays unchanged until authorization.
7. After authorization, focus is the unit boundary; discovery decides architectural ownership and exact standard layers.
8. Preserve output outside focus. Ordinary extension may add/update justified standard Markdown, but not destructive replacement, broad ownership restructuring, or optional-index creation/material expansion.
9. Validate full unit and reconcile reactivated workspace through `skills/handoff.md`. Do not select another focus under this authorization.

A contextual implementation recommendation enters this same action when a compatible map exists. It supplies evidence for a candidate focus but bypasses neither proposal nor alignment rules.

## Action: Inspect Code Map

Inspection is read-only.

1. If no map was named, present already-discovered usable names in stable lexical order as the inspection choices; do not rescan/pre-read all maps.
2. Load selected `code_map.md` first.
3. Resolve selected source and alignment only when source-dependent claims/identity matter.
4. Load only the subsystem/API/namespace/manifest/symbol/identity facet needed.
5. Verify non-obvious behavior against actual source; map claims remain navigation, not authority.
6. Report missing, stale, mismatched, uncertain, or malformed data without mutation.

Inspection never normalizes files, updates identity metadata, or preserves context unless a separate action is authorized. Explicit **Inspect Map/Source Identity** uses this same read-only path with identity/alignment as the facet: read map identity, inspect source only enough for source/snapshot identity, keep source location/source identity/map identity/project/map store distinct, classify alignment, and report evidence/uncertainty/safe follow-ups. Do not write metadata to make inspection conclusive or invent a universal registry/schema.

## Action: Refresh Code Map

Use when represented source changed materially and mapped knowledge needs bounded reconciliation without broad replacement. May be human-requested or accepted from contextual maintenance after authorized project work changed represented source.

1. Resolve usable map, represented source, and workspace.
2. Establish bounded affected mapped concern. Reuse trustworthy change evidence from invoking work; do not rescan unrelated source merely to rediscover the reason.
3. Verify identity/alignment. Expected drift caused by the known change motivates refresh but does not make unrelated stale claims trustworthy.
4. Reuse/reactivate compatible workspace; apply Mapping Proposal Gate unless the same focus is already authorized through active-map continuation.
5. Refresh focus is the authorization boundary; discovery selects required standard Markdown changes within it.
6. Improve justified existing artifacts in place and update standard map-owned artifacts whose durable content changed. Preserve established ownership/structure unless restructuring is separately authorized.
7. Maintain already-present dependent lookup artifacts only as needed to keep contracted routing correct. No optional lookup/index creation/material expansion without separate gate.
8. Recheck representative usage when reusable caller/extension/lifecycle/ownership/persistence/serialization/event/tracking mechanics changed.
9. Validate and reconcile the complete refresh unit before another focus.

Routine bug fixes, private refactors, tests, cosmetic cleanup, and ordinary churn do not by themselves justify refresh. Bonsai does not continuously scan for drift or silently refresh after edits.

If work broadens useful coverage beyond prior scope, route that portion through **Extend Code Map**. If safe reconciliation requires substantial replacement, destructive removal, or broad ownership restructuring, route through **Rebuild Code Map**.

## Action: Rebuild Code Map

Rebuild replaces substantial generated representation and always requires its own explicit destructive gate. Selecting Rebuild, including from another lifecycle action, does not authorize mutation.

Before approval:

1. resolve/display every existing agent-owned target to replace/remove;
2. display every known preserved item, including calibration, supplied source, and other unowned files;
3. show source snapshot, map identity, rebuild scope, proposed replacement artifacts, ownership changes if any, and validation plan;
4. stop for explicit approval, revision, discussion, or cancellation.

After approval, replace only displayed agent-owned targets. Never delete the named source directory as a shortcut; never move, rename, modify, or delete supplied source. If safe replacement cannot stay within approved targets, stop with unowned content preserved.

## Action: Remove Code Map

Removal is destructive and always requires its own explicit gate.

Before approval:

1. inspect selected map without mutation;
2. resolve exact agent-owned paths to remove;
3. list preserved calibration, supplied source, and other unowned files separately;
4. report ownership ambiguity rather than inferring ownership from location;
5. show exact verification proving preserved files remain unchanged.

Load `skills/menu.md`; offer approval of exact removal set, revision, discussion, or cancellation; wait for explicit approval.

After approval, remove only displayed map-owned artifacts. Never recursively delete the named source directory. Verify preserved targets remain and no transient inspection data entered durable map store. Report map removed only when no usable agent-owned `code_map.md` remains.

## Mapping and Editing Rules

### Layer responsibilities

| Layer | Responsibility |
| --- | --- |
| `code_map.md` | Compact source identity, orientation, drill-down routing |
| `subsystems/<subsystem>/map.md` | One durable architectural domain, not folder/module inventory |
| `api_pub.md` | Optional decision-ready caller mechanics |
| `api_ext.md` | Optional decision-ready extension mechanics |
| `namespace_router.tsv` | Optional fuller namespace ownership routing |
| `manifest.tsv` | Optional compact subsystem/path registry; never sole identity proof |
| `symbol_index.tsv` | Optional selective high-value symbol routing; never exhaustive |
| workspace plan/state | Mapping continuation only, never another generated-map layer |

Do not duplicate one layer in another. Prefer durable navigation and recurring non-obvious mechanics over source extraction. Smaller reusable memory is better than comprehensive-looking output.

### Mapping focus and subsystem ownership

A generated subsystem requires demonstrated architectural responsibility, ownership boundary, lifecycle, data/execution concern, reusable API/extension surface, or another durable architectural domain. Directory, module, source root, package group, or human-selected focus is evidence, not automatic subsystem identity.

Prioritize owner-weighted, foundational, developer-facing, cross-boundary, widely reused, risky, or repeatedly misunderstood concerns. Deprioritize generated code, narrow helpers, leaf utilities, shallow inventories, obvious details, and non-representative examples.

Complete all standard architecture/API effects directly justified by the selected focus before selecting another. Do not force unrelated caller/extension analysis merely because an affected subsystem has other surfaces.

New human-selected focus or material scope expansion requires human direction. A newly justified subsystem/API map found while representing the existing focus does not.

Fresh-session boundaries should normally fall between bounded units. If a unit grows enough to reduce confidence/compression quality, finish and reconcile it when practical before the next focus. Do not deliberately split discovery from standard map production merely to create a session boundary.

### Evidence discipline

Use when claim status matters:

- **Observed:** directly confirmed from source, tests, examples, build files, or representative use.
- **Inferred:** reasoned from observed structure but not directly established.
- **Uncertain:** verification required before reliance.

Never overstate confidence. Correct stale content when authorized; otherwise expose mismatch/uncertainty.

### TSV discipline

For `namespace_router.tsv`, `manifest.tsv`, `symbol_index.tsv`:

1. preserve canonical header/column order;
2. use literal tabs between fixed columns;
3. one logical record per physical line;
4. no multiline cells, ad hoc columns, prose blocks, or tabs/newlines inside values;
5. terse notes;
6. after material edits, validate header, separators, and consistent column count.

Put detail that does not fit fixed shape in the appropriate Markdown layer.

### Compression and drift prevention

When an artifact grows, cut before adding:

- keep `code_map.md` startup-sized; move fuller namespace routing to optional TSV;
- keep subsystem maps architectural, not exhaustive;
- keep API maps focused on mechanics that prevent recurring mistakes;
- keep lookup tables selective and structurally boring;
- remove duplicated, stale, wrong-layer, obvious, or low-value content.

Routine maintenance must not structurally normalize an existing map. Template existence never justifies optional artifacts. Do not turn maps into project/session guides, API manuals, filesystem mirrors, prose indexes, or hand-maintained language-server databases.

## Agent Context During Mapping

Use `skills/agent_context.md` only for qualifying durable operational facts such as stable source checkout location, established source-selection rule, or reusable project-to-map association.

Do not store active project/map selection, transient extraction/inspection locations, speculative source identity, map workflow state, or map content in agent context. Context maintenance never broadens mapping authorization.

## Contextual First Use, Extension, and Refresh

Project implementation may surface map work at a natural boundary, but must not silently mutate reusable maps or expand source inspection merely to search for opportunities.

### First useful map

- Substantial existing source without a useful map may receive one contextual **Create Code Map** offer.
- If declined, return disposition to invoking workflow so creation moves under **See more options** rather than interrupting again in the same context. Create no placeholder map/state for a decline.
- Greenfield source with little stable structure receives no map pressure.

### Mapping opportunity discovered during project work

When already-authorized project inspection establishes reusable, non-obvious, architecturally significant knowledge not adequately mapped, Bonsai may recommend preserving it:

- no suitable map: recommend **Create Code Map**;
- compatible map missing the concern: recommend **Extend Code Map** with one bounded candidate focus;
- explain implicated source/map, focus, costly/non-obvious knowledge, and reuse value;
- use only evidence encountered during authorized project work; inspect no unrelated source to manufacture recommendations;
- combine closely related observations into one recommendation;
- recommendation alone does not create/mutate map, reactivate workspace, or change project scope;
- if declined/deferred, return disposition and do not repeatedly resurface the same recommendation during that work merely because it remains possible.

### Known map maintenance after source change

When authorized project work materially changed source represented by a known relevant map and mapped coverage is affected, Bonsai may recommend **Refresh Code Map**.

A known relevant map is already selected for the project, already loaded/used by current work, or cheaply identifiable from current source identity without surveying the map store.

- carry known change evidence and bounded affected concern into refresh proposal;
- do not enumerate/inspect every reusable map after routine edits;
- local/narrow bug fixes, private refactors, formatting, tests, and other changes that do not materially alter mapped knowledge do not trigger refresh;
- recommendation does not authorize mutation; accepted maintenance enters normal Refresh and bounded-unit flow.

Persist longer-lived source/selection rules only when they independently qualify under `skills/agent_context.md`.

## Transient Source Inspection

Inspect supplied archive directly when practical. If extraction/inspection workspace is needed:

- keep it outside durable map store;
- treat as disposable, non-authoritative working state;
- do not copy into a project merely to enable mapping;
- do not preserve in agent context or map data;
- remove/abandon it without modifying supplied source.

One archive's location never establishes a general source-location convention. Create/update/rebuild/removal must preserve supplied archives even when colocated with map artifacts.

## Completion Checks

Before reporting an authorized mapping unit or scope complete, verify:

1. `code_map.md` sufficiently identifies source for intended alignment and remains compact;
2. entry, subsystem, API, calibration, state, and lookup content remains in contracted layers;
3. each created/updated subsystem has demonstrated architectural responsibility and source-backed owning paths;
4. standard architecture/API layers directly implicated by selected focus were created, updated, or deliberately found unnecessary;
5. non-obvious claims are source-backed or visibly Inferred/Uncertain;
6. relative links and optional-artifact references match existing files;
7. every materially edited TSV has valid header, literal tabs, fixed column count, and one-line rows;
8. every generated-map mutation was inside selected focus's standard envelope or separately authorized;
9. no destructive work, ownership restructuring, optional-index creation, or material optional-index expansion occurred without required gate;
10. supplied source, every consulted calibration, and other unowned files remain unchanged;
11. no transient inspection state became durable map data;
12. map-wide roadmap, active scoped plan if any, and current resume state were reconciled through shared handoff;
13. only qualifying agent context was maintained through `skills/agent_context.md`.

If no real next focus/work remains in current scope, mark it complete rather than inventing more mapping.

## Completion and Invoking-Gate Return

After substantive active-map work:

1. report mapping unit, source, map identity, bounded result, changed map-owned files, checks actually performed, preserved unowned files, remaining uncertainty, and whether qualifying agent context changed;
2. reconcile `agent_plan.md`, `agent_state.md`, active scoped plan if any, generated output, and source/map identity through `skills/handoff.md`; reconcile qualifying agent context when applicable;
3. never silently revise human calibration, project final truth, or project execution memory;
4. let shared handoff present refreshed active-map completion, blocker, next-focus selection, or continuation gate;
5. do not also restore older repository-entry or **Manage Code Maps** gate after active workspace execution.

For cancellation, declined contextual offer, or non-mutating inspection that did not complete an active-map exact action, return control to retained invoking workflow. If a project is active, its owning workflow reconciles project execution state; if none, create none. Load `skills/menu.md` and re-present the refreshed invoking gate unless the mapping action created a required blocker/design/final-truth/review gate.

Do not silently end the parent workflow because mapping completed/cancelled. Do not silently select or execute another focus. A completed unit may surface concrete next-focus choices, but the human selects before another unit becomes authorized.

## Output Style

Use concise wording, exact paths, stable headings, explicit uncertainty, and no filler. Distinguish observation from inference. Never claim a source, map, identity, mutation, removal, or check that was not actually inspected or performed.
