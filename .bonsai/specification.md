# Bonsai Specification

**Version: 2.0.0**

Bonsai is a workspace-memory and execution-workflow system for AI-assisted software development. It
preserves the structured context an AI needs to design, build, inspect, map, and continue serious
software work across fresh sessions without making chat history authoritative.

Bonsai defines two resumable workspace types:

- **projects**: durable product/architecture truth plus implementation execution memory;
- **maps**: durable repository-local mapping execution memory that produces reusable generated
  source knowledge.

It supports simple repositories, multiple independent projects, long-running code mapping,
multi-repository source universes, reusable library/framework maps, reusable developer/agent
context, and frequent fresh sessions with small startup prompts.

Bonsai is not a general software-engineering methodology. Coding style, testing philosophy,
abstraction preferences, framework conventions, tooling choices, and similar engineering guidance
belong in developer/repository/source guidance or applicable skills unless they are approved project
requirements or architecture.

This document defines the Bonsai operating model. It is framework-authoring truth, not routine
implementation-session context. `README.md` owns human-facing usage guidance.

---

# 1. Authority and Framework Discovery

## 1.1 Specification authority

`specification.md` is the human-owned authoritative final truth for Bonsai. Standard prompts,
skills, templates, bootstrap files, helper scripts, category guides, README guidance, and workflow
behavior implement it; they are not peer authorities.

```text
specification.md    human-owned Bonsai final truth
    ↓
prompts/            standard entry workflows
    ↓
skills/             detailed triggered procedures
    ↓
templates/          workflow-consumed structures
```

When another standard artifact conflicts with this specification, this specification wins unless the
human explicitly revises it. Changes to Bonsai behavior, boundaries, ownership, lifecycle,
environment, workspace, mapping, or interaction models should be reflected here before or alongside
the implementing standard changes.

Detailed mechanics may remain in prompts/skills when repeating them here would add size without
adding specification value.

## 1.2 Progressive framework discovery

`specification.md` is the normal starting point for understanding or designing Bonsai changes. When
implementation-facing detail is needed, discover progressively:

```text
<bonsai-home>/specification.md
        ↓
category guide
        ↓
specific framework artifact
```

Category guides:

```text
<bonsai-home>/skills/skills.md
<bonsai-home>/prompts/prompts.md
<bonsai-home>/templates/templates.md
```

A category guide is a concise routing aid, not a peer authority or duplicate specification. It
identifies current artifacts and enough responsibility information to choose relevant ones. Normally
update a guide only when an artifact is added, removed, renamed, or materially changes
responsibility. Internal artifact changes do not require guide restatement.

For Web UI design of Bonsai changes, the human should normally provide the current
`specification.md` plus the proposed change/problem. The design agent uses it to identify
potentially relevant categories, then requests the applicable guide and specific artifacts as
needed. The human should not need to preload or know the entire standard. Unless intentionally
comparing versions, supplied guides/artifacts should resolve from the same Bonsai Home as the
specification.

Code maps are outside this category-guide mechanism; map/source context may be supplied separately
when relevant.

---

# 2. Core Operating Principles

## 2.1 Durable truth vs. working state

Project requirements/architecture describe the product and target system. Project/map plans and
state describe how selected work is being executed. Execution decisions must not casually become
durable project truth or reusable source truth.

## 2.2 Human-owned vs. agent-owned memory

For project, map-workspace, and context memory, human-owned artifacts normally use natural names;
agent-owned execution/operational memory uses `agent_` names.

```text
Human-owned: requirements.md, architecture.md, developer_context.md,
             icebox.md, map_calibration.md
Agent-owned: agent_plan.md, agent_state.md, agent_context.md
```

`agent_` means Bonsai may maintain or rewrite the artifact under its lifecycle rules. It does not
imply automatic loading. Generated code-map artifacts follow the mapping model's identities instead
of this naming convention.

## 2.3 Meaningful human control

Use explicit human gates for material approval, selection, revision, or resolution, not for every
internal execution detail.

Project gates may include detailed-plan approval, later phase planning approval when required,
durable contract review, final-truth clarification/revision, and material execution deviations. Map
work uses human gates only for real human decisions and does not inherit project phase, contract, or
final-truth gates merely because it shares workspace lifecycle. Routine agent-owned memory
maintenance needs no approval.

## 2.4 Keep simple work simple

A normal repository should not need a registry, dependency graph, generic workspace framework, or
elaborate configuration merely to use Bonsai. Add structure only when real work requires it.

## 2.5 AI sessions are primary

The canonical coding-agent startup is intentionally small:

```text
Read .bonsai/start.md and follow its instructions.
```

Shell helpers may improve convenience but are not the conceptual center.

## 2.6 Bootstrap resolves identity, not knowledge

Bootstrap establishes Bonsai Home, repository home, active workspace identity, and retained startup
request. It does not eagerly load every context file, map, skill, requirement area, architecture
subsystem, or mapping artifact. The implementation kernel loads knowledge after identity is known.

## 2.7 Cheap deterministic discovery

Use host tools, not model reasoning, for deterministic facts such as environment variables,
filesystem enumeration, project/map listing, and similar discovery when practical.

## 2.8 Durable discovery becomes agent memory

When an operational fact is durable, actionable, sufficiently supported, and likely to matter again,
preserve its current useful rule in the appropriate `agent_context.md`:

```text
discover → qualify → preserve actionable rule → reuse
```

Store the useful conclusion, not troubleshooting history.

## 2.9 Load context only when useful

Adding an artifact must not automatically add permanent context cost. Bonsai distinguishes
bootstrap, workflow-triggered, and facet-triggered context. Large/specialized artifacts should
normally load only when current work needs them.

## 2.10 Projects and maps are workspaces

Projects and maps both use:

```text
agent_plan.md
agent_state.md
```

Workspace type is structural: `.bonsai/projects/<name>/` is a project and
`.bonsai/maps/<name>/` is a map. Do not duplicate that identity in a workspace-local manifest.

Both support exact-next-step resumption, execution readiness, human gates when required,
current/fresh-session continuation, fresh-session one-step auto-execution, `Exit for now`, and
session-local active workspace identity.

The shared seam exists to eliminate duplicated lifecycle behavior, not to create a generic plugin
system. Do not generalize to arbitrary workspace types until a concrete third use case proves the
need.

## 2.11 Mapping is integrated but conceptually distinct

Code mapping is part of Bonsai. A long mapping effort may be durable, planned, and resumable. The
**code map** is the normal user-facing source-knowledge product; the **map workspace** is its
durable execution mechanism for create/extend/refresh/rebuild/resume.

Users should normally be able to say:

```text
Create a code map for this source.
```

Bonsai may create/reuse the required map workspace automatically. Explicit workspace management
remains available for deliberate preparation, standalone mapping, long-running
resumption/inspection, or independent scope/calibration management.

Generated maps describe a source universe/snapshot, not the project that created them. Project
context may inform mapping but does not define map identity. Bonsai must not knowingly reason from a
generated map representing an incompatible source version.

---

# 3. Environment Model

Bonsai separates the shared standard, reusable developer assets, repository-local workspace memory,
project truth, and reusable generated source maps.

## 3.1 Bonsai Home

The **Bonsai Home** is the standard used by the current session. Normally:

```text
BONSAI_HOME
```

identifies it.

Conceptual layout:

```text
$BONSAI_HOME/
├── specification.md
├── README.md
├── prompts/
│   ├── prompts.md
│   ├── implementation.md
│   ├── create_project.md
│   └── create_map.md
├── skills/
│   ├── skills.md
│   ├── artifact_index.md
│   ├── menu.md
│   ├── phase_execution.md
│   ├── dry_run.md
│   ├── handoff.md
│   ├── final_truth_update.md
│   ├── agent_context.md
│   └── code_maps.md
├── templates/
│   ├── templates.md
│   ├── plan_phase_template.md
│   └── icebox_template.md
├── developer_context.md        # optional reusable human-owned context
├── agent_context.md            # optional reusable agent-owned context
└── maps/
    ├── source-a/
    └── source-b/
```

Physical paths are host/environment dependent. Bonsai must not assume Unix `~`, Windows profile, WSL
home, or other home concepts are the same physical location. Multiple environments may point to one
physical Bonsai Home when practical.

## 3.2 Embedded Bonsai

If `BONSAI_HOME` is unavailable and repository-local `.bonsai` contains a valid embedded standard,
that directory may serve as Bonsai Home:

```text
repo/.bonsai = Bonsai Home + repository Bonsai memory
```

Embedded mode uses the same workspace semantics. When map-workspace memory and generated-map storage
physically overlap, their conceptual ownership remains distinct.

## 3.3 Repository home and local memory

The **repository home** is the source-repository root containing the local `.bonsai` anchor.
`.bonsai/start.md` establishes that anchor for normal AI sessions.

In Bonsai Home mode, repository-local `.bonsai` contains the small bootstrap plus
repository/workspace memory, not copies of the standard:

```text
repo/.bonsai/
├── start.md
├── developer_context.md                 # optional local human context
├── agent_context.md                     # optional local agent context
├── projects/<project>/
│   ├── requirements.md
│   ├── architecture.md
│   ├── agent_plan.md
│   ├── agent_state.md
│   ├── agent_context.md                 # optional project operational context
│   ├── icebox.md                        # optional
│   ├── plan/agent_plan_phase_<N>.md
│   ├── requirements/requirements_<AREA>.md
│   └── architecture/architecture_<SUBSYSTEM>.md
└── maps/<map>/
    ├── agent_plan.md
    ├── agent_state.md
    ├── map_calibration.md               # optional human input
    └── plan/                            # optional detailed map plans
```

## 3.4 Reusable developer material

Bonsai Home may hold cross-repository developer context, operational knowledge, source locations,
and generated maps. Their meaning remains distinct from repository/workspace memory even when
physically colocated.

---

# 4. Workspaces and Startup

## 4.1 Workspace model

A Bonsai workspace is a repository-local durable unit of resumable agent work. Exactly two concrete
structural types exist:

```text
project → repo/.bonsai/projects/<project>/
map     → repo/.bonsai/maps/<map>/
```

The containing `projects/` or `maps/` path is authoritative for workspace type. Do not create or
require a workspace-local manifest merely to restate type, name, routing, or standard type-specific
behavior; a file inside a workspace cannot override its structural type. Do not introduce a generic
repository-level `workspaces/` directory.

Every established workspace contains:

```text
agent_plan.md
agent_state.md
```

These shared execution-memory artifacts, together with the structural path, distinguish an
established workspace from a merely present directory. This matters especially in Embedded Bonsai,
where a generated-map directory may physically occupy `.bonsai/maps/<map>/` without yet being a
resumable map workspace.

`agent_plan.md` is the workspace-wide roadmap. `agent_state.md` is the current resume state.
Volatile progress, blockers, readiness, exact next action, and active detailed-plan identity belong
in `agent_state.md`; roadmap structure belongs in `agent_plan.md`. Workspace-specific sections may
extend those roles without changing ownership.

Standard project-vs-map loading/routing behavior belongs in the implementation kernel and triggered
skills, not duplicated inside each workspace.

## 4.2 Canonical startup

Every enabled repository has:

```text
.bonsai/start.md
```

Normal prompt:

```text
Read .bonsai/start.md and follow its instructions.
```

Natural-language qualifiers may be appended, for example:

```text
Active project: configuration-runtime.
Active map: niagara4.
Manage Code Maps.
```

No formal startup-command language is required.

`start.md` should remain small. It establishes environment identity, resolves an active workspace
when needed, derives workspace type from its structural path, verifies the selected workspace is
established, and hands control to the Bonsai Home or embedded implementation kernel.

Bootstrap responsibilities:

1. establish repository home from local `.bonsai`;
2. resolve Bonsai Home;
3. resolve active workspace type/name/path when applicable, with type derived from `projects/` or
   `maps/`;
4. verify the selected workspace directory and required shared execution-memory artifacts exist;
5. retain Bonsai Home, repository home, active workspace identity/path, and startup request as
   session context;
6. load `<bonsai-home>/prompts/implementation.md`;
7. continue under the standard implementation workflow.

Bootstrap does not routinely load requirements, architecture, generated maps, developer/agent
context, detailed plans, or specialized skills.

## 4.3 Bonsai Home resolution

Resolve in order:

1. valid `BONSAI_HOME`;
2. valid embedded standard in repository `.bonsai`;
3. otherwise ask the human to identify/configure Bonsai Home.

Do not broadly search the filesystem to guess an installation.

## 4.4 Workspace selection

Explicit human workspace identity is authoritative for the session:

```text
Active project: <project>.
Active map: <map>.
```

Selection is session-local and must not be persisted merely because one session chose it.
Workspace type comes from the selected structural path and is not separately declared or inferred
from workspace contents.

Without explicit identity, implementation may choose a deterministic conventional entry such as
an established `projects/main`, a sole established project, or another unambiguous repository
condition. It must not silently choose among several plausible workspaces.

---

# 5. Artifact Ownership and Durable Truth

Ownership controls durable meaning; it is separate from loading behavior.

## 5.1 Human-owned artifacts

Human-owned project/context artifacts use natural names. An AI may draft or mechanically maintain
them when instructed, but changes to durable meaning require human authorization.

Typical artifacts:

```text
requirements.md
architecture.md
developer_context.md
icebox.md
map_calibration.md
```

## 5.2 Agent-owned artifacts

Agent-owned project/context artifacts use `agent_` names and are actively maintained when current
truth changes:

```text
agent_plan.md
agent_state.md
agent_context.md
plan/agent_plan_phase_<N>.md
plan/agent_plan_<scope>.md
```

They describe current useful state, not a historical diary.

## 5.3 Standard, derived, and historical artifacts

Prompts, skills, templates, category guides, bootstrap files, and helper scripts are standard
framework artifacts. An implementation agent may mutate them only when an authorized Bonsai change
requires it and the resulting standard remains consistent with this specification.

Avoid genuinely ambiguous ownership. Ownership follows who controls durable meaning, not who types
the text. `icebox.md`, for example, remains human-owned because an observation is preserved there
only by human choice.

Semantic review artifacts under `review/` are derived workflow artifacts, not human final truth or
agent execution memory; their semantic filenames are part of the review model. Historical archives
preserve original artifact identities and do not rename copied artifacts merely to normalize names.

## 5.4 Project final truth

`requirements.md` is human-owned product truth: purpose, users, workflows, functional requirements,
product constraints, accepted product decisions, scope boundaries, and intentionally retained
unresolved product questions. It is not an implementation log.

`architecture.md` is human-owned target-architecture truth: approved boundaries, major components,
data/control relationships, and architectural constraints. Detailed architecture may be decomposed
into `architecture/architecture_<SUBSYSTEM>.md` when useful.

Implementation must not silently change durable project truth because source work reveals a
conflict; use the final-truth workflow.

## 5.5 Execution memory

For projects, `agent_plan.md` tracks implementation roadmap/phase progression. For maps, it tracks
map-wide roadmap, current scope, completed/pending mapping work, and scoped-plan locations. Keep it
roadmap-level.

`agent_state.md` stores the minimum durable resume truth, as applicable:

- current project phase or mapping scope;
- active detailed plan;
- execution readiness;
- blocker;
- exact next action;
- success condition;
- resume-critical references.

Replace stale state rather than append history.

Detailed project plans use `plan/agent_plan_phase_<N>.md`. Maps may use flat
`plan/agent_plan_<scope>.md`. A map scoped plan refines one bounded mapping unit; it is not a
project phase. Do not create nested map-plan directories merely because scope is large; use
additional flat peer plans when needed.

## 5.6 Developer context

`developer_context.md` is human-owned reusable working guidance: stable preferences, conventions,
local tooling instructions, and similar durable guidance. It is not product truth, cannot override
approved requirements/architecture, and is not the default destination for agent-discovered facts.

## 5.7 Agent context

`agent_context.md` is agent-owned operational memory. Suitable content includes reliable build/tool
invocations, tooling limitations, temporary-directory choices, runtime/filesystem constraints,
source/map locations, map-selection rules, environment-specific working rules, and other stable
facts learned through actual work.

Store current actionable knowledge, not troubleshooting history. Using an existing correct rule is
read-only consumption; do not rewrite/normalize the file merely because guidance was applied.

Agent context must not contain secrets and does not authorize software installation, machine
configuration changes, dependency changes, developer-context changes, or implementation/mapping
scope expansion.

Current blockers belong in active `agent_state.md`; durable lessons from resolving them may also
qualify for agent context.

Scopes:

```text
$BONSAI_HOME/agent_context.md
        +
repo/.bonsai/agent_context.md
        +
repo/.bonsai/projects/<project>/agent_context.md
        =
effective project operational context
```

More specific statements win. Store a discovered fact at the narrowest reusable scope. Active
project/map identity belongs in none of these; map-workspace identity/progress stays in map
execution memory.

### Project-to-code-map associations

A project may select useful reusable maps in project `agent_context.md`:

```text
Useful code maps:
- barcache
- tickerview
```

Code-map management should add/remove these selections without requiring future full-store
rediscovery. Association changes affect only project operational context; they do not create,
extend, refresh, rebuild, move, rename, or delete maps.

## 5.8 Context layering and lazy loading

Effective context is developer-level + repository-local + project-local when applicable; more
specific statements prevail. Bonsai needs no formal Markdown override language. Do not add layers
without demonstrated need.

Loading model:

- **bootstrap**: identity plus minimum state needed to determine what happens next;
- **workflow-triggered**: menus, planning, contract review, dry run, handoff, final-truth
  reconciliation, management, mapping;
- **facet-triggered**: maps, developer/agent context, deep architecture/requirements, detailed map
  plans, icebox observations.

The implementation kernel owns exact loading rules. Adding an artifact must not make every future
session more expensive.

---

# 6. Project and Map Creation

## 6.1 Project creation

Product/architecture design is a Bonsai capability but is often better done in a Web UI AI
conversation than in a coding CLI. Let design develop naturally; do not force templates prematurely.

When mature enough to preserve, use:

```text
<bonsai-home>/prompts/create_project.md
```

Initial synthesis produces a repository-root extractable package normally containing:

```text
.bonsai/
├── start.md
└── projects/<project>/
    ├── requirements.md
    ├── architecture.md
    ├── agent_plan.md
    └── agent_state.md
```

It may add project-local `agent_context.md`, `requirements/`, or `architecture/` when genuinely
warranted.

Before initial synthesis, resolve project name: use a supplied valid name; otherwise ask and suggest
`main` as the conventional default. Generated `.bonsai/start.md` is the canonical bootstrap for the
Bonsai version owning the workflow.

For an existing-project design update, preserve unambiguous project identity and package only
materially affected project files. Approved external source/map information identified during design
may seed project `agent_context.md`.

Project creation does **not** generate the initial detailed Phase 1 plan. Phase 1 planning remains
the first implementation gate.

## 6.2 Direct code-map creation

Normal coding-agent intent:

```text
Create a code map.
```

With an active project/repository, reuse established context instead of asking the human to restate
reliably known facts. Where unambiguous, derive defaults for current source location, source
identity/snapshot, map identity, initial mapping scope/focus, corresponding repository-local map
workspace, and optional active-project association. The human may override defaults.

If durable mapping needs a workspace, create or reuse the corresponding repository-local map
workspace as part of the approved mapping action. Reuse/resume a suitable existing workspace rather
than duplicate execution memory.

Conceptually:

```text
source selection
    ↓
map identity resolution
    ↓
create/reuse map workspace
    ↓
select bounded mapping focus
    ↓
execute bounded mapping unit
    ↓
generated reusable code map
```

Workspace creation is an implementation detail of the user's code-map intent, not a prerequisite the
user must perform separately.

## 6.3 Explicit map-workspace creation

For deliberate Web UI preparation/calibration, use:

```text
<bonsai-home>/prompts/create_map.md
```

This is useful when scope needs calibration, source is external to the current project, mapping is
substantial, or the human wants durable mapping memory before coding-agent execution.

Initial output normally contains:

```text
.bonsai/
├── start.md
└── maps/<map>/
    ├── agent_plan.md
    ├── agent_state.md
    └── map_calibration.md     # optional human-owned guidance
```

`plan/` may be created empty or later when needed.

This workflow must not generate reusable map outputs such as `code_map.md`, subsystem maps,
`namespace_router.tsv`, `manifest.tsv`, or `symbol_index.tsv`. Source remains authoritative. A map
workspace does not require a Bonsai project for that source.

---

# 7. Implementation, Readiness, Gates, and Session Boundaries

## 7.1 Implementation kernel

After bootstrap resolves session identity and verifies the selected workspace is established,
continue through:

```text
<bonsai-home>/prompts/implementation.md
```

The kernel:

1. receives Bonsai Home, repository home, active workspace type/name/path, and retained startup
   request;
2. loads minimum active workspace state;
3. determines exact next step and execution readiness;
4. routes by structural workspace type to project- or map-specific behavior;
5. loads additional project truth, generated maps, plans, context, or skills only as required;
6. identifies blockers/inconsistencies;
7. applies project final-truth classification when project final truth is implicated;
8. stops at the structured startup gate unless an explicit startup request authorizes the one exact
   next action after canonical state reconstruction;
9. executes only that authorized action; startup authorization never carries into a subsequent
   action;
10. reconciles completed work and workspace execution memory;
11. preserves qualifying operational discoveries;
12. when authorized project work materially changes source represented by a known relevant map,
    determines whether mapped coverage needs maintenance and surfaces one bounded maintenance action
    at a natural boundary;
13. when already-required source inspection reveals reusable, non-obvious, architecturally
    significant knowledge not adequately mapped, may surface one bounded mapping recommendation
    without expanding source inspection to hunt for opportunities;
14. reconciles framework category guides when authorized standard artifacts are added, removed,
    renamed, or materially change responsibility;
15. stops at the next natural gate.

For map work, one exact action may be an entire bounded mapping unit. Source discovery, ownership
resolution, standard map-layer updates, validation, and reconciliation inside that unit are not
separate authorization steps simply because they occur sequentially.

Project phase mechanics belong in project workflow/skills. Mapping mechanics and map/source identity
belong in mapping workflow and `skills/code_maps.md`.

Project implementation may propose mapping work but does not silently gain authority to mutate
reusable maps. Accepted recommendations route through the applicable map workspace and normal
bounded mapping-unit authorization.

A **known relevant map** is one already selected for the project, loaded/used in current work, or
cheaply identifiable from current source identity without surveying the full map store. Do not
enumerate every map after every source edit.

Mapping recommendations must arise from source already legitimately inspected for the current
authorized project action. Do not explore unrelated source merely to find mapping opportunities.

## 7.2 Execution readiness

Readiness must reflect the actual current gate. Common values include:

```text
Design required
Planning required        # or a more specific planning state
Awaiting review
Blocked
Ready to execute
Complete
```

`Ready to execute` means one safe exact agent-performable action is established and no independent
human-decision gate remains. For maps, that may be a complete bounded mapping unit established by a
selected focus.

`Complete` means the selected workspace scope has no unfinished required work and relevant durable
state is reconciled. Completing an intermediate step such as map discovery is insufficient.

## 7.3 Human gates and menus

Menus present choices; they do not own the workflow decisions shown. The invoking workflow remains
responsible for determining valid choices, validating selection, applying mutations, and reconciling
state.

Require a human gate for material approval, selection, revision, or resolution. Do not insert a gate
merely because execution discovered more detail inside an already-authorized bounded action. In
mapping, resolving exact standard generated-map targets within the selected focus/output envelope is
normally internal execution detail.

## 7.4 Shared continuation model

Bonsai preserves continuity across sessions but does not control the host application. It cannot
terminate, clear, reset, or create a chat/session; those remain human actions.

At a natural handoff, reconcile the active workspace and persist exact next action/readiness before
presenting continuation choices.

When one concrete agent-performable exact next action exists and no independent human-decision gate
is active, offer as contextually appropriate:

- execute it in the current session;
- continue in a fresh session that reconstructs canonical state and auto-executes that one action;
- review/change the next step;
- **Exit for now**.

This applies to project and map workspaces, including project planning or map planning/mapping when
the next action is durable and agent-performable. Required planning approvals still stop at their
gates.

For an executable map action, the exact next action may be one complete bounded mapping unit.
Fresh-session boundaries should therefore normally fall **between mapping units**, not between
discovery and generated-map production.

A mapping-unit authorization ends when that unit is reconciled or earlier at a real
blocker/mandatory gate. It does not authorize selection or execution of the next mapping focus.

`Complete`, blockers, design requirements, approvals, reviews, final-truth decisions, contracts, and
other mandatory gates are never bypassed by continuation. Neither current- nor fresh-session
continuation is inherently preferred.

A session just entered through fresh-session continuation should not immediately offer another
fresh-session continuation before substantive work. This is session-local interaction context, not
durable memory.

## 7.5 Ordinary resume and Exit for now

Ordinary resume always preserves the active workspace identity already known at handoff.

Project:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

Map:

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

Do not discard known project identity merely because startup could deterministically infer the same project.

**Exit for now** preserves the current durable execution condition and presents the applicable
ordinary startup pointer introduced by wording equivalent to:

```text
You can resume later with:
```

It carries no auto-execution authorization and neither approves, discards, executes, nor otherwise
resolves the action/gate. Do not change durable state merely to record that the human exited.

## 7.6 Fresh-session auto-execute

Fresh-session auto-execute always preserves the active workspace identity already known at handoff.

Project:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate. Active project: <project>.
```

Map:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate. Active map: <map>.
```

Do not omit project identity merely because startup could deterministically infer the same project.

The request must not embed rendered phase, mapping unit, pass, readiness, approval state, or
next-step text. The new session reconstructs canonical durable state and executes the one exact
action it establishes.

If a reconstructed map action is a ready bounded mapping unit, authorization covers the complete
unit, not only discovery. Authorization is not persisted and does not extend to a subsequent action.
If reconstruction finds a mandatory gate or no safe exact action, stop there.

---

# 8. Code Maps: Model, Storage, Inputs, and Lifecycle

Code maps are selective structural memory for source navigation. They are navigation aids, not
substitutes for source inspection and not project truth.

## 8.1 Lifecycle intents

- **Create**: establish a reusable map when no suitable map exists for the source identity.
- **Extend**: deliberately broaden useful coverage, such as another subsystem, cross-cutting
  concern, reusable caller, or extension surface. Reuse/reactivate the existing compatible map
  workspace; do not duplicate the map merely because scope expands.
- **Refresh**: reconcile mapped knowledge after material source change while normally preserving map
  identity and intended coverage.
- **Rebuild**: intentionally replace substantial generated representation. Destructive removal,
  broad ownership restructuring, or substantial replacement remains separately gated.

All intents use the same source-backed model. Once a bounded mapping focus is selected/authorized,
`skills/code_maps.md` executes the mapping unit.

## 8.2 Map store and identity

Active generated-map store:

```text
Bonsai Home mode: $BONSAI_HOME/maps/
Embedded mode:    repo/.bonsai/maps/
```

Each map has meaningful source identity. Folder names should be useful but need not encode every
identity detail forever; `code_map.md` may preserve richer identity. Version/revision distinctions
may be included when needed.

Map identity follows the source universe, not the creating project. Several projects using the same
repository source should normally consume one compatible map, not duplicate maps per project.

A map describes a particular source snapshot. Identity may include logical source name, version, Git
revision, artifact coordinates, source type, and exact source location, using the smallest
sufficient metadata. For released dependencies, matching released source may be preferable to an
unrelated development checkout; for active cross-repository work, an exact matching revision may be
preferable.

## 8.3 Mapping inputs

Actual source is authoritative.

When source belongs to a Bonsai project, relevant project memory may calibrate what
concepts/boundaries matter, including requirements, architecture, archaeological analysis, and
implementation knowledge. It never replaces source inspection.

Optional human-owned `map_calibration.md` may describe important concepts, representative entry
points, deeper/lightweight areas, extension points, misleading areas, and patterns worth
recognizing. It is not product truth, architecture truth, source evidence, generated output,
execution state, or map identity.

Project memory and calibration may both be used.

## 8.4 Workspace context vs. generated-map storage

Source context, repository-local mapping execution memory, and reusable generated-map storage are
distinct concerns.

For a selected repository checkout, source-local calibration may live at:

```text
<source-repository>/.bonsai/maps/<source>/map_calibration.md
```

It remains human-owned and must not be moved, copied, or rewritten merely because generated output
is stored elsewhere.

With an active Bonsai Home, reusable output belongs under:

```text
$BONSAI_HOME/maps/<map>/
```

Embedded mode may physically overlap workspace memory, calibration, and generated output without
merging their conceptual ownership.

Rule:

> Mapping execution uses source-local workspace context; reusable generated output uses the active
> Bonsai map store.

Source without a Bonsai project is fully supported:

```text
actual source + repo-local map workspace → mapping workflow → named reusable map
```

A map workspace alone is sufficient durable memory for a substantial standalone mapping effort.

## 8.5 Map entry document

`code_map.md` is the normal generated map entry document. It identifies the map and routes to
detailed map data. Index/manifest formats may evolve through use, but the source-identity boundary
is required.

---

# 9. Integrated Mapping Execution

Mapping uses the same startup, workspace, menu, context-layering, execution-memory, handoff, and
fresh-session model as projects where those concepts actually apply. It does not inherit unrelated
project-only semantics.

A mapping workflow must:

- resolve/create/reuse the applicable repository-local map workspace and make it active for mapping
  execution;
- use the active Bonsai generated-map store;
- identify source independently of any active project;
- use relevant project memory and source-local calibration when available;
- treat actual source as authoritative;
- organize substantive work as human-selected bounded mapping focuses;
- use optional flat scoped plans when a unit is too large for roadmap-level execution;
- preserve stable source locations/mapping rules in appropriate agent context;
- maintain map `agent_plan.md`/`agent_state.md` and exact-next-step resumability;
- reconcile generated output plus map/source identity before declaring current scope complete.

Retain existing useful generated navigation/index structures. Do not rewrite map data solely for
architectural neatness.

## 9.1 Bounded mapping unit

The normal executable mapping unit is established by a **human-selected bounded mapping focus**,
such as a subsystem, public/extension API concern, cross-cutting behavior, persistence, event
handling, serialization, lifecycle, tracking, or another bounded source-backed concern. Focus need
not map one-to-one to a generated subsystem.

Selection answers **what** the next unit is; continuation choice answers **where** that
already-selected unit executes:

```text
select focus
    ↓
persist exact next mapping unit
    ↓
choose current session / fresh session / review / exit
    ↓
execute complete unit
```

Selecting/reconciling a focus updates durable execution memory but does not itself begin substantive
source inspection or generated-output mutation.

Once the unit is executable and authorized, authorization normally covers:

```text
selected focus
    ↓
inspect authoritative source
    ↓
determine architectural ownership
    ↓
determine justified standard map layers
    ↓
create/update those layers
    ↓
validate against source
    ↓
reconcile agent_plan / agent_state
    ↓
stop at next mapping-unit boundary
```

Discovery and map production are normally one authorized action. Discovery may resolve exact
standard targets needed to represent the selected focus.

Normal non-destructive standard output envelope:

```text
code_map.md
subsystems/<subsystem>/map.md
subsystems/<subsystem>/api_pub.md
subsystems/<subsystem>/api_ext.md
```

A unit may update one or several existing subsystems, justify a new subsystem, or touch only some
standard layers. A cross-cutting focus may distribute durable knowledge across existing
architectural owners and require no same-named standalone subsystem.

No second human gate is required merely because discovery:

- resolves different standard targets than predictable beforehand;
- places one concern in several existing subsystem maps;
- justifies `api_pub.md` or `api_ext.md`;
- justifies a new subsystem inside the selected focus;
- shows that no standalone subsystem corresponds to the focus.

The selected focus remains the authorization boundary. Discovery resolves exact standard
destinations inside it.

Stop for human direction when work requires:

- material expansion of selected focus or source scope;
- materially different source/map identity;
- resolution of source/map misalignment;
- destructive rebuild/removal;
- restructuring existing generated-map ownership rather than ordinary updates;
- genuinely unrelated new mapping objective;
- a costly optional artifact;
- creation/material expansion of optional lookup/index artifacts;
- insufficient source evidence for safe mapping;
- another material decision requiring human judgment.

## 9.2 Extension and maintenance

A completed map is complete only for its current scope and represented source state; later
extension/maintenance may reactivate it.

An explicit coverage-expansion request reactivates the compatible workspace and establishes a new
bounded focus. The human may name a subsystem, cross-cutting concern, or ask Bonsai to review
current coverage and suggest valuable additions. A requested subsystem is a mapping focus, not an
instruction to blindly create a same-named directory/artifact; source discovery still determines
architectural ownership.

Material source change is a different trigger. When authorized project work changes source
represented by a known relevant map, surface bounded maintenance at a natural project boundary if
mapped knowledge is materially affected, including public/extension structure, lifecycle/ownership
behavior, reusable caller/extension mechanics, architectural relationships,
persistence/serialization/event/tracking contracts, or source identity/routing facts.

Do not trigger maintenance merely for routine local implementation edits, narrow bug fixes, private
refactors, formatting, or other changes that do not materially alter mapped knowledge.

Maintenance is not an incidental side effect of project source mutation. Project work
identifies/proposes the bounded map work; accepted maintenance executes through the normal map
workspace. Use knowledge already gained from the source change rather than rediscovering the entire
library just to assess maintenance.

## 9.3 Project-discovered mapping opportunities

Authorized project work may recommend map creation/extension when all are true:

- knowledge arose from source inspection already required for the authorized project action;
- it is source-level and useful beyond the current project-specific implementation;
- it is non-obvious enough that preserving it materially reduces future rediscovery;
- it is architecturally significant, cross-boundary, reusable, or otherwise valuable map content;
- it is not adequately represented by a useful current map.

The recommendation should identify source/existing map, proposed bounded focus, and why the
knowledge is reusable. Prefer extending a compatible existing map; otherwise use normal creation.

A recommendation does not authorize additional source exploration, map mutation, project-scope
expansion, or durable map/project state merely because the agent noticed an opportunity. If
accepted, route through normal map selection, mapping-unit authorization, and continuation. Combine
related observations and do not repeatedly interrupt with the same declined/deferred suggestion
during the same work.

## 9.4 Map-specific handoff

Map handoff reconciles as applicable:

- current mapping scope;
- completed/selected bounded focus;
- active detailed map plan;
- generated output touched by the completed unit;
- source/map identity concerns;
- whether generated output is sufficiently reconciled for that focus.

Source discovery alone is normally not a handoff boundary. If focus remains valid and evidence is
sufficient to determine justified standard layers, continue through production and validation before
reconciling at the mapping-unit boundary.

If useful work remains but no next bounded focus is selected, handoff presents concrete next-focus
choices and stops for human direction. Selecting the next focus changes durable map execution memory
but does not begin substantive source inspection or output mutation.

Map handoff must not invent project phase, pass, contract, or final-truth semantics.

---

# 10. Manage Code Maps

**Manage Code Maps** is Bonsai's user-facing code-map lifecycle surface. During ordinary project
implementation it generally appears under **See more options** unless mapping is directly relevant.

Primary operations:

- Create Code Map;
- Inspect Code Map;
- Extend Code Map;
- Refresh Code Map;
- Rebuild Code Map;
- Remove Code Map;
- Add a Code Map to the Active Project;
- Remove a Code Map from the Active Project;
- Manage Map Workspaces.

**Extend Code Map** broadens useful coverage. After map selection, choices may include another
subsystem, cross-cutting concern/reusable behavior, another public/extension surface, or review of
current coverage to suggest valuable additions. These select/derive a bounded focus; they do not
prescribe generated filesystem structure.

**Refresh Code Map** is the normal non-destructive source-change reconciliation path and should use
the narrowest source-backed maintenance focus that restores trustworthy coverage.

**Rebuild Code Map** is for cases where extension/refresh is insufficient and substantial
replacement or ownership restructuring is intended; destructive/broad restructuring gates remain in
force.

Map-workspace operations are secondary. **Manage Map Workspaces** may offer Create, Inspect, and
Resume Map Workspace.

## 10.1 Context-aware create/extend

When Create/Extend is invoked from an active repository/project, prefer known session context over
re-asking. Where reliably derivable, present/use defaults for current repository source location,
logical source identity, source snapshot, map identity, corresponding local map workspace,
initial/expanded scope, initial bounded focus, and optional active-project association for new maps.
Human overrides remain allowed.

Approval authorizes the selected mapping focus plus standard generated-output envelope, not a
precomputed list of exact Markdown files. Creating/reactivating the required map workspace is part
of the same approved action and does not require a redundant workspace gate.

Extending a compatible map reuses its identity and preserves existing generated output unless
destructive replacement/restructuring is separately authorized.

## 10.2 First use

For a substantial existing codebase without a useful map, Bonsai may surface map creation once as a
primary contextual action. If declined, leave mapping under **See more options** rather than
repeatedly interrupting. Normally defer mapping for greenfield repositories with little useful
source.

## 10.3 Contextual maintenance/recommendations

When authorized project work materially changes source represented by a known relevant map, surface
a concise maintenance recommendation at the next natural project boundary rather than knowingly
leaving the map misleading. Identify the map and bounded refresh area; offer current-session
execution, fresh-session continuation, focus review/change, or deferral. Recommendation alone does
not authorize map mutation.

When already-required project source inspection reveals reusable, non-obvious knowledge not
adequately mapped, Bonsai may recommend create/extend. State the implicated source/map, bounded
focus, expensive/non-obvious knowledge, and why preserving it helps future work. Do not inspect
unrelated source to manufacture recommendations. If declined/deferred, continue the project without
mutation and do not repeatedly resurface the same suggestion during the same work.

Accepted maintenance/recommendations enter the normal map workflow and `skills/code_maps.md`.

## 10.4 Project associations and map collections

Project map associations live in project `agent_context.md` and do not mutate generated maps.

Discover map workspaces from:

```text
repo/.bonsai/maps/
```

Discover reusable generated maps from the active Bonsai map store. These collections are distinct
even when Embedded Bonsai physically overlaps them.

---

# 11. Multi-Repository Source Universes and Archaeology

A project may depend on external source:

```text
application → library-a → library-b
```

Each repository may have its own Bonsai project memory, while generated maps remain reusable
developer assets under the active map store, for example:

```text
$BONSAI_HOME/maps/
├── application/
├── library-a/
└── library-b/
```

When external source is needed, Bonsai may use durable agent context, dependency information, map
identity, and source inspection to locate matching source/map. Preserve stable cross-repository
source locations/working rules in the appropriate agent context so sessions do not repeatedly
rediscover them. Do not duplicate machine-specific source paths into consuming-project
requirements/architecture.

Existing software may require archaeological work before design/implementation. Archaeology may
inspect source structure, runtime behavior, durable contracts, tests, extension points,
architectural relationships, and previous implementation decisions. Its output is supporting
analysis, not automatically product/architecture truth. Useful findings may later inform
requirements, architecture, plans, maps, or agent context according to the kind of truth discovered.

---

# 12. Standard Prompts, Skills, and Templates

Detailed workflow behavior belongs in triggered artifacts rather than a permanently loaded
monolithic prompt.

## 12.1 Prompts

Standard entry workflows live under:

```text
<bonsai-home>/prompts/
```

with category guide `prompts/prompts.md`.

The prompt set should remain small.

- `prompts/implementation.md`: stable workspace-aware kernel/router. Receives session identity from
  `.bonsai/start.md`, loads minimum additional context, may surface map maintenance/opportunities
  from source already required by project work, and routes accepted map work to
  `skills/code_maps.md`. It does not roam through source looking for mapping opportunities.
- `prompts/create_project.md`: Web UI project synthesis/bootstrap packaging into
  `.bonsai/projects/<project>/` plus canonical `.bonsai/start.md` for initial synthesis.
- `prompts/create_map.md`: Web UI map-workspace synthesis/bootstrap packaging into
  `.bonsai/maps/<map>/`; may synthesize `map_calibration.md`; never generates reusable map output.

## 12.2 Skills

Detailed triggered procedures live under:

```text
<bonsai-home>/skills/
```

with category guide `skills/skills.md`.

Skills are standard files, not workspace memory. Typical responsibilities:

- `artifact_index.md`: maintain `skills/skills.md`, `prompts/prompts.md`, and
  `templates/templates.md` when corresponding standard artifacts are added, removed, renamed, or
  materially change responsibility. Add/remove/reconcile references, validate resolution, detect
  missing relevant artifacts, and keep descriptions concise/responsibility-oriented. Do not
  duplicate specifications/procedures. Category-guide reconciliation is part of completing the
  authorized lifecycle change. This skill does not own code-map discovery/lifecycle indexing.
- `skills/phase_execution.md`: project phase execution only; never apply merely because maps share
  plan/state/handoff/fresh-session lifecycle.
- `skills/final_truth_update.md`: project final-truth clarification/revision; not a routine map
  lifecycle step unless map work actually implicates project final truth.
- `skills/handoff.md`: shared workspace handoff plus workspace-specific reconciliation where
  applicable.
- `skills/agent_context.md`: qualification, layering, maintenance, and project map associations.
- `code_maps.md`: map-workspace execution, source inspection, create/extend/refresh/rebuild,
  generated output/maintenance, map/source identity, validation, and map-specific completion. It
  owns execution after accepted project mapping recommendations.

## 12.3 Templates

Templates live under:

```text
<bonsai-home>/templates/
```

with category guide `templates/templates.md`.

Create a template only when an explicit Bonsai workflow consumes it, not because a document type
could theoretically be templated.

For generated code maps, template existence does not authorize output. Standard Markdown map
artifacts may be generated when justified inside an authorized mapping unit. Optional lookup/index
artifacts remain separately gated when creation/material expansion is costly or unnecessary by
default.

---

# 13. Optional Helpers and Repository Enablement

## 13.1 Optional helper scripts

Bonsai may provide small shell/host helpers for convenience, for example:

```text
bonsai.sh init
bonsai.sh --list
bonsai.sh <project>
```

A helper may create initial `.bonsai/start.md`, create conventional `projects/main`, list projects
without AI, or launch a configured coding CLI with a Bonsai prompt. Helpers are optional; the
underlying capabilities must remain understandable from the AI workflow. Once a Bonsai session is
running, routine implementation, project switching/listing/creation, and map management must not
depend on helpers.

## 13.2 Enabling a repository

A repository becomes Bonsai-enabled when it has:

```text
.bonsai/start.md
```

plus project-memory area when project memory is needed. Conventional simple structure:

```text
.bonsai/
├── start.md
└── projects/main/
```

The Web UI project synthesis workflow may create bootstrap plus initial project memory as one
repository-root extractable package. A helper or manual distribution copy may also create the
bootstrap. Creating only the local anchor/project memory does **not** create an Embedded Bonsai
standard. Enabling a repository does not approve or invent product design.

---

# 14. File Maintenance Discipline

- **Specification:** `specification.md` is human-owned Bonsai final truth; all standard artifacts
  and README guidance conform to it.
- **Category guides:** after an authorized standard prompt/skill/template is added, removed,
  renamed, or materially changes responsibility, reconcile the corresponding guide through
  `skills/artifact_index.md` before completion. Keep guides concise and non-duplicative.
- **Project final truth:** do not silently redefine `requirements.md`, `architecture.md`, or layered
  final-truth documents. Clarification/revision requires human authorization.
- **Execution memory:** actively maintain `agent_plan.md`, `agent_state.md`, and applicable detailed
  plans when their current truth changes; replace stale state rather than append history.
- **Agent context:** preserve only durable, actionable, sufficiently supported operational facts
  likely to matter again; omit transient failures/troubleshooting noise.
- **Icebox:** update `icebox.md` only when the human chooses to preserve an observation.
  Preservation does not authorize implementation.
- **Maps:** refresh when material structural changes affect represented knowledge; extend for later
  valuable concerns outside current scope. Routine local edits need not trigger maintenance. Project
  source mutation may surface bounded maintenance but does not authorize map mutation. Natural
  discovery of valuable unmapped reusable knowledge may surface a mapping recommendation, but must
  not broaden source inspection merely to find one. Maintain trustworthy map/source identity. Within
  an authorized bounded unit, discovery may choose exact standard map targets inside the standard
  envelope without prior path-by-path approval.

---

# 15. Clean Rebuild Objective

Project memory should describe the target system and current execution reality, not every historical
detour. A mature project should support clean rebuild from useful durable memory.

Preserve:

- final requirements;
- final architecture;
- useful roadmap structure;
- current execution state;
- durable operational knowledge;
- useful maps.

Discard/replace:

- obsolete pivots;
- stale session history;
- resolved blockers;
- superseded execution state;
- troubleshooting history;
- temporary scaffolding;
- accidental implementation scars that no longer describe the target system.

---

# 16. Typical Working Rhythm

## 16.1 Project

1. Enable repository with `.bonsai/start.md`.
2. Explore product/architecture in Web UI AI.
3. Use `prompts/create_project.md` to synthesize durable project memory.
4. Save under `.bonsai/projects/main/` or a named project.
5. Start with `Read .bonsai/start.md and follow its instructions.`
6. Plan/review current phase when required.
7. Execute the exact authorized next action.
8. Reconcile execution memory at natural boundaries.
9. If work materially affected a known map, address the bounded maintenance recommendation; if
   already-required source inspection revealed valuable reusable unmapped knowledge, optionally act
   on the mapping recommendation.
10. Continue current session, use fresh-session one-step continuation, review/change the next step,
    or exit.
11. Preserve qualifying durable operational discoveries in agent context.
12. Complete only when approved project scope is implemented and reconciled.

## 16.2 Map

1. From the source repository, choose Create/Extend/Refresh Code Map or resume an existing map
   workspace.
2. Let Bonsai derive unambiguous source location, source identity, and map identity; review/override
   when needed.
3. Create/reuse/reactivate required repository-local map workspace and make it active.
4. Use `agent_plan.md` as map-wide roadmap.
5. Select one bounded focus appropriate to lifecycle intent.
6. Reconcile that focus into roadmap/state as the exact next unit without changing generated output.
7. Choose current-session continuation, fresh-session continuation, review/change, or **Exit for
   now**.
8. Execute the complete unit: inspect source, determine ownership, resolve/update justified standard
   layers, validate, reconcile workspace state.
9. Add flat scoped plans only when a unit is too large for roadmap-level execution.
10. At the next mapping-unit boundary, select another bounded focus rather than automatically
    entering unrelated work.
11. Mark complete only when current scope is exhausted and generated output/source identity are
    reconciled.
12. Later reactivate the same workspace for extension, source-change maintenance, or an accepted
    project-discovered recommendation.

For mapping needing deliberate preparation/calibration before coding-agent execution, use
`prompts/create_map.md` first.

---

# 17. Validation Cases

The standard should validate at least these behaviors. These are behavioral expectations, not a
mandate for a particular test harness.

## Workspace startup

1. A normal `projects/main` repository starts with `Read .bonsai/start.md and follow its
   instructions.`
2. Explicit named project resolves that project workspace.
3. `Active map: <map>` resolves an established `.bonsai/maps/<map>/` as a map workspace from its
   path and shared execution memory without requiring a workspace manifest.
4. Active workspace identity remains session-local and is not written to `agent_context.md`.
5. Startup does not eagerly load full project truth, full generated maps, or detailed map plans.

## Shared handoff

6. Executable project exact-next-step offers current-session and fresh-session one-step
   continuation.
7. Executable map exact-next-step offers the same semantics.
8. Project auto-execute reconstruction does not bypass project gates.
9. Map auto-execute reconstruction does not bypass real human gates/blockers.
10. `Exit for now` changes no durable state merely because the human exits.
11. Project resume and fresh-session prompts include explicit `Active project: <project>`.
12. Map resume and fresh-session prompts include explicit `Active map: <map>`.

## Map planning

13. Small map may execute entirely from `agent_plan.md`.
14. Large mapping unit may create `plan/agent_plan_<scope>.md`.
15. Larger sub-scope may create another flat scoped plan; no nested plan directories.
16. `agent_state.md` identifies active detailed plan and exact next step.
17. Detailed map plans do not become project phases or automatically create phase-review gates.

## Map storage and ownership

18. Map-workspace execution memory remains repository-local.
19. Reusable generated map output remains in the active map store.
20. Embedded Bonsai may physically overlap those locations without confusing roles; generated map
    output alone does not establish a resumable map workspace without shared execution memory.
21. Legacy generated-map state is absent from the active execution model; map
    `agent_plan.md`/`agent_state.md` own continuation.
22. `map_calibration.md` remains human-owned input, not execution state.

## Project-map associations

23. A project can add/remove useful map selections in project `agent_context.md`.
24. Association changes do not rebuild, move, or delete generated maps.
25. Future project sessions can use selections without rediscovering the full map store.

## Creation workflows

26. `create_project.md` creates project memory under `.bonsai/projects/<project>/` plus repository
    bootstrap for initial synthesis; the path establishes project workspace type.
27. `create_map.md` creates `agent_plan.md`, `agent_state.md`, optional `map_calibration.md`, and
    repository bootstrap under `.bonsai/maps/<map>/`; the path establishes map workspace type.
28. `create_map.md` does not generate `code_map.md`, subsystem maps, or lookup tables.

## Code-map creation interaction

29. Create Code Map may create/reuse the corresponding local map workspace as part of the same
    approved map action.
30. Automatic workspace creation preserves existing generated output, calibration, supplied source,
    and unknown colocated files.
31. A partial or ownership-ambiguous same-name workspace blocks automatic repair/overwrite.
32. A newly usable map may be associated with the active project only when that association was part
    of the approved action or separately selected later.

## Map completion/reactivation

33. Map completion requires exhausted current scope plus reconciled generated output/source
    identity.
34. Completing a scoped map plan returns to the map-wide roadmap, not a project-style phase
    transition.
35. A completed map workspace may reactivate for real source change, explicit maintenance, or
    expanded scope without destroying prior generated output.
36. Handoff does not write project phases, passes, contracts, project final-truth state, icebox
    state, active workspace identity, or session history into map memory.

## Mapping-unit authorization

37. Selecting a bounded focus updates durable map execution memory without substantive source
    inspection or generated-output mutation.
38. Once the focus is one executable exact-next-action, current/fresh continuation authorizes the
    complete mapping unit, not discovery alone.
39. Source discovery may resolve exact standard Markdown targets without another gate.
40. A cross-cutting focus may update standard layers in several existing subsystems without a
    same-named standalone subsystem.
41. Discovery may justify `api_pub.md`, `api_ext.md`, or a new subsystem map inside the selected
    focus without second approval merely because paths were unpredictable.
42. Material source-scope expansion, materially different source/map identity, destructive work,
    generated-map ownership restructuring, unrelated mapping work, or insufficient evidence stops at
    the applicable human gate.
43. Creating/materially expanding optional lookup/index artifacts remains separately gated and is
    not silently absorbed into standard mapping output.
44. Mapping handoff normally follows generated-map production/validation, not discovery, unless
    discovery reaches a blocker/mandatory human decision.

## Extension, maintenance, and project recommendations

45. Extend Code Map reuses/reactivates the existing compatible workspace and does not duplicate a
    map merely because coverage expands.
46. A request to map another subsystem becomes a bounded focus; discovery determines justified
    architectural ownership rather than blindly creating a same-named artifact.
47. A human may request a cross-cutting focus or ask Bonsai to review current coverage and suggest
    additions before selecting the next unit.
48. When Bonsai materially changes source represented by a known relevant map during authorized
    project work, it surfaces bounded maintenance at a natural project boundary when mapped
    knowledge is affected.
49. Routine private implementation changes that do not materially alter mapped knowledge do not
    trigger maintenance merely because files changed.
50. If required project work establishes reusable, non-obvious, architecturally significant source
    knowledge that is inadequately mapped, Bonsai may recommend map creation/extension.
51. Project implementation does not inspect unrelated source merely to seek mapping opportunities.
52. A maintenance/opportunity recommendation does not mutate maps or silently expand project scope
    before human acceptance.
53. Accepted maintenance/recommendation enters the normal map-workspace/bounded-unit workflow and
    may use current/fresh-session continuation.
54. Combine closely related mapping observations; do not repeatedly resurface a declined/deferred
    suggestion during the same work merely because it remains possible.
55. Refresh preserves intended map identity/coverage where possible; rebuild remains separately
    gated for destructive replacement or broad ownership restructuring.
