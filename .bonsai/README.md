# Bonsai Project Workflow

This directory contains the Bonsai project-memory system.

Bonsai is meant to live inside a repository as:

```text
.bonsai/
```

Its job is to preserve the structured memory an AI needs to design, build, and continue serious
software work across many fresh sessions.

This guide focuses on **how to use Bonsai inside a project**.

For the broader rationale and public overview, see the repository-level `README.md`.
For repository code mapping, see [the Bonsai Maps guide](maps/README.md).

---

# Directory Layout

```text
.bonsai/
├── README.md
├── design_session.md
├── implementation_prompt.md
├── style_guide.md
├── maps/
│   └── ...
└── projects/
    ├── task-tracker/                         # Included example project
    │   └── ...
    └── <project>/
        ├── requirements.md
        ├── architecture.md
        ├── plan.md
        ├── state.md
        ├── icebox.md                          # Optional
        ├── plan/
        │   └── plan_phase_<N>.md             # Optional
        ├── requirements/
        │   └── requirements_<AREA>.md        # Optional
        └── architecture/
            └── architecture_<SUBSYSTEM>.md   # Optional
```

---

# The Core Idea

Bonsai separates durable project memory by type.

| File                                       | Role                                       | Ownership        |
| ------------------------------------------ | ------------------------------------------ | ---------------- |
| `requirements.md`                          | Product truth                              | Human-owned      |
| `requirements/requirements_<AREA>.md`      | Deep product-area requirements             | Human-owned      |
| `architecture.md`                          | Target implementation truth                | Human-owned      |
| `architecture/architecture_<SUBSYSTEM>.md` | Deep subsystem architecture                | Human-owned      |
| `plan.md`                                  | Execution roadmap                          | Agent-maintained |
| `state.md`                                 | Current-session baton pass                 | Agent-maintained |
| `icebox.md`                                | Out-of-scope observations worth preserving | Agent-maintained |
| `plan/plan_phase_<N>.md`                   | Detailed active phase execution plan       | Agent-maintained |

This separation matters.

* Requirements should not become implementation notes.
* Architecture should not become a task list.
* Plans should not pretend to be product truth.
* State should not become a historical journal.
* Icebox notes should not become an unapproved backlog.
* Deep requirement areas should not bloat top-level product truth.
* Deep subsystem architecture should not bloat top-level implementation truth.

Each file has a narrow job.

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

* the design-synthesis instructions
* the output rules
* the clarification rules
* the inline document templates the design AI should use

The design AI uses that single document to generate durable Bonsai project memory.

---

## 2. Implementation and execution

Use an IDE / CLI coding agent to:

* read the project memory
* inspect the repository
* execute the active plan
* update operational state
* preserve useful out-of-scope observations without expanding scope
* maintain code maps when structural changes justify it

Start with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>.
```

The coding agent should:

1. read the shared code map, when one exists and is relevant
2. read the active project memory
3. read area-level requirements, phase-level plans, or subsystem-level architecture only when needed
4. summarize the current state
5. recommend the appropriate AI level for the exact next step
6. wait for the human to proceed
7. execute only that next step

---

# Try the Included Example First

This repository includes:

```text
.bonsai/projects/task-tracker/
```

a small example Bonsai project produced by a completed design session.

It is useful for seeing what the initial project memory looks like before implementation begins.

To try it, open your coding AI and run:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker.
```

The agent should:

1. read the example project memory
2. summarize the current implementation state
3. identify the exact next step
4. recommend an AI effort level
5. stop for human approval or redirection before making changes

That startup gate is a core Bonsai behavior.

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

Do not try to prematurely fill templates by hand unless that is genuinely easier. The design session
is where ambiguity gets resolved.

---

## Step 2: Synthesize the design into Bonsai memory

When the design has matured, paste the full contents of:

```text
.bonsai/design_session.md
```

into the same conversation.

The design AI will use the inline instructions and templates in that document to synthesize the
conversation into durable project memory.

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

Layered requirements, subsystem architecture files, and detailed phase plans are created only when
their extra structure materially improves the project memory.

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

## Step 5: Start implementation

Open your coding AI and begin with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>.
```

Example:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: audit-logging.
```

The coding agent will load the project memory, summarize the next execution step, recommend an AI
effort level, and stop for approval or redirection before substantive work begins.

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

When a product area develops deep, isolated requirement complexity that would bloat this top-level
document, preserve the summary here and move the detailed truth into:

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

Requirement-area files should remain product-facing. They should split by capability, workflow, or
product concern, not by implementation subsystem.

Examples:

```text
requirements/requirements_licensing.md
requirements/requirements_audit_events.md
requirements/requirements_import_workflow.md
```

---

## `architecture.md`

**Human-owned target implementation truth.**

Defines:

* target system structure
* major subsystems
* canonical domain model and data ownership
* allowed flows and dependency boundaries
* cross-cutting rules
* architectural guardrails
* rejected approaches, when they matter

It should be rebuild-grade.

It should describe the system you ultimately want, not merely the accidental shape of the current
implementation.

When a subsystem develops deep, isolated architectural complexity that would bloat this top-level
document, preserve the summary here and move the detailed truth into:

```text
architecture/architecture_<SUBSYSTEM>.md
```

---

## `architecture/architecture_<SUBSYSTEM>.md`

**Optional human-owned deep subsystem architecture.**

Use this when a subsystem has enough complexity that its:

* boundaries
* interfaces
* data flow
* dependencies
* cross-cutting rules
* guardrails

would clutter the top-level `architecture.md`.

---

## `plan.md`

**Agent-maintained execution roadmap.**

Defines:

* build strategy
* phase summaries
* which phase is active
* whether a phase uses single-pass or two-pass execution
* deferred work
* completed work

It changes when roadmap-level execution truth changes.

---

## `state.md`

**Agent-maintained current-session baton pass.**

Defines:

* current phase
* active phase pass
* active phase plan file
* current objective
* recent work
* active blockers
* exact next step
* recommended AI effort level

It should remain compact, volatile, and easy to read at every implementation-session startup.

---

## `icebox.md`

**Optional agent-maintained out-of-scope observation storage.**

Use this when the implementation agent notices work that is useful to preserve but should not be
handled during the current exact next step.

Examples:

* adjacent bugs
* technical debt
* missing tests
* refactor opportunities
* documentation gaps
* follow-up questions worth revisiting later

The agent should record these observations concisely and continue the assigned work.

`icebox.md` is **not**:

* an approved backlog
* an execution roadmap
* a substitute for `plan.md`
* a place to silently expand project scope

A human may later review `icebox.md` and promote selected items into:

```text
requirements.md
requirements/requirements_<AREA>.md
architecture.md
architecture/architecture_<SUBSYSTEM>.md
plan.md
plan/plan_phase_<N>.md
```

when appropriate.

---

## `plan/plan_phase_<N>.md`

**Optional agent-maintained detailed execution plan for an active phase.**

Use this when a phase:

* is complex enough to need ordered sequencing
* uses contract-first two-pass execution
* has multiple validation gates
* would bloat `plan.md`

Completed phase plans may later be compressed or archived once their details are no longer
execution-relevant.

---

# Starting an Implementation Session

Open your coding AI and begin with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>.
```

Example:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: audit-logging.
```

The agent should then read:

1. `.bonsai/maps/code_map.md`, when present and relevant
2. project core:

    * `requirements.md`
    * `architecture.md`
    * `plan.md`
    * `state.md`
3. active phase plan, if named in `state.md`
4. requirement-area files only when relevant to the exact next step
5. subsystem architecture files only when relevant to the exact next step
6. `icebox.md`, only when present and relevant to the exact next step or recent project context

It should respond with a compact startup summary:

* active project
* current phase
* current phase pass
* exact next step
* blockers
* recommended AI level

Then it should stop and wait for the human to explicitly proceed.

---

# Recommended AI Level at Session Startup

For the initial implementation startup, use a capable general-purpose level such as:

* **medium**
* **thinking**

rather than immediately spending the maximum available AI level.

That startup step is mainly a bounded orientation task:

1. read the Bonsai memory
2. identify the active project state
3. surface the exact next step
4. recommend the appropriate AI level for executing that step

After that, follow the recommendation:

* use stronger reasoning for architecture, API contracts, difficult debugging, or uncertain tradeoffs
* use lighter or cheaper levels for narrow, mechanical, or well-specified work
* reserve maximum reasoning for work that actually deserves it

---

# Fresh Sessions Are the Default

Bonsai is designed around **frequent clean sessions**.

A session should end when:

* the exact next step changes meaningfully
* the current objective completes
* the agent has accumulated too much local noise
* a review gate is reached
* a major decision changes the direction of work

Before ending, the agent should update:

```text
state.md
```

and any other agent-maintained files whose truth changed.

Then start a new session with the same implementation prompt.

The chat is temporary working space.
The repository is durable project memory.

---

# Contract-First Two-Pass Work

For phases that introduce an important API, subsystem boundary, or abstraction, Bonsai supports a
**Two-Pass Contract-First** workflow.

## Pass A: Contract

The coding agent drafts:

* the high-level API shape
* behavioral tests that show intended use
* minimal scaffolding needed to make the contract reviewable

Then it stops.

---

## Human Review

The human reviews:

* Is this the right abstraction?
* Is the API shaped correctly?
* Do the tests express the right behavior?
* Should implementation proceed?

---

## Pass B: Implementation

Only after approval does the agent build the underlying implementation.

This keeps the human involved before the wrong abstraction becomes a large amount of working code.

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

These preserve product and architectural truth.

---

## Agent-maintained files

The coding agent should actively maintain:

```text
plan.md
state.md
icebox.md
plan/plan_phase_<N>.md
```

when their truth changes.

### Update `plan.md` when

* phase status changes
* roadmap order changes
* new deferrals appear
* a phase completes
* a separate detailed phase plan becomes necessary

### Update `state.md` when

* exact next step changes
* current objective changes
* blockers change
* recommended AI level changes
* active pass changes
* phase transition occurs

### Update `icebox.md` when

* an out-of-scope bug is discovered
* technical debt is noticed
* a useful refactor opportunity appears
* a missing test or documentation gap should be preserved
* a follow-up issue may matter later but should not interrupt the current step

Keep entries compact, specific, and easy for a human to triage.

Do not treat `icebox.md` as approved scope.
Do not execute icebox items unless the human explicitly moves them into the active plan or tells the
agent to address them.

### Update `plan/plan_phase_<N>.md` when

* active sequencing changes
* contract/implementation pass changes
* validation plan changes
* phase-level open questions change

---

# Code Maps During Implementation

Implementation sessions should use:

```text
.bonsai/maps/code_map.md
```

for top-level repository orientation when it exists and is relevant.

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

When map updates are needed, the agent should follow the mapping-system instructions referenced by
the code-map artifacts rather than improvising local map-writing rules.

---

# Clean Rebuilds

Bonsai project memory should describe the **target system**, not every historical detour taken while
building it.

That means a mature Bonsai project can eventually support a clean rebuild:

* preserve the final requirements
* preserve the final architecture
* preserve the durable roadmap lessons worth keeping
* discard implementation scars from early pivots

This is especially valuable for prototypes that became real systems through repeated experimentation.

---

# Practical Working Rhythm

A typical Bonsai project may look like this:

1. Web UI design conversation
2. Paste `.bonsai/design_session.md`
3. Generate initial project memory
4. Save it under `.bonsai/projects/<project>/`
5. Coding-agent startup
6. Agent summarizes state and waits at the startup gate
7. Human approves or redirects the next step
8. Agent executes one bounded next step
9. Agent records useful out-of-scope discoveries in `icebox.md`, when needed
10. Agent updates `state.md`
11. Start a fresh session
12. Continue
13. Pause at contract review gates when appropriate
14. Periodically revise human-owned requirements or architecture in a deliberate design session
15. Keep roadmap, state, and icebox compact as the project evolves

---

# Summary

Use Bonsai to keep four things cleanly separated:

1. **What the product should be**
2. **How the system should be shaped**
3. **What the AI should do next**
4. **What the AI noticed but should not act on yet**

That separation is what makes frequent fresh-session AI development practical.
