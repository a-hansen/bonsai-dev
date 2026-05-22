# Bonsai

**Structured project memory for serious AI-assisted software development.**

Bonsai is a repo-local memory system and workflow for using AI to design, build, and evolve software
over many sessions without losing the thread.

It helps you:

* start fresh AI sessions frequently without starting over
* keep context small, structured, and high-signal
* move cleanly from Web AI design to IDE / CLI implementation
* preserve and actively reconcile product intent, architecture, roadmap, current execution state, and useful out-of-scope observations separately
* layer deep product requirements, subsystem architecture, detailed phase plans, and stage-specific implementation procedures without bloating always-loaded context
* guide coding agents through large codebases using layered code maps
* right-size AI effort instead of burning maximum reasoning on every step
* keep the human in the loop through explicit approval and execution gates
* preview risky execution with optional compact dry runs
* rebuild a project cleanly from its final intended form after early pivots and experimentation

Bonsai is plain Markdown plus a small set of prompts.

No server.
No database.
No framework lock-in.

Just durable, structured memory that travels with the project.

---

# Repository Layout

This repository intentionally contains Bonsai under:

```text
.bonsai/
```

because that is how Bonsai is meant to live inside a real software project.

```text
bonsai-dev/
├── README.md
└── .bonsai/
    ├── README.md
    ├── design_session.md
    ├── implementation_prompt.md
    ├── phase_execution.md
    ├── step_completion.md
    ├── dry_run.md
    ├── style_guide.md
    ├── maps/
    │   └── ...
    └── projects/
        └── task-tracker/
            └── ...
```

The repo root is the public project landing page.
The `.bonsai/` directory is the actual framework you copy into another repository.

This repository also includes:

```text
.bonsai/projects/task-tracker/
```

a small example Bonsai project showing the output of a completed design session before implementation begins.

It gives new users a concrete reference for what Bonsai project memory looks like in practice, including:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`

and any supporting project documents needed for the example workflow.

---

# TL;DR

## Try Bonsai immediately with the included example

Clone the repo, open your AI coding tool, and begin with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker.
```

The AI should:

1. load the existing `task-tracker` project memory
2. summarize the current execution state
3. identify the exact next implementation step
4. recommend the appropriate AI level for that step
5. stop at a structured startup gate before execution begins

At that gate, you can proceed, request a compact dry run first, correct the identified next step, or
stop. This is the fastest way to see the Bonsai implementation workflow in action.

---

## Add Bonsai to your own project

Copy:

```text
.bonsai/
```

into the root of the repository where you want to use it.

Each software effort gets its own project memory directory under:

```text
.bonsai/projects/<project>/
```

Then follow:

```text
.bonsai/README.md
```

for the project workflow.

---

## Start a design session

Use a Web UI AI to brainstorm the product, architecture, constraints, and tradeoffs.

When the design has matured, paste the full contents of:

```text
.bonsai/design_session.md
```

into the conversation.

The AI will synthesize the conversation into durable project memory:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`

and, when warranted:

* `plan/plan_phase_<N>.md`
* `requirements/requirements_<AREA>.md`
* `architecture/architecture_<SUBSYSTEM>.md`

A new Bonsai project usually begins with only the four core project memory documents:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`

Layered requirements, subsystem architecture files, detailed phase plans, and code maps are added only
when the project warrants them.

---

## Start an implementation session

Open your AI coding tool and begin with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>.
```

The AI will load the relevant Bonsai memory, summarize the current execution state, identify whether
the exact next step affects approved final truth, recommend the appropriate AI level, and then stop at
a structured startup gate before execution begins.

`implementation_prompt.md` stays compact by loading specialized procedures only when needed:

* `phase_execution.md` when phase planning, execution-mode resolution, or contract gates are active
* `dry_run.md` when the human requests an execution preview
* `step_completion.md` when approved work is being closed and handed off

This is the command you will use over and over. At completion, the agent reconciles the result against
approved final truth and any approved dry-run baseline, updates operational project memory, reports
the result, and recommends starting a clean session for the recorded next step.

---

## Build repository code maps

For large or unfamiliar codebases, Bonsai also includes a dedicated mapping workflow.

Code maps help future implementation agents:

* orient quickly
* route to the right subsystem
* avoid repeatedly rediscovering the repository
* preserve non-obvious caller and extension mechanics

See:

```text
.bonsai/maps/README.md
```

for the full mapping workflow.

---

# Why Bonsai Exists

AI coding tools are powerful, but serious software work exposes their weak spots quickly.

## Long sessions rot

A single giant chat or coding session slowly becomes:

* expensive
* noisy
* hard to steer
* full of stale decisions and dead branches
* increasingly prone to drift

Bonsai is designed for the opposite approach:

> **Start clean sessions often. Keep the memory outside the session. Load only what matters.**

---

## Re-explaining a project is wasteful

Without persistent structure, every new session forces the human to restate:

* what the product is
* what architecture has already been chosen
* what work is in progress
* what decisions are settled
* where the relevant code lives
* what should happen next

Bonsai makes that context durable and reusable.

The project remembers itself.

---

## “More context” is not the same as “better context”

Many AI workflows respond to forgetting by stuffing more text into the model. Bonsai takes a
different approach:

* **telegraphic, structured memory**
* **layered documents**
* **compact session handoff**
* **selective reading**
* **progressive drill-down only when needed**

The goal is not to maximize context.
The goal is to maximize **useful context per token**.

---

## Product development is messy. Final products should not be.

Early software development involves pivots:

* requirements sharpen
* bad ideas get discarded
* architectures improve
* APIs change shape
* the implementation path wanders

That exploration is healthy. But the final repository should not be forced to preserve every wrong
turn.

Bonsai distinguishes between:

* **the path you took**
* **the product you ultimately decided to build**

Its durable project memory is intended to describe the **final desired system**, not merely chronicle
the historical implementation journey.

That truth is not only established during design. During implementation, Bonsai classifies proposed
or discovered impact on requirements and architecture as:

* `None`: existing final truth already covers the work
* `Clarification`: intended behavior is unchanged, but final truth should be stated more precisely
* `Revision`: intended behavior, constraints, architecture, or system boundaries change

A revision does not silently slip through as code or planning detail. The affected final-truth
documents must be updated and approved before substantive implementation proceeds.

That enables a powerful workflow:

> **Once the product and architecture have matured, Bonsai can guide an AI to rebuild the system
> cleanly from scratch as though the final design had been known from the beginning.**

A prototype that survived five pivots may work, but still carry the scars. Bonsai gives you a path
toward a coherent rebuild, not just endless patching.

---

# What Makes Bonsai Different

Bonsai is not just a folder of AI instructions.

It is a development memory system built around a specific belief:

> **AI-assisted software work improves dramatically when the project carries its own durable,
> structured memory.**

---

## It is not just a bigger prompt

A single giant project prompt eventually becomes its own problem:

* too much stale detail
* too much history mixed with current truth
* too much irrelevant context loaded into every session
* too little distinction between product intent, architecture, roadmap, and active work

Bonsai uses layered, purpose-specific documents instead.

It does not try to put the whole project into one prompt.
It gives the AI a structured way to load the right memory at the right time.

---

## It is not just an `AGENTS.md` file

Repository instructions are useful. Bonsai is built for a different job.

A typical agent instruction file tells an AI:

* how to behave
* how to build or test
* which conventions to follow

Bonsai preserves:

* what the product is
* what architecture is intended
* what decisions have been made
* what phase of work is active
* what exactly should happen next
* what useful out-of-scope observations should be preserved without becoming active work
* how to find deeper codebase understanding when needed

Agent instructions shape behavior.
Bonsai preserves project memory.

They are complementary, not interchangeable.

---

## It is not agent orchestration

Agent orchestration can be valuable. Multiple agents can divide work, explore alternatives, or operate
in parallel.

But adding agents does not automatically solve:

* weak project memory
* bloated or stale context
* architectural drift
* repeated rediscovery of the codebase
* lossy handoffs between design and implementation

> **Throwing more agents at a poorly remembered project is still throwing more bodies at the wrong
> problem.**

Bonsai addresses a more fundamental layer: the quality and continuity of the memory each agent
receives.

It is independent of orchestration.

* Use Bonsai with one AI assistant.
* Use Bonsai with a coding agent.
* Use Bonsai inside a larger multi-agent workflow.

The principle is the same:

> **Better agents help. Better project memory helps every agent.**

---

## It is built to survive pivots

Many AI workflows are good at helping you move forward from wherever you currently are.

Bonsai is also designed to preserve the final product shape that emerges after experimentation,
reconsideration, and change.

That means it can support a clean rebuild later:

> **Not a replay of every development detour, but a fresh implementation of the final system you now
> know you wanted.**

---

# What Bonsai Gives You

## 1. Durable AI project memory

Bonsai stores the important truths of a project in versioned Markdown files inside the repo.

It separates:

* product truth
* architecture truth
* execution roadmap
* active session state
* useful out-of-scope observations
* phase-level execution detail
* shared codebase navigation knowledge

These are different kinds of memory, and mixing them together makes both humans and agents worse at
their jobs.

---

## 2. Layered truth without top-level bloat

Top-level project memory should stay orienting and authoritative.

But serious projects eventually accumulate detail that deserves preservation without being loaded into
every session.

Bonsai supports optional layered documents for product depth, architecture depth, and execution depth:

```text
requirements/requirements_<AREA>.md
architecture/architecture_<SUBSYSTEM>.md
plan/plan_phase_<N>.md
```

Use these when a product area, architectural subsystem, or active implementation phase has deep,
isolated complexity that would otherwise bloat the top-level documents.

The top-level files retain the project-wide truth.
The layered files preserve detailed truth that can be loaded only when relevant.

---

## 3. Frequent fresh-session workflow

Bonsai is designed around the idea that **fresh sessions are good**.

Instead of stretching one AI conversation until it becomes a swamp, you:

1. execute one bounded, authorized step
2. let the agent update `state.md` and report completion
3. normally end the current session at that handoff
4. start a new session
5. reload only the meaningful project memory
6. continue cleanly

The completion gate still lets you continue in the current session when that is more convenient, but
the recommended path is a clean restart. This keeps reasoning sharper and conversations easier to
manage.

---

## 4. Context minimization by design

Bonsai aggressively avoids bloated memory.

Its documents are intended to be:

* structured
* telegraphic
* skimmable
* updated intentionally
* read selectively

The implementation workflow reads the high-level project memory first, then drills into deeper
documents only when the current task requires it.

The implementation instructions follow the same rule. The always-loaded prompt preserves startup,
authority, final-truth, scope, and maintenance invariants. Stage-specific procedures for phase
execution, dry runs, and step completion are loaded only when their trigger applies.

A large project should not require dumping the entire project history or every implementation
procedure into every AI session.

---

## 5. A bridge from design AI to coding AI

Bonsai assumes two different kinds of AI work.

### Web UI AI

Best for:

* brainstorming
* product shaping
* requirements discovery
* architecture discussion
* tradeoff analysis
* turning a fuzzy idea into a coherent build plan

### IDE / CLI AI

Best for:

* reading the repository
* editing code
* running tests
* executing a plan
* updating operational project memory

Bonsai connects those modes.

The Web AI helps produce the project memory.
The coding AI consumes that memory and executes against it.

---

## 6. Clear human authority boundaries

Not all Bonsai documents are equal.

Some represent durable decisions the human owns.
Others represent operational state the agent maintains.

### Human-owned truth

* `requirements.md`
* `requirements/requirements_<AREA>.md`
* `architecture.md`
* `architecture/architecture_<SUBSYSTEM>.md`

These should describe what the product is and how it is intended to work. They are not disposable
scratchpads. They are maintained final truth.

The coding agent does not silently modify them to match implementation drift. At implementation gates
and completion, it identifies whether work has no final-truth impact, requires a clarification, or
requires a revision. The human approves changes to final truth before revised behavior or architecture
becomes the project direction.

### Agent-maintained execution memory

* `plan.md`
* `state.md`
* `icebox.md`
* `plan/plan_phase_<N>.md`

These evolve as implementation proceeds.

This split matters. It gives the agent enough authority to manage execution without casually
rewriting the project’s underlying intent.

---

## 7. A compact baton pass between sessions

`state.md` is the current-session handoff document.

It captures:

* current phase
* current pass within the phase
* active detailed phase plan, if any
* current objective
* recent work
* active blockers
* exact next step
* recommended AI effort level

It should stay compact.

A new coding session should be able to read `state.md` and understand immediately:

> “What is happening right now, and what exactly do I do next?”

---

## 8. A parking lot for useful observations

Implementation sessions often surface useful work that is **not** part of the exact next step:

* adjacent bugs
* technical debt
* missing tests
* refactor opportunities
* documentation gaps
* follow-up concerns worth revisiting later

Bonsai gives those observations a place to live:

```text
icebox.md
```

The coding agent can preserve them without expanding scope mid-session.

`icebox.md` is not an approved backlog and not an execution plan.
It is a triageable parking lot for potentially valuable discoveries.

A human can later promote selected items into requirements, architecture, or planning when they
actually become intended work.

---

## 9. Roadmap memory without roadmap bloat

`plan.md` tracks the implementation roadmap:

* the build strategy
* major phases
* active phase
* completed work
* deferred work
* whether a phase uses single-pass or contract-first two-pass execution

For phases that need real execution detail, Bonsai uses:

```text
plan/plan_phase_<N>.md
```

This keeps the roadmap readable while still allowing complex work to be planned carefully.

---

## 10. Layered code maps

Coding agents waste enormous time rediscovering a repository.

Bonsai addresses that with layered code maps.

A top-level code map gives the agent a broad orientation:

* major areas of the codebase
* key architectural domains
* high-value routing guidance
* where to look for a given kind of work

Deeper maps can provide more specific guidance for:

* large architectural subsystems
* framework internals
* package families
* extension seams
* caller-facing mechanics
* implementation patterns worth preserving

The agent starts broad and drills down only when needed.

This keeps startup context lean while still giving the AI a durable understanding of the codebase.

> **Bonsai’s code maps are not meant to replace reading code.
> They are meant to help the agent read the right code.**

See the [Bonsai Maps guide](.bonsai/maps/README.md).

---

## 11. Contract-first execution for high-leverage human review

For phases that introduce an important API, subsystem boundary, or abstraction, Bonsai supports a
**Two-Pass Contract-First** workflow.

### Pass A: Contract

The coding AI drafts:

* the high-level API shape
* behavioral tests that show intended use
* minimal scaffolding needed to make the contract reviewable

Then it **stops**.

### Human Review

The human reviews:

* Is this the right abstraction?
* Is the API shaped correctly?
* Do the tests express the right behavior?
* Should implementation proceed directly or after a dry run?

The gate makes that transition explicit: approve and proceed, approve and preview implementation
with a dry run, request revisions, or return to the phase plan.

When the proposed contract changes final truth, contract approval alone is not enough. The affected
requirements or architecture must also be updated and approved before Pass B begins.

The detailed phase and contract-gate procedure lives in:

```text
.bonsai/phase_execution.md
```

and is loaded only when that workflow is active.

### Pass B: Implementation

Only after approval does the AI build the underlying implementation.

This keeps the human involved at the highest-leverage moment:

> **Before the wrong abstraction becomes a large amount of working code.**

---

## 12. Explicit human gates

Bonsai does not treat “read the prompt” as permission to start editing immediately.

At the beginning of an implementation session, the coding AI:

1. reads the relevant Bonsai memory
2. identifies the active project state
3. surfaces the exact next step
4. classifies its anticipated final-truth impact
5. recommends the appropriate AI level
6. stops at a structured startup gate

The startup gate is an execution decision: proceed with the identified step, request a dry run first,
correct the next step, or stop.

Other gates name what the human is deciding. A phase plan or API contract is **approved**. A named
implementation step is authorized to **proceed**. If execution would materially change approved scope,
contract boundaries, requirements, or architecture, the agent stops and requests a decision instead
of quietly broadening the work or silently rewriting final truth.

That precision matters. It lets the human catch stale state, shift direction, or review a high-value
boundary before the agent commits to the next block of work.

---

## 13. Optional dry runs

When a planned step is risky, unclear, or expensive to reverse, Bonsai can preview execution before
the agent changes files.

A dry run is intentionally compact. It identifies:

* the approved basis for the work
* expected touch points
* intended result
* planned checks
* likely scope concerns
* anticipated final-truth impact and affected truth documents, when any

When the dry run is approved, the agent can compare actual results and actual final-truth impact
against that execution baseline in its completion summary.

The procedure lives in:

```text
.bonsai/dry_run.md
```

and is loaded only when a dry run is requested.

---

## 14. AI effort right-sizing

Not every task deserves the most expensive or capable model.

Bonsai’s implementation workflow asks the coding AI to recommend the appropriate **AI level for the
exact next step** during session startup, and to keep that recommendation current in `state.md` as
the work changes.

That makes model selection part of the operating discipline:

* use stronger reasoning when architecture, contracts, or ambiguous debugging warrant it
* use lighter or cheaper levels for bounded implementation, maintenance, or straightforward
  continuation
* avoid burning maximum AI effort merely because a session has started

This is another way Bonsai keeps AI-assisted development focused, economical, and intentional.

---

## 15. Tool-agnostic and lightweight

Bonsai is intentionally boring technology:

* Markdown files
* plain text prompts
* repo-local structure
* versionable in Git
* usable with many Web AI and coding-agent tools

It does not require you to commit to a proprietary memory backend or a specific editor ecosystem.

If your AI tool can read files and follow instructions, it can probably work with Bonsai.

---

# Getting Started

## Option 1: Try the included example

The fastest way to understand Bonsai is to run the included example project.

This repository already contains:

```text
.bonsai/projects/task-tracker/
```

a small example project memory package produced by a completed Bonsai design session.

Open your AI coding tool and run:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker.
```

The coding AI should:

1. read the `task-tracker` project memory
2. summarize the current implementation state
3. identify the exact next step
4. recommend the appropriate AI level
5. stop at the structured startup gate before making changes

A startup summary should look roughly like this:

```text
Active project: task-tracker

Current phase:
Phase 1 — Establish the initial application contract and core project scaffolding

Exact next step:
Review the active phase plan, then prepare the contract-first implementation work for the first approved slice of the project.

Recommended AI level:
Medium / Thinking

No code changes have been made yet.

1. Proceed with the identified next step.
2. Show a dry run first.
3. Correct the identified next step.
4. Stop here.
```

That startup gate is central to Bonsai. It gives the human a chance to authorize the named work,
inspect it first, or correct stale state before execution begins.

---

## Option 2: Start Bonsai on your own project

### 1. Copy Bonsai into your repository

Copy:

```text
.bonsai/
```

into the root of the repository where you want to use it.

### 2. Create or choose a project memory directory

Each software effort lives under:

```text
.bonsai/projects/<project>/
```

For example:

```text
.bonsai/projects/my-product/
```

### 3. Use a Web UI AI to shape the project

Brainstorm the product, requirements, constraints, architecture, tradeoffs, and implementation approach
in a Web UI AI conversation.

When the design has matured, paste the full contents of:

```text
.bonsai/design_session.md
```

into that same conversation.

The AI will synthesize the discussion into Bonsai project memory.

A typical new project begins with:

```text
requirements.md
architecture.md
plan.md
state.md
```

More detailed layered documents are created only when warranted.

### 4. Save the generated project memory

Place the generated files under:

```text
.bonsai/projects/<project>/
```

For example:

```text
.bonsai/projects/my-product/
├── requirements.md
├── architecture.md
├── plan.md
└── state.md
```

### 5. Start implementation in your coding tool

Run:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>.
```

The AI will summarize the next step, recommend an AI effort level, and stop at a structured startup
gate before execution.

### 6. Add code maps when they become useful

For large, mature, or unfamiliar repositories, build code maps using:

```text
.bonsai/maps/README.md
```

Code maps are optional. Add them when repository rediscovery starts costing real time.

---

# Who Bonsai Is For

Bonsai is for developers who use AI as a serious engineering collaborator, not just an autocomplete
engine.

It is especially useful when:

* a project spans many AI sessions
* you regularly switch between product thinking and implementation
* your codebase is large enough that repository rediscovery is expensive
* you want AI help without surrendering architectural control
* you want to preserve decisions cleanly instead of letting them disappear into old chats
* you expect the product to evolve, pivot, and eventually benefit from a clean rebuild
* you want to manage AI context and AI effort with some discipline instead of treating every task the
  same

If you have ever thought:

> “This AI is useful, but I keep having to teach it the project again,”

Bonsai is meant for that.

---

# Status

Bonsai is an evolving workflow extracted from real AI-assisted software development practice.

It is already useful for:

* shaping a project in Web AI and handing it cleanly to a coding agent
* maintaining durable project memory across many implementation sessions
* keeping agents aligned through structured gates, execution state, and focused next steps
* preserving final truth by surfacing clarifications and blocking unapproved revisions during implementation
* reducing always-loaded implementation instructions through triggered phase and completion procedures
* previewing risky execution with optional compact dry runs
* recommending clean-session continuation after completed work
* mapping large repositories so agents spend less time rediscovering structure
* preserving architectural intent while letting execution state evolve

The system is still being refined. Areas currently evolving include:

* smoother first-time onboarding
* example-driven documentation
* the code mapping workflow
* the balance between layered depth and operational simplicity
* real-project feedback on final-truth reconciliation and triggered implementation procedures
* better conventions for preserving useful discoveries without expanding active scope

---

# Name

A bonsai is not wild growth.
It is growth shaped deliberately over time.

That is the point of this system.

AI can generate enormous amounts of motion.
Bonsai is about turning that motion into deliberate, maintainable software.