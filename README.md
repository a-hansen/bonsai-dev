# Bonsai

**Structured project memory for serious AI-assisted software development.**

Bonsai is a repo-local memory system and workflow for using AI to design, build, and evolve software
over many sessions without losing the thread.

It helps you:

* start fresh AI sessions frequently without starting over
* keep context small, structured, and high-signal
* move cleanly from Web AI design to IDE / CLI implementation
* preserve product intent, architecture, roadmap, current execution state, and useful out-of-scope observations separately
* layer deep product requirements and subsystem architecture without bloating top-level project memory
* guide coding agents through large codebases using layered code maps
* right-size AI effort instead of burning maximum reasoning on every step
* keep the human in the loop before an agent hardens the wrong abstraction
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
    ├── design_prompt.md
    ├── implementation_prompt.md
    ├── style_guide.md
    ├── maps/
    │   └── ...
    └── projects/
        └── ...
```

The repo root is the public project landing page.
The `.bonsai/` directory is the actual framework you copy into another repository.

---

# TL;DR

## Add Bonsai to a project

Copy:

```text
.bonsai/
```

into the root of the repository where you want to use it.

Then follow:

```text
.bonsai/README.md
```

for the project workflow.

---

## Start a design session

Use a Web UI AI to brainstorm the product, architecture, constraints, and tradeoffs.

When the design has matured, paste the contents of:

```text
.bonsai/design_prompt.md
```

into the conversation, along with the relevant Bonsai templates.

The AI will synthesize the conversation into durable project memory:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`

and, when warranted:

* `icebox.md`
* `plan_phase_<N>.md`
* `requirements/requirements_<AREA>.md`
* `architecture/architecture_<SUBSYSTEM>.md`

---

## Start an implementation session

Open your AI coding tool and begin with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>.
```

The AI will load the relevant Bonsai memory, summarize the current execution state, recommend the
appropriate AI level for the exact next step, and then stop for human approval or redirection before
execution begins.

This is the command you will use over and over.

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

Bonsai supports optional layered documents for both product and architecture depth:

```text
requirements/requirements_<AREA>.md
architecture/architecture_<SUBSYSTEM>.md
```

Use these when a product area or architectural subsystem has deep, isolated complexity that would
otherwise bloat the top-level documents.

The top-level files retain the project-wide truth.
The layered files preserve detailed truth that can be loaded only when relevant.

---

## 3. Frequent fresh-session workflow

Bonsai is designed around the idea that **fresh sessions are good**.

Instead of stretching one AI conversation until it becomes a swamp, you:

1. end the current session when appropriate
2. let `state.md` preserve the baton pass
3. start a new session
4. reload only the meaningful project memory
5. continue cleanly

This keeps reasoning sharper and conversations easier to manage.

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

A large project should not require dumping the entire project history into every AI session.

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
scratchpads.

### Agent-maintained execution memory

* `plan.md`
* `state.md`
* `icebox.md`
* `plan_phase_<N>.md`

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
plan_phase_<N>.md
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
* Should implementation proceed?

### Pass B: Implementation

Only after approval does the AI build the underlying implementation.

This keeps the human involved at the highest-leverage moment:

> **Before the wrong abstraction becomes a large amount of working code.**

---

## 12. A startup gate before implementation begins

Bonsai does not treat “read the prompt” as permission to start editing immediately.

At the beginning of an implementation session, the coding AI:

1. reads the relevant Bonsai memory
2. identifies the active project state
3. surfaces the exact next step
4. recommends the appropriate AI level
5. stops for human approval or redirection

That pause matters.

It lets the human catch stale state, shift direction, or change priorities before the agent commits to
the next block of work.

---

## 13. AI effort right-sizing

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

## 14. Tool-agnostic and lightweight

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

1. Copy `.bonsai/` into your repository.
2. Read `.bonsai/README.md`.
3. Use a Web UI AI session to create your first project memory.
4. Start implementation with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>.
```

5. Review the startup summary, then approve or redirect the agent before execution begins.
6. For large or unfamiliar repos, build code maps using:

```text
.bonsai/maps/README.md
```

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

Bonsai is an evolving workflow extracted from real AI-assisted development practice.

The current system focuses on:

* structured project memory
* design-to-implementation handoff
* execution continuity
* startup-gated implementation sessions
* context minimization
* layered requirements and architecture
* contract-first development
* scoped preservation of out-of-scope observations
* layered codebase guidance
* AI effort right-sizing
* clean rebuildability after early product pivots

---

# Name

A bonsai is not wild growth.
It is growth shaped deliberately over time.

That is the point of this system.

AI can generate enormous amounts of motion.
Bonsai is about turning that motion into deliberate, maintainable software.
