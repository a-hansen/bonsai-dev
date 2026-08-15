# Bonsai Project Workflow

This directory contains the Bonsai project-memory system.

Bonsai is meant to live inside a repository as:

```text
.bonsai/
```

Its job is to preserve the structured memory an AI needs to design, build, and continue serious software work across fresh sessions without requiring the chat history to remain authoritative.

Bonsai governs project memory and execution workflow. It is intentionally not a general software-engineering style guide. Coding style, test philosophy, abstraction preferences, local tooling, and similar developer-specific concerns belong in project conventions, developer context, or external skills.

This guide focuses on **how to use Bonsai inside a project**.

For the broader rationale and public overview, see the repository-level `README.md`.

For repository code mapping, see [the Bonsai Maps guide](maps/README.md).

---

# Directory Layout

```text
.bonsai/
├── README.md
├── design_session.md
├── implementation_prompt.md             # Always-loaded implementation router and invariants
├── developer_context.example.md         # Optional template for human-supplied local/developer context
├── tooling.md                           # Optional, agent-created learned operational memory
├── templates/
│   ├── plan_phase_template.md           # Canonical structure for implementation-time phase plans
│   └── icebox_template.md               # Canonical structure for first-time icebox creation
├── skills/
│   ├── phase_execution.md               # Loaded for phase planning or contract gates
│   ├── dry_run.md                       # Loaded only when a dry run is requested or accepted
│   ├── handoff.md                       # Loaded when closing work or preparing a handoff
│   ├── final_truth_update.md            # Loaded when final-truth clarification or revision is needed
│   └── tooling_memory.md                # Loaded only when tooling/environment knowledge is relevant
├── maps/
│   └── ...
└── projects/
    ├── task-tracker/                    # Included example project
    │   └── ...
    └── <project>/
        ├── requirements.md
        ├── architecture.md
        ├── plan.md
        ├── state.md
        ├── icebox.md                    # Optional, human-triaged deferred observations
        ├── plan/
        │   └── plan_phase_<N>.md        # Optional
        ├── requirements/
        │   └── requirements_<AREA>.md   # Optional
        └── architecture/
            └── architecture_<SUBSYSTEM>.md # Optional
```

---

# The Core Idea

Bonsai separates durable project memory by type.

| File | Role | Ownership |
| --- | --- | --- |
| `requirements.md` | Product truth | Human-owned |
| `requirements/requirements_<AREA>.md` | Deep product-area requirements | Human-owned |
| `architecture.md` | Target implementation truth | Human-owned |
| `architecture/architecture_<SUBSYSTEM>.md` | Deep subsystem architecture | Human-owned |
| `plan.md` | Execution roadmap | Agent-maintained |
| `state.md` | Current resume state | Agent-maintained |
| `plan/plan_phase_<N>.md` | Detailed active phase execution plan; always used for initial Phase 1 planning, conditional later | Agent-maintained |
| `icebox.md` | Human-triaged deferred observations | Agent-maintained, human-authorized |
| `.bonsai/developer_context.md` | Optional human-supplied developer/local context | Developer/team-maintained |
| `.bonsai/tooling.md` | Optional learned operational tooling/environment memory | Agent-maintained |
| `.bonsai/templates/*.md` | Reusable structures for implementation-time artifacts | Framework templates |
| `.bonsai/skills/*.md` | Triggered implementation workflow | Framework skills |

This separation matters.

* Requirements should not become implementation notes.
* Architecture should not become a task list.
* Plans should not pretend to be product truth.
* State should describe what matters now, not preserve session history.
* Icebox entries should exist only because the human chose to preserve them.
* Developer context should not override project truth.
* Learned tooling memory should record current operational facts and workarounds, not session history.
* Triggered skills should not be copied into project memory.
* Deep requirement areas should not bloat top-level product truth.
* Deep subsystem architecture should not bloat top-level implementation truth.

## Human-owned final truth

Human-owned final truth describes the product and target system intended to exist after successful implementation.

It normally includes:

```text
requirements.md
architecture.md
requirements/requirements_<AREA>.md
architecture/architecture_<SUBSYSTEM>.md
```

It may also include project-specific design or contract documents when the human explicitly designates them as durable project truth.

During implementation, proposed or discovered work is classified against this truth as:

* `None`
* `Clarification`
* `Revision`

A `Revision` requires explicit human approval of the affected final-truth documents before substantive implementation continues.

## Execution memory

These files describe how the project is currently being executed:

```text
plan.md
plan/plan_phase_<N>.md
state.md
```

They are maintained by the agent as execution progresses.

Changing execution memory is normal workflow maintenance. It is not itself a final-truth clarification or revision.

---

# Workflow Overview

Bonsai assumes two main kinds of AI work.

## 1. Design and planning

Use a Web UI AI to explore:

* what you are building
* who it is for
* what matters most
* constraints
* architecture
* alternatives
* risks
* sequencing

When the design is mature enough to preserve, paste the full contents of:

```text
.bonsai/design_session.md
```

into the same conversation.

`design_session.md` is a self-contained synthesis packet. It includes:

* design-synthesis instructions
* output rules
* clarification rules
* execution-readiness rules
* inline templates for the core project files and optional layered requirements/architecture

The design AI uses that single document to generate durable Bonsai project memory. It does not generate the
initial detailed phase plan. Instead, a new project leaves design synthesis with Phase 1 planning as the first
implementation gate.

Bonsai should preserve the design that emerged from the conversation. It should not invent interfaces, abstraction layers, builders, module boundaries, testing strategies, or other implementation conventions merely to make the generated documents look architecturally complete.

---

## 2. Implementation and execution

Use an IDE / CLI coding agent to:

* read the project memory
* inspect the repository
* identify the exact next step
* determine whether planning is actually complete
* execute the active plan
* reconcile proposed and completed work against approved final truth
* maintain compact operational state
* preserve durable learned tooling/environment knowledge without loading it into every session
* surface useful out-of-scope observations without automatically preserving them
* maintain code maps when structural changes justify it

Start with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

The coding agent should:

1. read the shared code map when present
2. read developer context when present
3. read the active project memory
4. read deeper requirements, architecture, phase plans, or skills only when their trigger applies
5. for a newly synthesized project, draft `plan/plan_phase_1.md` as the first implementation planning action
   and stop for human approval before substantive Phase 1 work
6. lazy-load tooling memory only when the tooling-memory trigger applies
7. summarize the current state and exact next step
8. state execution readiness explicitly
9. classify anticipated final-truth impact as `None`, `Clarification`, or `Revision`
10. stop at a structured startup gate
11. execute only the human-authorized next step
12. reconcile completed work against final truth and any approved dry-run baseline
13. clean operational state and record the next exact step
14. stop at the next natural gate

`implementation_prompt.md` is the always-loaded router and invariant set. It conditionally loads skills only when the current state or requested action requires them:

```text
.bonsai/skills/phase_execution.md       # Phase-mode resolution, phase plans, and contract gates
.bonsai/skills/dry_run.md               # Optional execution previews
.bonsai/skills/handoff.md               # Completion reconciliation and handoff
.bonsai/skills/final_truth_update.md    # Final-truth clarification or revision handling
.bonsai/skills/tooling_memory.md        # Lazy-loaded learned tooling/environment memory
```

This keeps normal implementation sessions smaller without hiding the rules that protect scope, authority, and final truth.

---

# Optional Developer Context

Bonsai includes a template for developer-specific context:

```text
.bonsai/developer_context.example.md
```

If useful, copy it to:

```text
.bonsai/developer_context.md
```

Use this file for stable context that is useful across AI sessions but does not belong in project truth.
It is intentionally supplied and maintained by the developer or team.

Good examples:

* preferred coding style
* testing philosophy
* abstraction preferences
* known local SDK or toolchain paths
* intentionally documented machine-specific setup
* known build/runtime constraints
* AI session preferences
* recurring constraints that apply when AI tools work with you

This distinction is important.

Bonsai itself should remain usable with different developer styles and different external skills. A rule about how code should normally be structured or tested belongs here, in repository guidance, or in another applicable skill unless it is genuinely part of the project's approved architecture.

Do not use developer context for product requirements, target architecture, phase plans, or current execution state.

Do not use it as an automatic destination for environment or tooling facts discovered by the implementation
agent. Learned operational facts belong in optional `.bonsai/tooling.md` when they satisfy the
tooling-memory skill's preservation rules.

Those project concerns belong in project memory.

## Source control guidance

`developer_context.md` may be local-only or team-managed depending on your project.

Keep it out of source control when it contains:

* personal preferences
* absolute local paths
* machine-specific setup
* private environment details

Commit it only when the team intentionally wants shared developer/operator context.

Never put secrets in this file.

---

# Optional Tooling Memory

Bonsai can preserve durable operational facts that an implementation agent learns while working in the repository:

```text
.bonsai/tooling.md
```

This file is different from `developer_context.md`.

* `developer_context.md` is intentionally supplied and maintained by the developer or team.
* `tooling.md` is agent-maintained memory learned from actual repository/environment work.

Examples of useful tooling memory include:

* a tool exists but is not on the expected `PATH`
* a repository must use its wrapper rather than a system build tool
* a temporary-directory location is unreliable and a repository-local alternative works
* a recurring permission or runtime constraint changes how commands must be executed
* an installed tool or runtime version materially limits available commands
* a known warning is harmless and can be ignored during a specific validation path

`tooling.md` is intentionally lazy-loaded. It is not part of routine implementation startup.

When `state.md` identifies a tooling/environment blocker, the exact next step is explicitly tooling/environment
work, or execution encounters an unexpected tooling/build/filesystem/runtime problem, the implementation agent
loads:

```text
.bonsai/skills/tooling_memory.md
```

That skill decides whether existing `tooling.md` should be read and whether a newly learned fact is durable
enough to create or update the file.

The file should preserve current actionable knowledge, not failed-attempt history. A useful entry describes the
working rule or workaround rather than every command that failed before it was discovered.

The implementation agent may maintain qualifying tooling memory without human approval. That does not authorize
the agent to install software, change dependencies, modify developer-owned context, alter machine configuration,
or broaden implementation scope.

If a current tooling issue blocks the exact next step, the blocker still belongs in `state.md`. A durable lesson
learned while resolving or characterizing that blocker may also belong in `tooling.md`.

Keep secrets out of `tooling.md`.

For source control, keep machine-specific tooling memory local unless the team intentionally wants to share it.
Repository-wide, reproducible operational knowledge may be committed when that is useful.

---

# Try the Included Example First

This repository includes:

```text
.bonsai/projects/task-tracker/
```

a small example Bonsai project produced by a completed design session.

It is useful for seeing what initial project memory looks like before implementation begins.

To try it, open your coding AI and run:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker
```

The agent should:

1. read the example project memory
2. summarize the current implementation state
3. identify the exact next step
4. state whether the project is ready to execute
5. stop at a structured startup gate before making changes

The startup gate normally offers:

1. Proceed with the identified next step.
2. Correct or discuss the identified next step.
3. Stop here.

Dry runs remain available when requested. They are not advertised at every routine gate.

---

# Creating a New Project

## Step 1: Design the project in a Web UI AI

Discuss the project naturally.

Work through:

* goals
* product behavior
* users
* scope
* workflows
* architecture
* major decisions
* open questions
* likely implementation phases

Do not try to prematurely fill templates by hand unless that is genuinely easier.

The design session is where meaningful ambiguity gets resolved.

---

## Step 2: Synthesize the design into Bonsai memory

When the design has matured, paste the full contents of:

```text
.bonsai/design_session.md
```

into the same conversation.

The design AI will use the inline instructions and templates in that document to synthesize the conversation into durable project memory.

For initial synthesis it must generate:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`

It may also generate these optional human-owned design files when the design discussion clearly warrants them:

* `requirements/requirements_<AREA>.md`
* `architecture/architecture_<SUBSYSTEM>.md`

A new Bonsai project usually begins with only the four core documents:

```text
requirements.md
architecture.md
plan.md
state.md
```

Layered requirements and subsystem architecture files are created only when their extra structure materially
improves project memory.

The design session does **not** generate `plan/plan_phase_1.md`. When the design is sufficient to proceed,
`state.md` should initialize the first implementation boundary as:

```text
Active Phase Plan File: None
Phase Plan Status: None
Current Phase Pass: Phase Planning
Execution Readiness: Phase planning required
```

The first implementation session drafts `plan/plan_phase_1.md` from
`.bonsai/templates/plan_phase_template.md` and stops at the Phase Plan Approval Gate. This initial phase-plan
review happens every time, even when Phase 1 is single-pass and straightforward.

---

## Step 3: Create the project directory

Create:

```text
.bonsai/projects/<project>/
```

Example:

```text
.bonsai/projects/audit-logging/
```

---

## Step 4: Save the generated project memory

Copy the generated documents into:

```text
.bonsai/projects/<project>/
```

For a simple project, the initial result may look like:

```text
.bonsai/projects/audit-logging/
├── requirements.md
├── architecture.md
├── plan.md
└── state.md
```

For a more complex project, the design session may also produce optional layered design files beneath:

```text
requirements/
architecture/
```

The `plan/` directory is created later by the implementation workflow when it drafts the first phase plan.

---

## Step 5: Optionally add developer context

If you want the implementation agent to know stable developer preferences or local environment details, copy:

```text
.bonsai/developer_context.example.md
```

to:

```text
.bonsai/developer_context.md
```

Fill in only stable, reusable context.

Examples:

* local SDK locations
* preferred build commands
* runtime caveats
* coding preferences
* testing preferences
* how direct or cautious you want the agent to be

Keep project truth out of this file.

---

## Step 6: Start implementation

Open your coding AI and begin with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

Example:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: audit-logging
```

The coding agent will load the project memory, summarize the next execution step, state execution readiness,
classify anticipated final-truth impact, and stop at a structured startup gate before substantive work begins.

For a newly synthesized project, that first authorized step is phase planning. The agent loads
`.bonsai/skills/phase_execution.md`, creates `plan/plan_phase_1.md` from
`.bonsai/templates/plan_phase_template.md`, updates execution memory, and stops again for phase-plan approval
before any substantive Phase 1 implementation.

The human may authorize the step, correct or discuss the proposed next step, or stop.

A dry run can be requested when useful.

---

# Execution Readiness

One of Bonsai's jobs is to make it obvious whether planning is actually finished.

`state.md` uses explicit execution-readiness values:

| Value | Meaning |
| --- | --- |
| `Design required` | Product or architecture decisions must be resolved first. |
| `Phase planning required` | Durable design is sufficient, but execution planning is incomplete. |
| `Awaiting human review` | A plan, contract, or other required artifact is waiting for human approval. |
| `Ready to execute` | The exact next implementation step has an approved basis and no required planning gate remains. |
| `Blocked` | A concrete blocker prevents safe execution. |
| `Complete` | No further implementation work is currently required. |

A plan document merely existing does not mean planning is complete.

For example:

```text
Plan Status: Ready for Review
Execution Readiness: Awaiting human review
```

means the phase has been planned but implementation is not yet authorized.

After explicit human approval:

```text
Plan Status: Approved
Execution Readiness: Ready to execute
```

may be appropriate if no other gate remains.

This distinction prevents a completed-looking planning artifact from being mistaken for an approved implementation basis.

---

# Design Pivots

Bonsai project memory is not frozen after the initial design session.

As the product, architecture, or roadmap changes, update the affected memory documents before asking the implementation agent to continue.

A design pivot is any change that materially affects:

* product behavior
* user workflows
* scope boundaries
* architectural direction
* accepted constraints
* implementation sequencing at the roadmap level

Examples:

* changing the persistence strategy
* replacing one major subsystem approach with another
* adding or removing a major product capability
* changing what is considered in scope
* revising the phase roadmap after new information appears

## Recommended pivot workflow

1. Start or continue a Web UI AI design conversation.
2. Provide the current Bonsai memory documents that may be affected.

   Usually include:

   ```text
   requirements.md
   architecture.md
   plan.md
   state.md
   ```

   Also include layered files when relevant:

   ```text
   requirements/requirements_<AREA>.md
   architecture/architecture_<SUBSYSTEM>.md
   plan/plan_phase_<N>.md
   ```

   Reuse `.bonsai/design_session.md` when useful. For an existing project it can apply the same requirements
   and architecture structures to the affected top-level or layered design documents without requiring a full
   project regeneration.

3. Explain the proposed pivot and the reason for it.
4. Ask the AI to update only the affected Bonsai documents.
5. Review changes to human-owned final truth explicitly.
6. Save the approved updated documents back into `.bonsai/projects/<project>/`.
7. Reconcile `plan.md`, phase plans, and `state.md` with the revised truth.
8. Continue implementation using the normal startup process.

Use:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

## What to update

Update `requirements.md` or `requirements/requirements_<AREA>.md` when product intent, behavior, workflows, constraints, or scope changes.

Update `architecture.md` or `architecture/architecture_<SUBSYSTEM>.md` when the intended target structure, durable contracts, dependencies, or architectural constraints change.

Update `plan.md` when the roadmap, phase order, active phase, deferred roadmap work, execution mode, or phase-plan status changes.

Update `state.md` when current execution reality changes.

## What not to do

Do not treat chat history as durable memory.

Do not ask the implementation agent to “just remember” a design pivot.

Do not bury product or architecture changes inside `plan.md` or `state.md`.

Do not let code changes become the only record of a changed decision.

The updated Bonsai documents are the durable memory.

---

# Core Project Files

## `requirements.md`

**Human-owned product truth.**

Defines:

* what the system is for
* who it serves
* workflows and functional requirements
* product constraints
* accepted decisions
* open product questions

It should remain readable as the top-level statement of product truth.

It should not contain implementation detail.

During implementation, any proposed or discovered change to product behavior or constraints must be classified and routed through explicit human approval rather than silently absorbed into code or execution memory.

When a product area develops deep, isolated requirement complexity that would bloat this top-level document, preserve the summary here and move detailed truth into:

```text
requirements/requirements_<AREA>.md
```

---

## `requirements/requirements_<AREA>.md`

**Optional human-owned deep product-area requirements.**

Use this when a product area has enough complexity that its:

* outcomes
* workflows
* functional requirements
* domain rules
* constraints
* exclusions
* accepted decisions

would clutter the top-level `requirements.md`.

Requirement-area files should split by capability, workflow, or product concern, not by implementation subsystem.

Examples:

```text
requirements/requirements_licensing.md
requirements/requirements_audit_events.md
requirements/requirements_import_workflow.md
```

---

## `architecture.md`

**Human-owned target implementation truth.**

Defines, when the intended architecture requires them:

* target system structure
* major subsystems
* canonical domain model and data ownership
* durable public contracts
* allowed flows and dependency constraints
* cross-cutting rules
* architectural guardrails
* rejected approaches

It should be rebuild-grade.

It should describe the system you ultimately want, not merely the accidental shape of the current implementation.

It also should not invent implementation structure merely because a template has a place for it.

For example, if the approved design does not prescribe an interface, dependency layer, or internal module boundary, architecture should say so rather than manufacturing one.

During implementation, any proposed or discovered change to intended structure or architectural constraints must be classified and routed through explicit human approval.

When a subsystem develops deep, isolated architectural complexity that would bloat this top-level document, preserve the summary here and move detailed truth into:

```text
architecture/architecture_<SUBSYSTEM>.md
```

---

## `architecture/architecture_<SUBSYSTEM>.md`

**Optional human-owned deep subsystem architecture.**

Use this when a subsystem has enough approved complexity that its:

* boundaries
* public contracts
* data flow
* dependencies
* cross-cutting rules
* guardrails

would clutter the top-level `architecture.md`.

Do not create interfaces or internal seams merely to populate the document.

---

## `plan.md`

**Agent-maintained execution roadmap.**

Defines:

* build strategy
* phase summaries
* which phase is active
* phase execution mode
* phase-plan presence
* phase-plan approval status
* deferred roadmap work
* completed work

It changes when roadmap-level execution truth changes.

It should not become a session log.

---

## `state.md`

**Agent-maintained current resume state.**

Defines:

* current phase
* active phase plan
* phase-plan approval state
* current phase pass
* execution mode
* execution readiness
* current objective
* current snapshot
* resume-critical active files
* active blockers or risks
* exact next step
* success condition
* compact approved dry-run baseline, only while one is active

`state.md` is not a historical journal.

When updating it, the agent should:

* remove completed next steps
* remove resolved blockers
* remove obsolete active files
* remove stale observations
* remove superseded decisions
* remove expired dry-run baselines
* replace stale snapshot text rather than append history

A useful rule is:

> If removing a fact would not materially change what the next implementation session does, it probably does not belong in `state.md`.

For pass terminology, single-pass work should be recorded as:

```text
Current Phase Pass: Single-pass Implementation
```

`Pass A (Contract)`, `Contract Review`, and `Pass B (Implementation)` are reserved for actual two-pass
contract-first phases. A single-pass implementation phase is not Pass B.

---

## `icebox.md`

**Optional human-triaged deferred observation storage.**

The icebox exists for out-of-scope observations that the human explicitly chooses to preserve for possible later consideration.

Examples might include:

* an adjacent bug
* technical debt
* a refactor opportunity
* a documentation gap
* a future enhancement
* a follow-up design question

The implementation agent should **not automatically record these observations**.

Instead:

1. the agent notices potentially useful out-of-scope work
2. it continues the authorized work when safe
3. at the next natural gate, it may report:

   ```text
   Out-of-scope observations available: 3
   ```

4. the human may choose to review them
5. only observations the human explicitly chooses to preserve or defer are written to `icebox.md`

`icebox.md` is not:

* an approved backlog
* an execution roadmap
* a substitute for `plan.md`
* a session history
* a dumping ground for every adjacent idea an agent notices

A human may later promote a preserved item into authoritative project memory or active execution work.

When the human first chooses to preserve an observation and the project does not yet have `icebox.md`, the agent
creates it from:

```text
.bonsai/templates/icebox_template.md
```

The template is not a reason to create an empty icebox.

---

## `plan/plan_phase_<N>.md`

**Agent-maintained detailed execution plan for an active phase.**

Phase 1 is intentionally special: every newly synthesized project drafts `plan/plan_phase_1.md` as the first
implementation planning action and stops for human approval before substantive implementation. The implementation
agent creates it from:

```text
.bonsai/templates/plan_phase_template.md
```

For Phase 2 and later, create a detailed phase plan when the phase:

* needs detailed ordered sequencing that would bloat `plan.md`
* uses contract-first two-pass execution
* has multiple meaningful human review or validation gates
* has explicit approved constraints that must remain visible during execution

Do not create a later phase plan merely because the implementation touches several modules or contains many
ordinary coding steps.

A phase plan has an explicit planning status:

```text
Draft
Ready for Review
Approved
Superseded
```

`Ready for Review` means planning is complete enough for human review, not that implementation may begin.

---

# Framework Templates

Reusable implementation-time artifact templates live under:

```text
.bonsai/templates/
```

Bonsai intentionally keeps only templates with explicit runtime consumers:

* `plan_phase_template.md` is consumed by `.bonsai/skills/phase_execution.md` whenever a new detailed phase plan
  is created.
* `icebox_template.md` is consumed when the human first authorizes preservation of an out-of-scope observation
  and the project does not yet have `icebox.md`.

Requirements and architecture templates remain inline in `design_session.md` because those artifacts are created
and revised in the Web UI design workflow.

---

# Framework Skill Files

Skill files live under:

```text
.bonsai/skills/
```

They are not project memory. They are triggered agent behaviors used by `implementation_prompt.md`.

## `.bonsai/skills/phase_execution.md`

Loaded when current work involves:

* phase execution-mode resolution
* phase-plan creation or correction
* phase approval gates
* Pass A contract work
* contract review gates

This file contains detailed phase and contract-first execution procedure. It uses
`.bonsai/templates/plan_phase_template.md` whenever it creates a new phase plan.

It also ensures Bonsai does not create abstractions or module boundaries solely to satisfy its own workflow,
while allowing native source-level API or structural skeletons to serve directly as code-contract review artifacts.

---

## `.bonsai/skills/dry_run.md`

Loaded when the human requests a dry run or accepts one that Bonsai suggested because of unusual execution risk or ambiguity.

A dry run is read-only.

It previews:

* approved basis
* expected touch points
* intended result
* planned checks
* likely scope concerns
* anticipated final-truth impact

Dry runs are available when useful. They are not a routine mandatory phase of Bonsai execution.

---

## `.bonsai/skills/final_truth_update.md`

Loaded when proposed or completed work requires human-owned final-truth clarification or revision.

It centralizes handling of:

* `None`
* `Clarification`
* `Revision`

This skill prevents implementation or execution memory from silently redefining requirements or architecture.

---

## `.bonsai/skills/tooling_memory.md`

Loaded when:

* `state.md` identifies a tooling/environment blocker
* the exact next step is explicitly to diagnose or change tooling/environment behavior
* execution encounters an unexpected tooling, build, test-runner, filesystem, temporary-directory,
  command-availability, dependency/tool-version, or runtime-environment issue

The skill governs:

* lazy loading of optional `.bonsai/tooling.md`
* deciding whether a discovered fact is durable enough to preserve
* updating current operational rules instead of accumulating troubleshooting history
* separating current blockers from durable operational memory
* keeping learned observations separate from developer-owned context
* preventing tooling memory from becoming implicit authority to modify the environment

---

## `.bonsai/skills/handoff.md`

Loaded when approved work is being closed, a session is ending, or execution state needs to be handed off cleanly.

It guides:

* completion reconciliation
* execution-memory cleanup
* final-truth impact comparison
* dry-run baseline comparison
* next-step recording
* optional out-of-scope observation review
* current-session or fresh-session continuation after completed work

A handoff is not a session history.

---

# Starting an Implementation Session

Open your coding AI and begin with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

Example:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: audit-logging
```

The agent should read required startup files in the order specified by `implementation_prompt.md`.

At a high level:

1. `.bonsai/maps/code_map.md`, when present
2. `.bonsai/developer_context.md`, when present
3. project core:

    * `requirements.md`
    * `architecture.md`
    * `plan.md`
    * `state.md`

4. active phase plan, when applicable
5. deeper requirement or architecture files only when relevant
6. triggered skills only when required

`icebox.md` is not a routine startup read. It is read only when the current step explicitly involves a preserved observation or human-requested icebox triage.

`tooling.md` is also not a routine startup read. It is read through `.bonsai/skills/tooling_memory.md` only when
a tooling-memory trigger applies.

The agent should respond with a compact startup summary:

* active project
* current phase
* current phase pass
* phase execution mode
* phase-plan status, when applicable
* execution readiness
* exact next step
* final-truth impact: `None`, `Clarification`, or `Revision`
* affected final-truth documents, when impact is not `None`
* blockers
* loaded skills
* mode recommendation and rationale, when execution mode remains unresolved

Then it should stop and present:

1. Proceed with the identified next step.
2. Correct or discuss the identified next step.
3. Stop here.

If project-memory files disagree about phase status, plan approval, readiness, or the exact next step, the agent should report that inconsistency rather than silently choosing an interpretation.

---

# Human Gates and Dry Runs

Bonsai uses explicit human gates rather than vague prompts such as “awaiting approval.”

* **Approve** applies to a reviewed artifact or contract.
* **Proceed** authorizes a stated execution action.
* **Dry run** is an optional read-only preview.

The implementation agent should prefer supported structured choices and otherwise use equivalent numbered choices.

## Returning from subordinate workflows

A gate may temporarily invoke a smaller workflow such as observation review, clarification, correction, or triage.
After that subordinate action completes, the agent reconciles execution memory, recomputes the exact next step and
execution readiness, and returns to the gate that invoked it. If the action materially changes the workflow or
creates a new required gate, that new gate replaces the prior one.

A successful subordinate action should not cause the parent handoff or approval gate to disappear.

## Dry runs

Dry runs remain available but are intentionally de-emphasized.

The agent should not place a dry-run choice in every routine menu.

The human can request one at any applicable execution gate.

Bonsai may proactively suggest a dry run only when a preview would materially reduce unusual execution risk or ambiguity.

When used, the agent reads:

```text
.bonsai/skills/dry_run.md
```

A dry run identifies:

* approved basis
* expected touch points
* intended result
* planned checks
* scope concerns
* anticipated final-truth impact

If approved, only a compact execution baseline is preserved in `state.md` until the work completes, is abandoned, or is redirected.

Then it is removed.

## Final-truth impact

At execution gates and completion, impact on human-owned final truth is classified as:

| Impact | Meaning | Handling |
| --- | --- | --- |
| `None` | Existing approved human-owned truth already covers the work. | Proceed under the normal gate. |
| `Clarification` | Intended behavior and architecture are unchanged, but final truth should be stated more precisely. | Propose the affected human-owned document update. |
| `Revision` | Intended behavior, constraints, architecture, or system boundaries change. | Stop before substantive implementation until affected final-truth documents are updated and approved. |

If continuing a step requires a material contract change, expanded approved scope, acceptance of failed required checks, or a new human design decision, the agent stops before making that change.

---

# Contract-First Two-Pass Work

Bonsai supports a **Two-Pass Contract-First** workflow when a phase establishes or materially changes a contract that independently deserves human review before implementation.

The phase-planning and contract-gate skill lives in:

```text
.bonsai/skills/phase_execution.md
```

It is loaded only when phase planning, execution-mode resolution, or contract-first work requires it.

## When contract-first is appropriate

Examples include:

* externally consumed APIs
* schemas
* persistent formats
* protocols or message formats
* extension or plugin contracts
* durable integration surfaces
* other durable contracts that downstream implementation or external consumers will rely on and that independently merit human approval before implementation

An already approved durable contract does not require a redundant Bonsai contract gate merely because a phase
implements it.

Contract-first is **not** automatically required because a phase:

* is large
* touches multiple modules
* creates new classes or packages
* has internal complexity
* introduces helper abstractions
* creates or changes internal module organization
* changes implementation dependency structure that is not itself an approved durable contract
* needs tests
* could theoretically use interfaces

A Bonsai contract does not imply a Java interface or any other particular implementation mechanism.

---

## Pass A: Contract

The coding agent produces the reviewable contract or durable design surface required by the approved phase.
Whenever practical, the contract should be reviewed in the native artifact form developers will ultimately
consume rather than translated into a separate prose specification.

Depending on the project, this might include:

* source-level API or structural skeletons
* API signatures
* concrete class shape
* schemas
* message examples
* protocol definitions
* usage examples
* behavior-focused tests that materially clarify intended behavior
* another project-appropriate review artifact

For a code contract, the normal Pass A shape is minimal source-level API or structural skeletons plus the tests
or usage examples needed to review behavior. Concrete classes with intentionally unimplemented methods are
valid contract artifacts. Pass A may establish names, types, signatures, visibility, and structural relationships
without implementing substantive behavior. A standalone prose contract document is appropriate only when
important semantics cannot be expressed clearly in the native artifacts or when the contract itself is naturally
non-code. Supplemental prose is fine when it materially improves review.

Pass A should preserve architecture constraints that already exist in approved project truth.

It should not invent:

* interfaces
* builders
* adapters
* dependency-injection layers
* module seams
* abstraction layers

merely to satisfy a Bonsai contract gate.

Then it stops at the contract review gate.

---

## Human review

The human reviews the contract that actually matters.

Typical questions include:

* Is this the right externally meaningful shape?
* Does it express the intended behavior?
* Does it conform to approved architecture?
* Is implementation ready to proceed?

The contract gate normally offers:

1. Approve the contract.
2. Request revisions to the contract.
3. Discuss concerns before deciding.
4. Return to the phase plan.

If approved, Bonsai records the Pass B next step and marks execution readiness appropriately.

A dry run may still be requested, but it is not automatically inserted into the contract menu.

If the proposed contract has `Revision` final-truth impact, the agent first routes affected human-owned final truth for explicit approval.

---

## Pass B: Implementation

Only after contract approval and any required final-truth approval does the agent build the underlying implementation.

Implementation follows:

* approved project truth
* approved contract
* project conventions
* developer context
* relevant source guidance
* applicable external skills

Bonsai itself does not dictate the internal implementation style.

---

# File Maintenance Rules

## Human-owned files

The coding agent should not modify these without explicit instruction:

```text
requirements.md
requirements/requirements_<AREA>.md
architecture.md
architecture/architecture_<SUBSYSTEM>.md
```

The coding agent classifies impact on these documents at relevant authorization gates and completion:

* `None`
* `Clarification`
* `Revision`

The human owns their approval.

---

## Agent-maintained execution memory

The coding agent actively maintains:

```text
plan.md
state.md
plan/plan_phase_<N>.md
```

when their truth changes.

### Update `plan.md` when

* phase status changes
* roadmap order changes
* new roadmap deferrals appear
* a phase completes
* execution mode changes
* a detailed phase plan becomes necessary
* phase-plan approval status changes

### Update `state.md` when

* exact next step changes
* current objective changes
* blockers change
* execution readiness changes
* active pass changes
* phase transition occurs
* active phase plan changes
* phase-plan approval state changes
* an approved dry-run baseline becomes active, completes, is abandoned, or is redirected

Every state update should also remove obsolete content.

Do not append historical entries merely because they once mattered.

### Update `plan/plan_phase_<N>.md` when

* active sequencing changes
* plan approval status changes
* contract/implementation pass changes
* validation plan changes
* phase-level execution questions change

---

## Agent-maintained `tooling.md`

`.bonsai/tooling.md` is optional learned operational memory.

Do not create or load it merely because a repository has build tools.

Create or update it only through `.bonsai/skills/tooling_memory.md` when a discovered fact is durable,
actionable, likely to matter again, and supported by enough evidence to state a useful current rule or workaround.

When maintaining it:

* preserve current operational truth, not troubleshooting history
* consolidate duplicate entries
* correct or remove stale entries when disproven
* keep transient failures, command typos, one-off network problems, and unique temporary paths out
* keep unresolved current blockers in `state.md`
* never record secrets
* do not silently modify `.bonsai/developer_context.md` to match an observation

---

## Human-triaged `icebox.md`

`icebox.md` is different from normal agent-maintained execution memory.

The agent does not automatically append to it.

Update `icebox.md` only when the human explicitly chooses to preserve or defer an out-of-scope observation.
If it does not yet exist, create it from `.bonsai/templates/icebox_template.md` and instantiate the approved
observation as the first entry.

Do not treat `icebox.md` as approved scope.

Do not execute icebox items unless the human explicitly promotes them into active work or tells the agent to address them.

---

# Out-of-Scope Observations

During implementation, an agent will often notice things outside the exact next step.

Examples:

* adjacent bugs
* technical debt
* questionable code
* refactor opportunities
* missing documentation
* missing tests
* possible future enhancements

Bonsai should prevent those observations from silently expanding the current task.

A durable tooling/environment fact is not an icebox observation merely because it was discovered incidentally.
When it qualifies under `.bonsai/skills/tooling_memory.md`, it may be preserved automatically in
`.bonsai/tooling.md` without human triage.

The default behavior for ordinary out-of-scope observations is:

1. notice the issue
2. do not fix it
3. continue the assigned work when safe
4. do not automatically persist the observation
5. at a natural gate, indicate that observations are available if they appear worth human attention

For example:

```text
Out-of-scope observations available: 2
```

The human can then choose whether to spend another interaction reviewing them. When an observation is reviewed,
a normal triage prompt is:

```text
Should this observation be preserved for later triage?

1. Leave it unpreserved for now.
2. Preserve it in icebox.md.
3. Discuss before deciding.
4. Other.
```

Only observations the human intentionally wants to retain belong in `icebox.md`. If observation review or an
immediate correction was invoked from a handoff, the agent returns to that handoff after the subordinate action
completes, unless the action creates a different required gate.

This keeps both project memory and token usage focused on information that has demonstrated value.

---

# Session Boundaries

Bonsai works well with clean sessions, but it does not control the chat or agent host.

Bonsai cannot:

* terminate a session
* clear a session
* reset a session
* create a new session

It can only stop its current workflow at an appropriate boundary and tell the human how to continue.

A clean session is often useful when:

* a substantial planning gate completes
* a contract is approved
* a major objective completes
* accumulated conversation context has become noisy
* the next step begins a substantially different pass

But starting a new session remains a human action.

## Canonical fresh-session prompt

When the human selects fresh-session continuation, Bonsai provides:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

Bonsai does not decide whether the human should continue in the current session or a fresh one. It offers both
when the recorded next step is executable. Starting the fresh session remains a human action.

That prompt is intentionally only a pointer.

It should not contain:

* previous-session summaries
* phase names
* pass names
* approval status
* exact next step
* dry-run state
* stop conditions
* required skills

Those details belong in `state.md`.

The new session discovers them through the normal startup process.

## Continuation choices

At a normal handoff, the human chooses whether executable work continues in the current session or a fresh one.
Neither session choice is recommended by Bonsai.

The completion summary first presents these as standalone fields:

```text
Next step:
<actual next step>

Execution readiness:
<status>
```

Then it asks:

```text
What would you like to do next?
```

When out-of-scope observations exist and the next step is executable, choices may look like:

1. Continue with `<concise actual next step>` in the current session.
2. Continue with `<concise actual next step>` in a fresh session.
3. Review or change the next step.
4. Review the `<N>` out-of-scope observation(s).
5. Do not continue right now.

Without observations, omit the observation choice and renumber `Do not continue right now.` to 4. The action
text should name the actual next step rather than referring indirectly to a "recorded next step."

Do not add a generic `Other` choice to Bonsai menus. Agent hosts may append their own free-form option.

If the human selects fresh-session continuation, Bonsai tells the human to start the new session themselves,
provides the canonical prompt, and stops without executing the next step in the current session.

If execution readiness does not permit execution, omit both continuation choices and present the applicable gate
or non-execution actions instead. A fresh session does not bypass a required gate or blocker.

---

# Code Maps During Implementation

Implementation sessions should use:

```text
.bonsai/maps/code_map.md
```

for top-level repository orientation when it exists.

When the exact next step touches a mapped subsystem, the agent may load:

```text
.bonsai/maps/subsystems/<subsystem>/map.md
```

and, only when needed:

```text
.bonsai/maps/subsystems/<subsystem>/api_pub.md
.bonsai/maps/subsystems/<subsystem>/api_ext.md
```

Maps are selective memory.

They are not substitutes for source inspection.

For the full repository mapping workflow, see:

```text
.bonsai/maps/README.md
```

---

# Updating Maps After Code Changes

The implementation agent should update shared maps only when code changes alter:

* public structure
* extension points
* lifecycles
* key architectural relationships
* rebuild-relevant behavior

It should not update maps for routine local code changes.

When map updates are needed, the agent should follow the mapping-system instructions referenced by the code-map artifacts rather than improvising local map-writing rules.

---

# Clean Rebuilds

Bonsai project memory should describe the **target system**, not every historical detour taken while building it.

Maintaining that target truth is an implementation responsibility as well as a design-session goal.

As implementation exposes gaps or approved pivots, final-truth reconciliation keeps human-owned requirements and architecture aligned with the intended rebuild target.

Execution memory should likewise represent the current execution reality rather than preserving a diary of how the project arrived there.

That means a mature Bonsai project can eventually support a clean rebuild:

* preserve final requirements
* preserve final architecture
* preserve useful roadmap structure
* preserve only current execution state
* discard implementation scars, obsolete pivots, and stale session history

This is especially valuable for prototypes that became real systems through repeated experimentation.

---

# Practical Working Rhythm

A typical Bonsai project may look like this:

1. Web UI design conversation
2. Paste `.bonsai/design_session.md`
3. Generate initial project memory
4. Save it under `.bonsai/projects/<project>/`
5. Optionally create `.bonsai/developer_context.md`
6. Coding-agent startup
7. Agent summarizes current state, execution readiness, and the Phase 1 planning next step
8. Human authorizes phase planning, corrects/discusses the step, or stops
9. Agent creates `plan/plan_phase_1.md` from the canonical template and stops for phase-plan approval
10. Human approves or revises the phase plan
11. Human requests a dry run only when useful
12. Agent executes one authorized bounded step
13. If a tooling/environment issue appears, agent lazy-loads `.bonsai/skills/tooling_memory.md` and consults or updates `.bonsai/tooling.md` only as warranted
14. Agent stops before any material deviation or unapproved final-truth revision
15. Agent may indicate that meaningful out-of-scope observations are available for review
16. Human chooses whether any observation is worth preserving in `icebox.md`
17. Agent loads `.bonsai/skills/handoff.md`, reconciles the completed step, and cleans execution memory
18. Agent records the next exact step and execution readiness
19. Human either continues deliberately in the same session or starts a fresh one
20. For later phases, load `.bonsai/skills/phase_execution.md` and create another phase plan only when the phase warrants one; pause at contract review gates when genuinely required
21. Explicitly approve updates to human-owned requirements or architecture when implementation reveals a clarification or revision
22. Keep roadmap, state, phase plans, dry-run baselines, tooling memory, and icebox content compact as the project evolves

---

# Summary

Use Bonsai to keep six things cleanly separated:

1. **What the product should be**
2. **What target architecture has actually been approved**
3. **What the AI should do next**
4. **What out-of-scope ideas the human deliberately chose to preserve**
5. **What the developer or team intentionally told the AI about the local environment and working preferences**
6. **What the AI learned about how to work successfully in this repository/environment**

Human-owned requirements and architecture establish final truth.

Agent-maintained plan and state describe current execution.

The icebox holds only deliberately preserved deferred observations.

Developer context preserves intentionally supplied developer/local guidance. Optional tooling memory preserves
qualified operational facts learned by the agent and is loaded only when relevant.

External skills can still control developer-specific working behavior without turning Bonsai itself into an
opinionated coding methodology.

That separation is what makes fresh-session AI development practical while keeping the human in control of product intent, architecture, and scope.