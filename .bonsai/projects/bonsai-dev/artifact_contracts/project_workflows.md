# Artifact Contracts — Project and Context Workflows

**Project:** `bonsai-dev`  
**Status:** Seeded; Phase 1 archaeology required before implementation

> **Staging note:** Target standard artifacts are implemented under `bonsai/` during the refactor and become runtime `.bonsai` / Bonsai Home artifacts after promotion. The `bonsai-dev` project itself remains on Bonsai 1.4 execution-memory filenames until that promotion.


## Artifact: `bonsai/prompts/create_project_memory.md`

**Classification:** Adapt from `.bonsai/design_session.md`

### Role

Synthesize a mature Web UI design conversation into durable Bonsai project memory without forcing the design discussion itself into templates prematurely.

### Loaded when

The human decides a design conversation is mature enough to preserve as Bonsai project memory.

Primarily a Web UI workflow.

### Inputs

- current design conversation;
- relevant supplied source/design artifacts;
- explicit project name when a named project is intended;
- otherwise conventional project name `main`.

### Responsibilities

- synthesize the conversation into human-owned requirements and architecture;
- initialize agent-owned roadmap and resume state;
- create deeper requirement/architecture documents only when useful;
- optionally seed project-level `agent_context.md` from human-approved operational information such as known useful external maps;
- produce a zip rooted at `.bonsai/projects/<project>/`;
- keep target design separate from implementation history;
- explicitly leave detailed Phase 1 planning for the implementation workflow.

### Must not

- force the human to fill templates during exploratory design;
- manufacture architecture merely to make documents look complete;
- generate the detailed initial Phase 1 plan;
- turn unresolved design uncertainty into invented final truth;
- copy chat history into durable memory;
- treat operational map/source paths as product requirements or architecture.

### Reads

The mature conversation and any explicitly relevant supplied artifacts.

### Writes / Output

Normally:

```text
.bonsai/projects/<project>/
    requirements.md
    architecture.md
    agent_plan.md
    agent_state.md
```

Optionally:

```text
agent_context.md
requirements/requirements_<AREA>.md
architecture/architecture_<SUBSYSTEM>.md
```

Output is normally a zip suitable for extraction at repository root.

### Delegates to

No coding-agent implementation workflow.

Its output intentionally sets execution readiness so Phase 1 planning is the first implementation gate.

### Human gates

Blocking clarification only when the durable design cannot be synthesized safely from the conversation.

The generated final truth remains human-owned.

### Preserve from existing version

The existing `design_session.md` contains substantial learned synthesis behavior that Phase 1 must inspect, especially:

- distinguishing new project synthesis from existing-project design updates;
- asking only blocking clarifications before synthesis;
- resolving module-boundary ambiguity when it materially affects architecture;
- keeping product requirements and implementation architecture distinct;
- avoiding speculative architecture;
- keeping top-level documents orienting and using deeper layered truth only when useful;
- initializing roadmap/state without pretending Phase 1 is already planned;
- preserving accepted decisions and exclusions;
- producing independently usable durable documents rather than chat summaries.

### v2 changes

- rename from design-session framing to project-memory creation;
- use v2 ownership names `agent_plan.md` / `agent_state.md`;
- default output root is `.bonsai/projects/main/`;
- project-level `agent_context.md` may be seeded with approved map/source operational information;
- output protocol is a zip;
- initial detailed Phase 1 plan remains absent.

### Validation cases

- simple greenfield project;
- project with deep subsystem architecture;
- design using external `barcache` and `tickerview` maps;
- named project request;
- unresolved design that requires clarification;
- no unnecessary layered documents.

---

## Artifact: v2 phase-plan template

**Existing source:** `.bonsai/templates/plan_phase_template.md`  
**Target source path:** expected under `bonsai/templates/`, exact filename to follow the specification's runtime name  
**Classification:** Adapt

### Role

Provide the reusable structure used by phase execution when a detailed phase plan is actually warranted.

### Loaded when

Only when drafting a new detailed phase plan.

### Responsibilities

- capture objective, scope, approved boundaries, contract surfaces, ordered work, validation, risks, and completion criteria;
- represent single-pass and two-pass modes correctly;
- make contract review explicit only when warranted;
- preserve current execution detail without bloating `agent_plan.md`;
- include maintenance rules that keep `agent_state.md` and roadmap state aligned.

### Must not

- force Pass A/Pass B on single-pass phases;
- require invented abstractions;
- imply phase plans are final product/architecture truth;
- require a phase plan merely because a phase touches multiple files.

### Preserve from existing version

Especially preserve:

- native contract review surface;
- compiling Pass A code-contract source;
- behavior tests may be disabled/failing until implementation when planned;
- test plumbing can change without semantic contract review;
- human review focus;
- explicit out-of-scope/do-not-do-yet;
- completion summary compression;
- active plan correction when stale.

### v2 changes

Use `agent_plan.md`, `agent_state.md`, and `agent_plan_phase_<N>.md` naming.

---

## Artifact: v2 icebox template

**Existing source:** `.bonsai/templates/icebox_template.md`  
**Target source path:** expected under `bonsai/templates/`  
**Classification:** Mostly Keep

### Role

Instantiate `icebox.md` only after the human chooses to preserve an out-of-scope observation.

### Loaded when

The first observation is explicitly authorized for preservation or when a new entry needs the template's structure.

### Responsibilities

- preserve compact, independently understandable deferred observations;
- make status and possible destination explicit;
- distinguish preservation from approval to execute;
- support pruning/promoting/superseding as current truth changes.

### Must not

- auto-create an empty icebox;
- become a bug/technical-debt dump;
- become requirements, architecture, roadmap, or execution authority;
- preserve rejected/superseded history merely for completeness.

### Preserve from existing version

The v1 template's human-triaged, non-authoritative semantics should survive nearly unchanged.

### v2 changes

The old template labels itself agent-maintained while the v2 specification defines `icebox.md` as human-owned because the human controls durable meaning. The contract and template must be reconciled to v2 ownership without losing agent-assisted mechanical maintenance.

---

## Required v2 behavior: Project Management

**Classification:** Missing / responsibility seam not yet assigned

### Required role

Support:

- List Projects;
- Switch Project;
- Create Project.

### Required behavior

- project listing uses cheap deterministic directory enumeration;
- explicit project request is authoritative for the session;
- `projects/main` is the conventional default;
- switching affects current session only;
- creating a project creates memory location but does not invent requirements/architecture;
- if durable design is missing, execution readiness becomes `Design required`;
- workflow normally lives under **See more options**;
- subordinate workflow returns to the invoking gate with refreshed active-project state.

### Must not

- write a repository-wide mutable current-project pointer;
- treat `main` as an alias;
- use model reasoning for simple project-directory enumeration.

### Phase 1 decision required

Determine whether this behavior belongs in a dedicated skill or remains a small workflow routed by the implementation kernel plus menu skill.

Do not create a new permanent artifact solely because a contract table wants a path.

---

## Required v2 behavior: Create Bonsai Home

**Classification:** Missing / responsibility seam not yet assigned

### Required role

Create and populate a reusable Bonsai Home from an embedded Bonsai environment.

### Required behavior

- require `BONSAI_HOME` to already be defined;
- allow the target directory not to exist;
- create/populate the target when authorized;
- preserve repository-local project memory;
- make Bonsai Home the preferred standard when both it and embedded standard are valid;
- explain any remaining environment setup;
- normally be reachable under **See more options** or by explicit startup request.

### Must not

- ask for a one-session path as a substitute for `BONSAI_HOME`;
- store Bonsai Home location in agent context as discovery fallback;
- silently modify shell startup files, machine configuration, or other developer-owned environment configuration.

### Phase 1 decision required

Assign the workflow to the smallest appropriate standard artifact after core routing/menu responsibilities are extracted.

---

## Required v2 behavior: Developer Context Layering

**Classification:** Adapt from v1 repository-only developer context

### Required role

Apply durable developer/team guidance without confusing it with product truth or agent-discovered operational memory.

### Required scopes

```text
$BONSAI_HOME/developer_context.md
repo/.bonsai/developer_context.md
```

Project-local developer context is not currently part of the v2 specification.

### Required behavior

- load when the current facet needs developer guidance;
- repository-specific statements override broader developer-level statements when they conflict;
- developer context does not override approved requirements or architecture;
- agent discoveries are not silently copied into developer context.

### Phase 1 decision required

Determine whether loading/layering belongs entirely in the implementation router or needs a reusable context skill distinct from `agent_context.md`.
