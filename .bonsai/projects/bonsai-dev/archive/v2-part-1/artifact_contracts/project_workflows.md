# Artifact Contracts — Project and Context Workflows

**Project:** `bonsai-dev`  
**Status:** Approved; Phase 1 project/context archaeology complete

> **Identity and placement:** Standard-artifact identities are relative to the Bonsai standard root. During this
> refactor, candidate artifacts are staged at `repo/bonsai/<artifact-identity>`; shared runtime artifacts resolve
> from `<bonsai-home>/<artifact-identity>`, and Embedded Bonsai uses `repo/.bonsai/` as its standard root. The
> `bonsai-dev` project itself remains on Bonsai 1.4 execution-memory filenames until promotion.

## Archaeological Evidence

### Project-memory synthesis

| Evidence ID | Source evidence | Specification rule | Classification and rationale | Owning contract | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `PROJECT-MEMORY-01` | `.bonsai/design_session.md` — **Purpose** and **Synthesis Rules** turn a mature conversation into durable memory rather than a transcript or generic engineering prescription. | **Project-Memory Creation Workflow**; **Simple projects should stay simple**. | **Keep** — conversational design remains primary and synthesis preserves only approved durable meaning. | `prompts/create_project_memory.md` | A mature conversation produces independently usable project truth and execution memory with no chat-summary filler or invented conventions. |
| `PROJECT-MEMORY-02` | `.bonsai/design_session.md` — **Output Protocol** requires four core documents and permits layered final truth only when justified. | **Project-Memory Creation Workflow**. | **Adapt** — retain conditional layering, but use v2 `agent_` names and zip output rooted at the selected project. | `prompts/create_project_memory.md` | A simple project contains only the four required files; a genuinely deep design adds only the warranted layered files. |
| `PROJECT-MEMORY-03` | `.bonsai/design_session.md` — **Existing-Project Design Updates** uses supplied final truth as baseline and updates only materially affected files. | **Project Final Truth**; **Final-truth impact**; **Clean Rebuild Objective**. | **Keep** — existing-project design updates remain useful and must not turn into implementation execution. | `prompts/create_project_memory.md` | An update preserves unaffected files, changes affected final truth only, and includes roadmap/state only when reconciliation is required. |
| `PROJECT-MEMORY-04` | `.bonsai/design_session.md` — **Blocking Clarifications Before Synthesis** asks only for materially implementation-shaping foundations and refuses vague defaults. | **Project-Memory Creation Workflow**; **Human control should not require constant babysitting**. | **Keep** — clarification is required only when durable synthesis would otherwise guess a consequential decision. | `prompts/create_project_memory.md` | A missing runtime or required dependency boundary blocks synthesis; an ordinary style preference does not. |
| `PROJECT-MEMORY-05` | `.bonsai/design_session.md` — **Blocking Clarifications Before Synthesis** preserves explicitly accepted foundational uncertainty instead of silently choosing. | **Project Final Truth**; **Execution Readiness**. | **Keep** — unresolved foundations remain explicit and force matching roadmap/readiness consequences. | `prompts/create_project_memory.md` | Human-directed synthesis with an unresolved foundation records it in final truth and yields `Design required` when it blocks safe planning. |
| `PROJECT-MEMORY-06` | `.bonsai/design_session.md` — **Module Boundary Clarification** captures only approved, material modules, public seams, dependencies, and forbidden coupling. | **`architecture.md`**; **Simple projects should stay simple**. | **Keep** — module structure is recorded only when it belongs to approved target architecture. | `prompts/create_project_memory.md` | A design with no prescribed module shape gains none; a design with an approved public seam records it consistently. |
| `PROJECT-MEMORY-07` | `.bonsai/design_session.md` — **Synthesis Rules** distinguishes foundational from non-blocking questions, rejects hallucinations/placeholders, and preserves durable target truth. | **Project Final Truth**; **Clean Rebuild Objective**. | **Keep** — generated memory must state known truth plainly and isolate real uncertainty. | `prompts/create_project_memory.md` | No unresolved placeholder leaks into output; known decisions are not weakened into vague assumptions; questions are routed by consequence. |
| `PROJECT-MEMORY-08` | `.bonsai/design_session.md` — **How to Use the Inline Templates Below** keeps cross-document references and ownership consistent and separates developer-local guidance from project memory. | **Artifact Ownership**; **Developer Context**; **Context Layering**; **Project-Memory Creation Workflow**. | **Adapt** — retain embedded output schemas and ownership checks under v2 names; `developer_context.md` is never project-memory output, and separately requested developer-context work remains outside this workflow at home or repository scope. | `prompts/create_project_memory.md` | Every linked layered file exists in the zip; ownership metadata is correct; the zip contains no `developer_context.md` at any path. |
| `PROJECT-MEMORY-09` | `.bonsai/design_session.md` — **Plan Initialization** selects two-pass only for an independently review-worthy durable contract and permits unresolved mode at activation. | **Phase plans**; **Contract-First Two-Pass Execution**. | **Keep** — contract value, not phase size or file count, determines initial roadmap mode. | `prompts/create_project_memory.md` | A public protocol phase may be two-pass; a large internal phase remains single-pass; genuinely premature mode selection remains unresolved. |
| `PROJECT-MEMORY-10` | `.bonsai/design_session.md` — **Initial Phase-Planning Boundary** always defers the detailed initial plan to the first implementation gate. | **Project-Memory Creation Workflow**; **Phase plans**; **Phase-plan gate**. | **Adapt** — preserve the boundary with `plan/agent_plan_phase_1.md` naming. | `prompts/create_project_memory.md`; v2 phase-plan template | Generated memory has no detailed Phase 1 plan and makes drafting it the next action before implementation. |
| `PROJECT-MEMORY-11` | `.bonsai/design_session.md` — **State Initialization** defines explicit readiness and forbids starting a new project directly in an implementation pass. | **Agent Execution Memory**; **Execution Readiness**. | **Adapt** — retain the state semantics in `agent_state.md`. | `prompts/create_project_memory.md` | Ready design yields `Phase planning required` and `Phase Planning`; unresolved design yields `Design required`; neither yields executable implementation. |
| `PROJECT-MEMORY-12` | None; v1.4 has no project-level operational-context output. | **Agent Context**; **Agent-context scopes**; **Project-Memory Creation Workflow**. | **Missing** — v2 may seed project `agent_context.md` from human-approved external-source or useful-map facts. | `prompts/create_project_memory.md`; `skills/agent_context.md` | Approved `barcache`/`tickerview` usage appears only in project agent context, not requirements or architecture. |
| `PROJECT-MEMORY-13` | `.bonsai/design_session.md` emits copyable Markdown blocks; `../../../../../README.md` requires the human to create directories and copy files manually. | **Project-Memory Creation Workflow** requires a zip rooted at `.bonsai/projects/main/` by default. | **Adapt** — replace manual multi-file copying with a complete extractable zip while retaining independently usable Markdown artifacts. | `prompts/create_project_memory.md` | The archive extracts at repository root to the exact selected project path with no extra wrapper directory. |
| `PROJECT-MEMORY-14` | `.bonsai/design_session.md` accepts an implementation project chosen outside the synthesis packet. | **Conventional default project**; **Named projects**; **Project-Memory Creation Workflow**. | **Adapt** — default to the real project `main`; use a named project only when explicitly requested. | `prompts/create_project_memory.md` | An unspecified project produces `projects/main`; an explicit safe project name produces that project and does not create `main` as an alias. |

### Phase-plan and icebox templates

| Evidence ID | Source evidence | Specification rule | Classification and rationale | Owning contract | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `PROJECT-PHASE-TEMPLATE-01` | `../../../../../templates/plan_phase_template.md` — **Objective & Scope**, **Execution Constraints**, **Ordered Work**, and **Validation & Done Criteria** provide a complete active-phase execution surface. | **Phase plans**; **Framework Templates**. | **Keep** — the structure remains justified because phase execution explicitly consumes it. | `templates/plan_phase_template.md` | A generated phase plan states bounded scope, authority, ordered work, checks, risks, and completion criteria without unresolved template placeholders. |
| `PROJECT-PHASE-TEMPLATE-02` | The template distinguishes Single-pass from **Pass A / Pass B** and requires deleting Pass A labels for single-pass work. | **Contract-First Two-Pass Execution**. | **Keep** — pass labels must reflect actual execution mode. | `templates/plan_phase_template.md`; `skills/phase_execution.md` | Single-pass output contains no Pass B label; two-pass output contains a contract review stop before implementation. |
| `PROJECT-PHASE-TEMPLATE-03` | The template preserves compiling source-contract surfaces, behavior-focused expectations, and test-plumbing flexibility without requiring interfaces. | **Pass A: Contract**; **Pass B: Implementation**. | **Keep** — these learned rules protect native contract review without freezing incidental test structure. | `templates/plan_phase_template.md`; `skills/phase_execution.md` | A code-contract plan requires compiling review artifacts and preserves scenario meaning while permitting fixture/helper changes. |
| `PROJECT-PHASE-TEMPLATE-04` | The template's **Maintenance Rules** aligns the detailed plan with `plan.md` and `state.md`, corrects stale plans, and compresses completion detail. | **Agent Execution Memory**; **File Maintenance Discipline**. | **Adapt** — preserve current-truth reconciliation under v2 `agent_` names. | `templates/plan_phase_template.md` | Phase/pass/review transitions agree across all execution memory and completed detail is compressed rather than appended as history. |
| `PROJECT-ICEBOX-TEMPLATE-01` | `../../../../../templates/icebox_template.md` — **Purpose** and **Entries** create the icebox only for the first human-selected observation and make preservation non-authorization explicit. | **Out-of-Scope Observations and `icebox.md`**; **Framework Templates**. | **Keep** — the template has an explicit first-use consumer and protects scope. | `templates/icebox_template.md`; `skills/handoff.md` | No empty icebox is created; first authorized preservation instantiates `ICE-001` with no sample placeholders. |
| `PROJECT-ICEBOX-TEMPLATE-02` | The template records Deferred / Promoted / Rejected / Superseded status and a possible destination. | **File Maintenance Discipline — Icebox**; **Clean Rebuild Objective**. | **Keep** — compact disposition supports later human triage and pruning. | `templates/icebox_template.md` | Promotion names its destination; rejected or valueless superseded entries are removed rather than retained as history. |
| `PROJECT-ICEBOX-TEMPLATE-03` | The v1 template metadata calls the file agent-maintained while durable preservation depends on human choice. | **Human-owned artifacts**; **Avoid hybrid ownership**. | **Adapt** — v2 metadata must identify `icebox.md` as human-owned while allowing instructed mechanical edits. | `templates/icebox_template.md`; `skills/handoff.md` | Generated icebox metadata is human-owned and no agent write changes durable meaning without human authorization. |
| `PROJECT-ICEBOX-TEMPLATE-04` | The template prohibits automatic bug/debt/test/doc entries and forbids copying entries into execution memory. | **Out-of-Scope Observations and `icebox.md`**. | **Keep** — non-authoritative, human-triaged semantics survive unchanged. | `templates/icebox_template.md`; `skills/handoff.md` | An unselected observation leaves no icebox/state/plan record; selected preservation still does not authorize execution. |

### Project, Bonsai Home, and developer context

| Evidence ID | Source evidence | Specification rule | Classification and rationale | Owning contract | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `PROJECT-MANAGE-01` | None; v1.4 requires a project name in the startup pointer and has no in-session project workflow. | **Projects**; **Project management**; **See more options**. | **Missing** — v2 requires List, Switch, and Create Project as a session workflow. | Project Management responsibility in this file; `prompts/implementation.md`; `skills/menu.md` | List is deterministic; switch is session-local; create establishes only memory location and design-required state. |
| `PROJECT-MANAGE-02` | `../../../../../README.md` treats each project as a direct named directory and never defines an alias. | **Conventional default project**; **Named projects**. | **Adapt** — use `main` as the real default and deterministic selection, never as an alias or mutable pointer. | `start.md`; Project Management responsibility | Default, unique, ambiguous, explicit, absent, and concurrent-session project cases resolve as specified. |
| `PROJECT-MANAGE-03` | None; v1.4 has no contextual secondary project menu or invoking-gate return. | **Subordinate workflows**; **Optional Helper Scripts**. | **Missing** — in-session management must work without a helper and return to the refreshed invoking gate. | `prompts/implementation.md`; `skills/menu.md` | Manage Projects returns to startup/handoff with recomputed active project and readiness unless a new design gate supersedes it. |
| `PROJECT-HOME-01` | None; v1.4 is embedded-only. | **Bonsai Home**; **Embedded Bonsai**; **Creating a Bonsai Home**. | **Missing** — v2 requires a reusable-home creation workflow starting from embedded Bonsai. | `skills/bonsai_home.md` | A defined target is created/populated; repository project memory remains local; the new valid home becomes preferred. |
| `PROJECT-HOME-02` | None; v1.4 has no environment-identity migration boundary. | **Creating a Bonsai Home**. | **Missing** — `BONSAI_HOME` must already identify the target; session-only paths and agent-context fallback are prohibited. | `skills/bonsai_home.md`; `start.md` | Missing `BONSAI_HOME` stops with configuration guidance and performs no write; no home path is persisted as learned context. |
| `PROJECT-HOME-03` | None; v1.4 has no reusable-home mutation workflow. | **Creating a Bonsai Home**; **Human control should not require constant babysitting**. | **Missing** — the workflow may create/populate the target when authorized but must not alter shell or machine configuration implicitly. | `skills/bonsai_home.md` | Authorized population succeeds without modifying startup files; unsafe/conflicting target content stops before overwrite. |
| `PROJECT-HOME-04` | None; v1.4 has no secondary or explicit startup request for home creation. | **Startup Bootstrap**; **See more options**; **Creating a Bonsai Home**. | **Missing** — natural-language startup routing and contextual secondary routing load the same bounded workflow. | `start.md`; `prompts/implementation.md`; `skills/menu.md`; `skills/bonsai_home.md` | Both entry paths invoke equivalent behavior and return to a refreshed gate after successful identity change. |
| `PROJECT-DEVELOPER-01` | `.bonsai/developer_context.example.md` and `../../../../../README.md` distinguish intentional developer/team guidance from product truth and agent-discovered tooling facts. | **Developer Context**; **Artifact Ownership**. | **Keep** — the semantic boundary survives: human-owned guidance cannot override final truth and is never an automatic discovery sink. | Developer Context Layering responsibility; `../../../../../../README.md`; `prompts/implementation.md` | Coding preferences affect implementation only after approved truth; an operational discovery is not appended to developer context. |
| `PROJECT-DEVELOPER-02` | `.bonsai/developer_context.example.md` covers coding/test/AI preferences, SDKs, toolchain, runtime constraints, source-control sensitivity, and secrets. | **Developer Context**. | **Keep** — these remain representative developer-context facets. | `../../../../../../README.md`; Developer Context Layering responsibility | Facet-triggered work applies relevant guidance; secrets are rejected; absent context is harmless. |
| `PROJECT-DEVELOPER-03` | v1.4 supports only repository `../../../../../developer_context.md`. | **Bonsai Home**; **Repository-local Bonsai memory**; **Context Layering**. | **Adapt** — v2 layers optional home and repository developer context broad-to-specific; it adds no project developer-context scope. | `prompts/implementation.md` | Home-only, repository-only, combined, and conflicting cases use only the specified scopes with repository specificity winning. |
| `PROJECT-DEVELOPER-04` | v1.4 loads repository developer context at every implementation startup. | **Lazy Loading**; **Facet-triggered context**. | **Drop** — unconditional loading is obsolete; developer context loads only when the current facet needs it. | `prompts/implementation.md` | An unrelated startup does not load either file; code/build work loads relevant guidance before making implementation choices. |
| `PROJECT-DEVELOPER-05` | `.bonsai/developer_context.example.md` is a shipped copy template, but v2 `../../../../../../README.md` already explains developer-context purpose/scopes and no workflow consumes an example artifact. | **Framework Templates**; **Developer Context**; **Clean Rebuild Objective**. | **Drop** — retire the standalone example artifact; preserve its useful guidance in `../../../../../../README.md` and router behavior rather than ship an unconsumed quasi-template. | `../../../../../../README.md`; Developer Context Layering responsibility | The candidate standard has no `developer_context.example.md`; users can create optional human-owned context from documented semantics without hidden required schema. |
| `PROJECT-DEVELOPER-06` | `.bonsai/developer_context.example.md` routes learned facts to v1 `.bonsai/tooling.md`. | **Agent Context**; **Agent-context scopes**. | **Adapt** — route qualifying discoveries to the narrowest v2 `agent_context.md` scope through `skills/agent_context.md`; retain conflict reporting. | `skills/agent_context.md`; Developer Context Layering responsibility | A durable discovery reaches agent context, not developer context; a conflict is surfaced without editing human-owned guidance. |


## Artifact: `prompts/create_project_memory.md`

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
- distinguish foundational uncertainty from non-blocking open questions and preserve each in the appropriate
  durable document;
- ask concise blocking clarifications instead of inventing implementation-shaping foundations;
- embed and instantiate the project-memory output schemas so the generated files remain structurally consistent;
- optionally seed project-level `agent_context.md` from human-approved operational information such as known useful external maps;
- produce a zip rooted at `.bonsai/projects/<project>/`;
- keep target design separate from implementation history;
- explicitly leave detailed Phase 1 planning for the implementation workflow;
- when current project memory is supplied for an existing-project design update, treat it as the approved baseline,
  update only materially affected files, and include execution-memory reconciliation only when needed.

### Must not

- force the human to fill templates during exploratory design;
- manufacture architecture merely to make documents look complete;
- generate the detailed initial Phase 1 plan;
- turn unresolved design uncertainty into invented final truth;
- copy chat history into durable memory;
- treat operational map/source paths as product requirements or architecture;
- create a project-level `developer_context.md` scope absent from the specification;
- generate implementation source, execute implementation work, or silently approve generated human-owned truth.

### Reads

The mature conversation and any explicitly relevant supplied artifacts.

For an existing-project update, the supplied current project final truth and any execution memory that may require
reconciliation.

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

The default project is the real directory `main`. A different project name is used only when the human explicitly
requests a named project. The zip must not add an extra wrapper directory above `../../../../..`.

### Delegates to

No coding-agent implementation workflow.

Its output intentionally sets execution readiness so Phase 1 planning is the first implementation gate.

### Human gates

Blocking clarification only when the durable design cannot be synthesized safely from the conversation.

The generated final truth remains human-owned and is not silently approved by generation.

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
- producing independently usable durable documents rather than chat summaries;
- preserving explicit foundational uncertainty and reflecting its execution consequences;
- using inline output schemas without creating runtime templates that have no consumer;
- updating only materially affected project-memory files during an existing-project design update.

### v2 changes

- rename from design-session framing to project-memory creation;
- use v2 ownership names `agent_plan.md` / `agent_state.md`;
- default output root is `.bonsai/projects/main/`;
- project-level `agent_context.md` may be seeded with approved map/source operational information;
- output protocol is a zip;
- initial detailed Phase 1 plan remains absent;
- source/map knowledge may seed project agent context but never product requirements or architecture;
- developer context is not part of project-memory output; separately requested developer-context work follows the
  home/repository context model outside this workflow;
- manual directory creation and multi-file copying are replaced by one complete archive.

### Validation cases

- simple greenfield project;
- project with deep subsystem architecture;
- design using external `barcache` and `tickerview` maps;
- named project request;
- unresolved design that requires clarification;
- unresolved foundation that the human explicitly accepts for preservation;
- no unnecessary layered documents;
- existing-project update that leaves unaffected files unchanged;
- archive root and cross-document reference integrity.

---

## Artifact: `templates/plan_phase_template.md`

**Existing source:** `../../../../../templates/plan_phase_template.md`  
**Target source path:** `templates/plan_phase_template.md`
**Classification:** Adapt

### Role

Provide the reusable structure used by phase execution when a detailed phase plan is actually warranted.

### Loaded when

Only when drafting a new detailed phase plan.

### Inputs

- current roadmap and state;
- approved requirements, architecture, and applicable durable contracts;
- the phase objective, execution mode, boundaries, risks, and required review/validation gates.

### Responsibilities

- capture objective, scope, approved boundaries, contract surfaces, ordered work, validation, risks, and completion criteria;
- represent single-pass and two-pass modes correctly;
- make contract review explicit only when warranted;
- preserve current execution detail without bloating `agent_plan.md`;
- include maintenance rules that keep `agent_state.md` and roadmap state aligned;
- instantiate all fields with current phase truth and remove the inapplicable pass structure.

### Must not

- force Pass A/Pass B on single-pass phases;
- require invented abstractions;
- imply phase plans are final product/architecture truth;
- require a phase plan merely because a phase touches multiple files;
- leave template placeholders or both single-pass and two-pass instruction branches in an instantiated plan.

### Reads

No project artifact directly. `skills/phase_execution.md` supplies the relevant loaded project truth and execution
memory when instantiating the template.

### Writes / Output

```text
repo/.bonsai/projects/<project>/plan/agent_plan_phase_<N>.md
```

### Delegates to

None. `skills/phase_execution.md` consumes this template and owns planning procedure and gates.

### Human gates

The template represents the Phase Plan Approval Gate and, for two-pass work, the Contract Review Gate. The
phase-execution skill owns presentation and state transitions.

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

### Validation cases

- mandatory first Phase 1 plan;
- optional later single-pass plan with no Pass A/Pass B labels;
- two-pass plan with a compiling native contract surface and explicit review stop;
- stale-plan correction and execution-memory reconciliation;
- no invented module/interface/abstraction boundary and no leaked placeholders.

---

## Artifact: `templates/icebox_template.md`

**Existing source:** `../../../../../templates/icebox_template.md`  
**Target source path:** `templates/icebox_template.md`
**Classification:** Keep + Adapt

### Role

Instantiate `icebox.md` only after the human chooses to preserve an out-of-scope observation.

### Loaded when

The first observation is explicitly authorized for preservation or when a new entry needs the template's structure.

### Inputs

- project name;
- the exact human-selected observation;
- why it is worth retaining;
- its current status and possible destination.

### Responsibilities

- preserve compact, independently understandable deferred observations;
- make status and possible destination explicit;
- distinguish preservation from approval to execute;
- support pruning/promoting/superseding as current truth changes;
- instantiate the first authorized observation as `ICE-001` without unused sample placeholders.

### Must not

- auto-create an empty icebox;
- become a bug/technical-debt dump;
- become requirements, architecture, roadmap, or execution authority;
- preserve rejected/superseded history merely for completeness;
- imply that preservation authorizes implementation.

### Reads

No durable artifact directly. The invoking handoff/triage workflow supplies the authorized observation and checks
whether `icebox.md` already exists.

### Writes / Output

On first authorized preservation only:

```text
repo/.bonsai/projects/<project>/icebox.md
```

Later entries update that human-owned file only under renewed human authorization.

### Delegates to

None. `skills/handoff.md` and `skills/menu.md` own observation review and authorization.

### Human gates

Human selection is required before creating the file, adding an entry, or changing durable observation meaning.
Mechanical pruning or status maintenance follows the human's disposition.

### Preserve from existing version

The v1 template's human-triaged, non-authoritative semantics should survive nearly unchanged.

### v2 changes

The old template labels itself agent-maintained while the v2 specification defines `icebox.md` as human-owned because the human controls durable meaning. The contract and template must be reconciled to v2 ownership without losing agent-assisted mechanical maintenance.

### Validation cases

- no file before human selection;
- first selected observation creates a fully instantiated human-owned `icebox.md`;
- unselected observation remains unpersisted;
- preservation does not alter plan/state or authorize execution;
- promoted, rejected, and superseded entries are maintained without retaining valueless history.

---

## Required v2 behavior: Project Management

**Classification:** Missing in v1.4; assigned without a new standard artifact

**Owning artifacts:** `prompts/implementation.md` for the small in-session workflow; `skills/menu.md` for
contextual presentation and invoking-gate return. Initial startup project resolution remains with `start.md`.

### Role

Support:

- List Projects;
- Switch Project;
- Create Project.

This bounded workflow does not justify a separate skill. Directory enumeration and session-local selection are
small routing responsibilities already owned by the implementation kernel, while reusable presentation already
belongs to the menu skill.

### Loaded when

The human selects **Manage Projects**, explicitly requests one of its actions, or startup identity resolution must
hand an absent/ambiguous project choice to the implementation workflow.

### Inputs

- repository home and current session project identity;
- cheap deterministic enumeration of `repo/.bonsai/projects/`;
- the invoking gate and the human's requested action.

### Responsibilities

- project listing uses cheap deterministic directory enumeration;
- explicit project request is authoritative for the session;
- `projects/main` is the conventional default;
- switching affects current session only;
- creating a project creates memory location but does not invent requirements/architecture;
- if durable design is missing, execution readiness becomes `Design required`;
- workflow normally lives under **See more options**;
- subordinate workflow returns to the invoking gate with refreshed active-project state;
- absent project design yields an explicit `Design required` result rather than invented memory.

### Must not

- write a repository-wide mutable current-project pointer;
- treat `main` as an alias;
- use model reasoning for simple project-directory enumeration;
- depend on optional helper scripts once an AI session is running;
- synthesize requirements, architecture, roadmap, or state merely because a directory was created;
- let a project switch silently discard the invoking gate.

### Reads

```text
repo/.bonsai/projects/
```

After selection, normal implementation startup reads only the selected project's required bootstrap memory.

### Writes

List and Switch write no durable project-selection pointer.

Create may create only:

```text
repo/.bonsai/projects/<project>/
```

Any initial design memory comes later from `prompts/create_project_memory.md` or explicit human-provided files.

### Delegates to

- `skills/menu.md` for presentation and return behavior;
- `prompts/create_project_memory.md` as guidance when design must be synthesized, without invoking a Web UI
  workflow inside the coding session automatically.

### Human gates

- human selection when several projects are available and none is explicit;
- explicit confirmation of a new project name before creating its directory;
- return to the invoking gate after list/switch, or present `Design required` after creating an undesigned project.

### Preserve from existing version

Preserve direct named project directories and explicit human project selection. No v1.4 in-session management
behavior exists to retain.

### v2 changes

Add conventional `main`, deterministic default/unique enumeration, concurrent session-local switching, creation
without design invention, and contextual menu access. Do not preserve the v1 requirement to place a project key in
every startup prompt.

### Validation cases

- `main` default;
- exactly one named project;
- several named projects requiring selection;
- explicit named project overriding defaults;
- list without writes;
- concurrent sessions switch independently;
- create produces only the selected directory and `Design required` state;
- subordinate action returns to a refreshed startup or handoff gate.

---

## Artifact: `skills/bonsai_home.md`

**Classification:** Missing in v1.4; new lazy-loaded workflow skill

### Role

Create and populate a reusable Bonsai Home from an embedded Bonsai environment.

This workflow merits a separate skill because it is infrequent, side-effecting environment work with its own
validation and stop conditions. Keeping it out of the stable implementation kernel preserves lazy loading without
creating a broader environment/configuration framework.

### Loaded when

- the human explicitly requests Create Bonsai Home at startup; or
- the human selects Create Bonsai Home from contextual **See more options** while running embedded.

### Inputs

- resolved repository home and current embedded Bonsai standard;
- `BONSAI_HOME` from the actual environment;
- target-path state;
- current invoking gate.

### Responsibilities

- require `BONSAI_HOME` to already be defined;
- allow the target directory not to exist;
- create/populate the target when authorized;
- preserve repository-local project memory;
- make Bonsai Home the preferred standard when both it and embedded standard are valid;
- explain any remaining environment setup;
- normally be reachable under **See more options** or by explicit startup request;
- validate the source standard and resulting home before treating the new home as current session identity;
- stop before overwriting target content that cannot be safely reconciled with the requested standard population;
- return to the invoking gate with freshly resolved Bonsai Home and project identity after success.

### Must not

- ask for a one-session path as a substitute for `BONSAI_HOME`;
- store Bonsai Home location in agent context as discovery fallback;
- silently modify shell startup files, machine configuration, or other developer-owned environment configuration;
- move or copy repository project memory into the reusable home;
- persist Bonsai Home identity in developer or agent context;
- broadly search for a target or infer one from host home-directory conventions;
- treat helper scripts as required implementation.

### Reads

- `BONSAI_HOME` from the environment;
- the resolved embedded Bonsai standard;
- target existence/content needed for safe population;
- repository-local `.bonsai` only to preserve its local bootstrap/context/project boundary.

### Writes

The configured `BONSAI_HOME` target may receive the shared Bonsai standard and reusable context/map locations
required by that standard.

The workflow does not write repository project memory, shell startup files, machine configuration, or any context
file merely to remember the target path.

### Delegates to

- `start.md` for post-creation identity resolution;
- `skills/menu.md` for presentation and invoking-gate return;
- an optional helper script only as a convenience, never as the sole workflow implementation.

### Human gates

- missing `BONSAI_HOME` stops with configuration guidance and no write;
- unsafe or ambiguous existing target content stops before replacement;
- the explicit workflow request authorizes creation/population of the configured target, but not external
  environment configuration changes.

### Preserve from existing version

None; Bonsai 1.4 has no reusable-home creation workflow.

### v2 changes

Introduce embedded-to-home transition, environment-variable identity, valid-home preference, repository-memory
preservation, and lazy workflow loading.

### Validation cases

- missing `BONSAI_HOME` performs no write and explains the required setup;
- configured nonexistent target is created and populated;
- configured safe existing target is populated without moving repository project memory;
- conflicting target stops before overwrite;
- neither shell startup files nor machine configuration change;
- no target path enters `agent_context.md`;
- successful creation makes the valid Bonsai Home preferred and returns to the refreshed invoking gate;
- explicit startup request and menu entry behave equivalently.

---

## Required v2 behavior: Developer Context Layering

**Classification:** Adapt from v1 repository-only developer context; assigned without a new standard artifact

**Owning artifact:** `prompts/implementation.md`. `skills/agent_context.md` owns only learned operational memory
and conflict handling at the human/agent boundary; it does not become a developer-context loader.

### Role

Apply durable developer/team guidance without confusing it with product truth or agent-discovered operational memory.

The loading rules remain in the implementation router because that router already decides which facet context the
exact next step requires. A separate developer-context skill would add routing indirection without an independent
workflow, durable write, or human gate.

### Loaded when

Only when the exact next step or requested workflow needs developer guidance, such as implementation style,
testing, build/toolchain, runtime, or AI interaction preferences.

### Scopes

```text
$BONSAI_HOME/developer_context.md
repo/.bonsai/developer_context.md
```

Project-local developer context is not currently part of the v2 specification.

### Responsibilities

- load when the current facet needs developer guidance;
- repository-specific statements override broader developer-level statements when they conflict;
- developer context does not override approved requirements or architecture;
- agent discoveries are not silently copied into developer context;
- load the home layer first and apply repository-specific statements as the more specific layer;
- load only the facets relevant to current work rather than treating file existence as startup authorization;
- surface a material mismatch between declared context and direct evidence instead of editing human-owned context;
- route qualifying learned operational facts to `skills/agent_context.md` at the narrowest reusable scope.

### Must not

- override requirements, architecture, or another explicitly human-owned final-truth artifact;
- create a project-local developer-context scope;
- load developer context unconditionally during bootstrap or every implementation startup;
- write, normalize, or merge developer-context files without explicit human instruction;
- preserve secrets or copy agent discoveries into human-owned context;
- retain `.bonsai/tooling.md` as a v2 compatibility destination.

### Reads

When the current facet requires them and the files exist, in broad-to-specific order:

```text
$BONSAI_HOME/developer_context.md
repo/.bonsai/developer_context.md
```

### Writes

None during normal implementation. Developer context is human-owned.

### Delegates to

`skills/agent_context.md` only when current work must read, preserve, correct, or reconcile qualifying agent-owned
operational memory.

### Human gates

No gate merely to apply compatible developer guidance. Stop at the applicable normal gate when guidance conflicts
with approved final truth, requests unauthorized environment change, or leaves a material execution choice unsafe.

### Preserve from existing version

- human/team ownership;
- separation from product truth, execution memory, and learned tooling memory;
- useful facets including code/test/AI preferences, SDK/toolchain paths, and runtime constraints;
- secrets and source-control sensitivity guidance;
- report evidence conflicts rather than silently editing the file.

### v2 changes

- add developer-level Bonsai Home and repository-level scopes with narrow-over-broad precedence;
- drop routine startup loading;
- drop the standalone `developer_context.example.md` distribution artifact and preserve its user guidance in
  `../../../../../../README.md`;
- replace the tooling-only learned-memory destination with scoped `agent_context.md`;
- keep project-local context agent-owned only; no project developer-context layer is introduced.

### Validation cases

- no developer context present;
- home-only and repository-only guidance;
- both layers with repository specificity winning;
- unrelated startup does not load context;
- relevant coding/build work loads it before choices are made;
- project truth wins over conflicting style guidance;
- direct evidence mismatch is reported without a developer-context write;
- qualifying learned fact routes to the appropriate `agent_context.md` scope;
- no project-local developer context and no `developer_context.example.md` candidate artifact.

## Human Review Focus

- Approve retaining the design-synthesis safeguards while changing the delivery contract from copyable blocks to a
  v2-named project-memory zip.
- Approve exact template identities `templates/plan_phase_template.md` and `templates/icebox_template.md`, including
  human ownership for instantiated `icebox.md`.
- Approve keeping Manage Projects in `prompts/implementation.md` plus `skills/menu.md` rather than adding a skill.
- Approve adding `skills/bonsai_home.md` as the one new project/context workflow artifact justified by its distinct,
  side-effecting, lazy-loaded environment boundary.
- Approve keeping developer-context loading in the implementation router and dropping the unconsumed
  `developer_context.example.md` artifact while preserving its guidance in `../../../../../../README.md`.
- Confirm that the 35 evidence records and six complete artifact/responsibility contracts are sufficient
  implementation authority for later phases.
