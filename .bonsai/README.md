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
├── developer_context.example.md         # Optional template for local/developer-specific context
├── skills/
│   ├── phase_execution.md               # Loaded for phase planning or contract gates
│   ├── dry_run.md                       # Loaded only when a dry run is requested or accepted
│   ├── handoff.md                       # Loaded when closing work or preparing a handoff
│   └── final_truth_update.md            # Loaded when final-truth clarification or revision is needed
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
| `plan/plan_phase_<N>.md` | Detailed active phase execution plan | Agent-maintained |
| `icebox.md` | Human-triaged deferred observations | Agent-maintained, human-authorized |
| `.bonsai/developer_context.md` | Optional developer/local context | Developer/team-maintained |
| `.bonsai/skills/*.md` | Triggered implementation workflow | Framework skills |

This separation matters.

* Requirements should not become implementation notes.
* Architecture should not become a task list.
* Plans should not pretend to be product truth.
* State should describe what matters now, not preserve session history.
* Icebox entries should exist only because the human chose to preserve them.
* Developer context should not override project truth.
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
* inline document templates

The design AI uses that single document to generate durable Bonsai project memory.

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
5. summarize the current state and exact next step
6. state execution readiness explicitly
7. classify anticipated final-truth impact as `None`, `Clarification`, or `Revision`
8. stop at a structured startup gate
9. execute only the human-authorized next step
10. reconcile completed work against final truth and any approved dry-run baseline
11. clean operational state and record the next exact step
12. stop at the next natural gate

`implementation_prompt.md` is the always-loaded router and invariant set. It conditionally loads skills only when the current state or requested action requires them:

```text
.bonsai/skills/phase_execution.md       # Phase-mode resolution, phase plans, and contract gates
.bonsai/skills/dry_run.md               # Optional execution previews
.bonsai/skills/handoff.md               # Completion reconciliation and handoff
.bonsai/skills/final_truth_update.md    # Final-truth clarification or revision handling
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

Good examples:

* preferred coding style
* testing philosophy
* abstraction preferences
* local SDK or toolchain paths
* machine-specific setup notes
* unusual build/runtime quirks
* AI session preferences
* recurring constraints that apply when AI tools work with you

This distinction is important.

Bonsai itself should remain usable with different developer styles and different external skills. A rule about how code should normally be structured or tested belongs here, in repository guidance, or in another applicable skill unless it is genuinely part of the project's approved architecture.

Do not use developer context for product requirements, target architecture, phase plans, or current execution state.

Those belong in project memory.

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

It must generate:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`

It may also generate these optional files when the design discussion clearly warrants them:

* `plan/plan_phase_<N>.md`
* `requirements/requirements_<AREA>.md`
* `architecture/architecture_<SUBSYSTEM>.md`

A new Bonsai project usually begins with only the four core documents:

```text
requirements.md
architecture.md
plan.md
state.md
```

Layered requirements, subsystem architecture files, and detailed phase plans are created only when their extra structure materially improves project memory.

A detailed phase plan should not exist merely because a phase is complicated or touches several modules.

If a phase plan is generated during design synthesis, it begins as:

```text
Plan Status: Ready for Review
```

not as approved implementation authority.

`state.md` should make that clear with:

```text
Execution Readiness: Awaiting human review
```

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

For a more complex project, the design session may also produce optional layered files beneath:

```text
plan/
requirements/
architecture/
```

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

The coding agent will load the project memory, summarize the next execution step, state execution readiness, classify anticipated final-truth impact, and stop at a structured startup gate before substantive work begins.

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

---

## `plan/plan_phase_<N>.md`

**Optional agent-maintained detailed execution plan for an active phase.**

Use this when a phase:

* needs detailed ordered sequencing that would bloat `plan.md`
* uses contract-first two-pass execution
* has multiple meaningful human review or validation gates
* has explicit approved constraints that must remain visible during execution

Do not create one merely because the implementation touches several modules or contains many ordinary coding steps.

A phase plan has an explicit planning status:

```text
Draft
Ready for Review
Approved
Superseded
```

`Ready for Review` means planning is complete enough for human review, not that implementation may begin.

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

This file contains detailed phase and contract-first execution procedure.

It also ensures Bonsai does not create abstractions or module boundaries solely to satisfy its own workflow.

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

## `.bonsai/skills/handoff.md`

Loaded when approved work is being closed, a session is ending, or execution state needs to be handed off cleanly.

It guides:

* completion reconciliation
* execution-memory cleanup
* final-truth impact comparison
* dry-run baseline comparison
* next-step recording
* optional out-of-scope observation review
* optional fresh-session guidance

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
* other high-leverage contracts that downstream implementation or external consumers will rely on

Contract-first is **not** automatically required because a phase:

* is large
* touches multiple modules
* creates new classes or packages
* has internal complexity
* introduces helper abstractions
* needs tests
* could theoretically use interfaces

A Bonsai contract does not imply a Java interface or any other particular implementation mechanism.

---

## Pass A: Contract

The coding agent produces the reviewable contract or durable design surface required by the approved phase.

Depending on the project, this might include:

* API signatures
* concrete class shape
* schemas
* message examples
* protocol definitions
* usage examples
* tests that materially clarify intended behavior
* another project-appropriate review artifact

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

## Human-triaged `icebox.md`

`icebox.md` is different from normal agent-maintained execution memory.

The agent does not automatically append to it.

Update `icebox.md` only when the human explicitly chooses to preserve or defer an out-of-scope observation.

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

The default behavior is:

1. notice the issue
2. do not fix it
3. continue the assigned work when safe
4. do not automatically persist the observation
5. at a natural gate, indicate that observations are available if they appear worth human attention

For example:

```text
Out-of-scope observations available: 2
```

The human can then choose whether to spend another interaction reviewing them.

Only observations the human intentionally wants to retain belong in `icebox.md`.

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

When a clean session would be useful, Bonsai may provide:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

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

## Same-session continuation

A human may also deliberately continue in the current session.

At a normal handoff, choices may look like:

1. Proceed to the recorded next step in this session.
2. Discuss or correct the result or recorded next step.
3. Stop here.

When a clean session would be useful, Bonsai may add after those choices:

```text
You can also start a fresh session yourself using:

Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

Bonsai should not describe this as terminating or resetting the current session.

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
7. Agent summarizes current state, execution readiness, and exact next step
8. Human proceeds, corrects/discusses the step, or stops
9. Human requests a dry run only when useful
10. Agent executes one authorized bounded step
11. Agent stops before any material deviation or unapproved final-truth revision
12. Agent may indicate that meaningful out-of-scope observations are available for review
13. Human chooses whether any observation is worth preserving in `icebox.md`
14. Agent loads `.bonsai/skills/handoff.md`, reconciles the completed step, and cleans execution memory
15. Agent records the next exact step and execution readiness
16. Human either continues deliberately in the same session or starts a fresh one
17. Load `.bonsai/skills/phase_execution.md` and pause at phase-plan or contract review gates only when they are genuinely required
18. Explicitly approve updates to human-owned requirements or architecture when implementation reveals a clarification or revision
19. Keep roadmap, state, phase plans, dry-run baselines, and icebox content compact as the project evolves

---

# Summary

Use Bonsai to keep five things cleanly separated:

1. **What the product should be**
2. **What target architecture has actually been approved**
3. **What the AI should do next**
4. **What out-of-scope ideas the human deliberately chose to preserve**
5. **What the AI should know about the developer or local environment**

Human-owned requirements and architecture establish final truth.

Agent-maintained plan and state describe current execution.

The icebox holds only deliberately preserved deferred observations.

Developer context and external skills control developer-specific style and working preferences without turning Bonsai itself into an opinionated coding methodology.

That separation is what makes fresh-session AI development practical while keeping the human in control of product intent, architecture, and scope.