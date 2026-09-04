# Bonsai

**Structured project memory and execution workflow for AI-assisted software development.**

Current release: **v2.0.0**

Bonsai is a Markdown-based memory system and workflow for developers who use AI to design, build, and evolve software across many sessions.

It helps you:

* preserve product and architecture truth outside chat history
* start fresh AI sessions without re-explaining the project
* keep requirements, architecture, execution planning, current state, and operational knowledge separate
* let coding agents maintain execution memory without surrendering human control of what is being built
* plan and execute work through explicit, reviewable phase boundaries
* carry one exact next action safely across a fresh-session boundary
* guide agents through large or multi-repository source trees with reusable code maps
* preserve useful environment and tooling discoveries so they do not need to be rediscovered every session

Bonsai is plain Markdown plus a small set of prompts, skills, and templates.

No server.  
No database.  
No external memory service.  
No agent framework lock-in.

It is a workflow built by a developer for developers who want AI to remain useful over the life of a real project, not just for one good chat.

For the complete operating guide, including installation models, migration, Bonsai Home, embedded use, project management, and detailed workflows, see [.bonsai/README.md](.bonsai/README.md).

---

# What's New in Bonsai 2.0

Bonsai 2.0 is a substantial redesign rather than an incremental update to 1.x.

The biggest changes are:

* **A reusable Bonsai Home with `BONSAI_HOME`.** Bonsai no longer has to carry the full framework inside every repository. A shared Bonsai Home can provide the current standard, prompts, skills, templates, reusable context, and a central code-map store. Upgrade Bonsai once and participating repositories can use the new version without copying the framework into each repo.

* **A formal Bonsai specification.** `specification.md` is now the authoritative human-owned truth for Bonsai itself. Prompts, skills, templates, bootstrap files, and other framework artifacts implement that specification rather than defining behavior independently. This gives Bonsai development a clear source of truth and makes framework changes much easier to reason about.

* **Bonsai now develops itself.** Bonsai 2.0 was designed, implemented, validated, and promoted through the persistent `bonsai-dev` project using Bonsai's own workflow. That project remains the durable development memory for continued Bonsai evolution.

* **One canonical startup path.** Coding sessions begin with:

  ```text
  Read .bonsai/start.md and follow its instructions.
  ```

  The small repository-local bootstrap resolves the Bonsai Home, repository, and active project before loading the standard implementation workflow.

* **Fresh-session continuation can execute the exact next step immediately.** At an appropriate boundary, Bonsai can generate a fresh-session prompt that reconstructs canonical state and executes the already-authorized exact next action without stopping at the normal startup gate. Independent approval, review, blocker, and final-truth gates still remain intact.

* **Code maps are reusable Bonsai assets.** Maps are integrated into the normal Bonsai workflow and stored centrally under Bonsai Home when one is active. They are tied to the source they describe rather than to a particular Bonsai project, so multiple projects can reuse the same map and multi-repository work becomes much cleaner.

* **Web UI workflows produce repository-ready artifacts.** Project-memory creation and map calibration produce ZIPs meant to be extracted directly at the repository root, reducing setup to a straightforward design → extract → start workflow.

# Try Bonsai First

This repository includes two examples with different purposes.

## Bonsai Testbed

`bonsai-testbed-project.zip` is the quickest way to see the Bonsai 2.0 workflow itself.

The application is deliberately tiny so the interesting part is Bonsai:

* project-memory startup
* Phase 1 planning
* execution gates
* agent-maintained state
* contract-first work when appropriate
* fresh-session continuation
* operational context
* later-phase planning
* correct phase and body-of-work completion

The testbed is also the fixture used while dogfooding Bonsai 2.0. It exists to make workflow behavior easy to observe without a substantial application getting in the way.

Extract the ZIP into a throwaway repository root, then start with:

```text
Read .bonsai/start.md and follow its instructions.
```

The repository still needs access to a valid Bonsai 2.0 standard, either through your configured Bonsai Home or an Embedded Bonsai installation. See [.bonsai/README.md](.bonsai/README.md) for setup details.

## Task Tracker

The included Task Tracker is a fuller example of Bonsai project memory around a small application.

It shows what requirements, architecture, execution planning, and state look like when Bonsai is attached to a real piece of software rather than a workflow test fixture.

See:

[Task Tracker Example](.bonsai/projects/task-tracker/README.md)

Start it with:

```text
Read .bonsai/start.md and follow its instructions. Active project: task-tracker.
```

---

# The Prompt You Will Use a Lot

For normal implementation work:

```text
Read .bonsai/start.md and follow its instructions.
```

That prompt is intentionally boring.

You do not need to reconstruct the correct implementation instructions every time you open a coding session. You do not need to summarize the previous session. You do not need to remember which project files, plans, context, maps, or skills the agent should load.

The local `start.md` establishes the repository anchor and routes the session into the active Bonsai standard. Bonsai then reconstructs the current project state and determines the next applicable gate or exact action.

For a repository with multiple named projects, you may specify one directly:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

If you do not, Bonsai can resolve `main`, select the only available project, or ask you to choose among multiple projects.

The project memory carries the continuity. The startup prompt stays small.

---

# How Bonsai Organizes Project Memory

A normal Bonsai project begins with four core memory files:

```text
.bonsai/projects/main/
├── requirements.md
├── architecture.md
├── agent_plan.md
└── agent_state.md
```

They have deliberately different jobs.

| File | Purpose | Ownership |
| --- | --- | --- |
| `requirements.md` | Product behavior, scope, and constraints | Human-owned |
| `architecture.md` | Intended system architecture and durable technical decisions | Human-owned |
| `agent_plan.md` | Implementation roadmap and phase-level execution state | Agent-maintained |
| `agent_state.md` | Current resume state and exact next step | Agent-maintained |

That separation is central to Bonsai.

Requirements should not turn into a progress log. Architecture should not quietly mutate to match whatever code happened to get written. Execution state should not become a diary of previous sessions.

Optional memory appears only when it is useful:

```text
.bonsai/projects/main/
├── agent_context.md
├── icebox.md
├── plan/
│   └── agent_plan_phase_1.md
├── requirements/
│   └── requirements_<AREA>.md
└── architecture/
    └── architecture_<SUBSYSTEM>.md
```

Bonsai also supports repository-level and reusable developer-level context, but those details belong in the operating guide.

---

# Design a Project in the Web UI

Bonsai assumes that product and architecture design often begin in a Web AI conversation.

Discuss the project normally:

* what you are building
* requirements and workflows
* scope and constraints
* architecture
* alternatives and tradeoffs
* implementation strategy

Do not force the conversation into Bonsai documents prematurely.

When the design is mature enough to preserve, use:

```text
prompts/create_project_memory.md
```

in that same conversation.

For a new project, the workflow resolves the project name and generates a ZIP meant to be extracted directly at the repository root.

Its core shape is:

```text
.bonsai/
├── start.md
└── projects/
    └── <project>/
        ├── requirements.md
        ├── architecture.md
        ├── agent_plan.md
        └── agent_state.md
```

Additional project memory appears only when the design genuinely needs it.

Extract the ZIP into the target repository root, review the generated human-owned final truth, and then begin implementation with:

```text
Read .bonsai/start.md and follow its instructions.
```

For a normal simple repository, `main` is the conventional project name. Named projects are useful when one repository contains several independent bodies of work.

The generated `start.md` creates the repository-local Bonsai entry point. The Bonsai standard itself may come from a reusable Bonsai Home or from a complete Embedded Bonsai installation. The detailed setup rules live in [.bonsai/README.md](.bonsai/README.md).

---

# Calibrate a Code Map in the Web UI

Source inspection is authoritative, but a repository owner often knows things that are expensive or unreliable for an agent to infer from source alone.

For example:

* which subsystems actually matter
* which entry points show representative usage
* which large areas are misleading or low-value
* where extension surfaces live
* what should be mapped deeply
* what should remain out of scope

Use:

```text
prompts/create_map_calibration.md
```

to preserve that knowledge before building a code map.

The workflow produces a repository-root ZIP containing human-owned calibration under:

```text
.bonsai/
└── maps/
    └── <source>/
        └── map_calibration.md
```

Extract it at the repository root.

The calibration is guidance, not source truth and not the map itself. Bonsai's mapping workflow later combines it with actual source to create or update the reusable code map.

A source does not need Bonsai project memory in order to be mapped.

---

# Fresh Sessions Are a Feature

Long AI sessions tend to accumulate noise:

* stale decisions
* abandoned approaches
* old debugging branches
* duplicated context
* assumptions that were true earlier but no longer matter

Bonsai is designed around a different model:

> **Keep durable memory in the project. Start clean sessions whenever it is useful.**

`agent_state.md` acts as the baton pass.

It records only the current execution condition, blockers or risks that still matter, resume-critical files, the exact next step, and the success condition.

At a natural boundary, Bonsai can also offer to continue one exact next action in a fresh session. The continuation prompt does not carry a handwritten summary of volatile state. The new session reconstructs the canonical state from project memory before it acts.

If you exit instead, Bonsai gives you the ordinary startup prompt so you can resume later without changing durable state merely to record that you stopped.

---

# Keep Final Truth Separate from Execution

Software development is messy.

Requirements sharpen. APIs change. Early designs turn out to be wrong. Implementation exposes assumptions that were never written down.

That is normal.

What Bonsai tries to prevent is allowing those discoveries to silently redefine the project.

`requirements.md` and `architecture.md` describe the intended system. During implementation, Bonsai distinguishes between:

* **None:** the current final truth already covers the work
* **Clarification:** the intended design is unchanged, but the truth should be stated more precisely
* **Revision:** product behavior, architecture, constraints, or system boundaries actually need to change

A revision requires human approval before it becomes the new direction.

The goal is for mature project memory to describe the system you ultimately decided to build, not every detour taken to discover it.

That gives Bonsai another useful property:

> **A mature project can be rebuilt from its final intended form rather than from the scars of its prototype history.**

---

# Human Control Without Constant Babysitting

Bonsai is intentionally human-centered, but it does not require approval for every file edit.

The coding agent maintains execution memory such as `agent_plan.md`, `agent_state.md`, phase plans, and qualifying operational context.

The human retains authority over product and architecture truth.

Every phase has an execution basis. Phase 1 always begins with a detailed plan review. Later phases still pass through planning, but Bonsai creates a detailed phase plan only when the work benefits from one.

For durable contracts such as externally consumed APIs, schemas, protocols, persistent formats, or extension surfaces, Bonsai can use contract-first two-pass execution:

1. produce the smallest useful reviewable contract surface
2. stop for human approval
3. implement beneath the approved contract

At meaningful boundaries, Bonsai stops and asks for a decision instead of treating the initial prompt as unlimited permission to continue.

The goal is simple:

> **Let the agent manage execution. Keep the developer in control of what is being built and why.**

---

# Large Repositories Need Navigation Memory Too

Project memory answers questions such as:

* What are we building?
* What architecture are we aiming for?
* What phase are we in?
* What happens next?

Large codebases introduce another recurring problem:

* Where is the relevant code?
* Which subsystem owns this behavior?
* What callers or extension points matter?
* What should the agent inspect before changing it?

Bonsai includes layered code maps for that problem.

Maps are named for the source they represent, not for whichever Bonsai project happened to create them. That makes them reusable across projects and especially useful when one project's source universe spans several repositories.

Optional human-owned `map_calibration.md` can tell the mapping workflow what deserves attention, what is misleading, and what should remain out of scope. Actual source remains authoritative.

The maps are not a substitute for reading source code. They help the agent find the right source code faster and avoid rediscovering the same repository structure every session.

---

# Bonsai Learns Operational Context Too

Not every useful discovery belongs in requirements, architecture, or execution state.

During real work an agent may discover facts such as:

* the correct build command in this environment
* a stable external source location
* a reusable code map
* a filesystem or tool limitation
* an environment-specific working rule

When a discovery is durable, actionable, sufficiently supported, and likely to matter again, Bonsai can preserve the current working rule in `agent_context.md`.

Agent context can be scoped to the developer environment, repository, or individual project.

That turns useful discovery into reusable operational memory without polluting product truth or preserving troubleshooting history.

---

# Bonsai Is Not an Agent Framework

Bonsai does not try to orchestrate a fleet of agents.

It does not replace `AGENTS.md`, repository instructions, coding standards, or your preferred AI tool.

Those solve different problems.

Bonsai focuses on durable project memory and execution continuity:

* product truth
* architecture truth
* execution roadmap
* current resume state
* operational context
* deeper project detail when needed
* repository navigation knowledge

Use it with one assistant, an IDE coding agent, a CLI agent, or a larger multi-agent system.

Better project memory helps all of them.

---

# Embedded Bonsai and Bonsai Home

Bonsai 2.0 supports two installation models.

A repository can contain a complete **Embedded Bonsai** standard inside its own `.bonsai` directory.

Or a reusable **Bonsai Home** can provide the shared standard, prompts, skills, templates, developer context, agent context, and reusable maps while each repository keeps only its local bootstrap and repository/project memory.

The implementation workflow is the same either way.

The details matter, especially for setup, migration, multi-repository work, and `BONSAI_HOME`, but they are operating-guide material rather than landing-page material.

See [.bonsai/README.md](.bonsai/README.md).

---

# Who Bonsai Is For

Bonsai is for developers who use AI as an engineering collaborator rather than only as autocomplete.

It becomes especially useful when:

* a project spans many AI sessions
* design and implementation happen in different tools
* you are tired of re-explaining the project to every new session
* the codebase is large enough that repository rediscovery costs real time
* the useful source universe spans multiple repositories
* you want the agent to manage execution without surrendering product or architecture control
* the project is likely to evolve, pivot, and accumulate deeper detail over time
* you want project memory to live close to the code instead of disappearing into chat history

If you have ever started a new coding session and thought:

> “I know the AI can help, but now I have to teach it the project again.”

Bonsai is meant to remove that part.

---

# Why Bonsai Exists

I built Bonsai out of the friction of using AI on real software projects.

The problem was not that the models could not write code.

The problem was continuity.

One session would contain important design decisions. Another would discover a better architecture. A coding agent would make progress, but the next session would need a careful recap. Large repositories would get rediscovered repeatedly. Old conversation context would become more expensive and less useful at the same time.

The obvious answer seemed to be more context.

For me, the better answer turned out to be **better-structured context**.

Bonsai keeps that structure in plain Markdown because Markdown is easy to inspect, diff, edit, version, copy, and hand to almost any AI tool.

The technology is deliberately boring.

The workflow is the product.

---

# Status

Bonsai 2.0 was developed using Bonsai itself.

The persistent `bonsai-dev` project carried the redesign through planning, implementation, validation, promotion, and subsequent workflow improvements. The self-hosting project remains active so later Bonsai changes can continue through the same project-memory and execution model the framework provides to its users.

The separate Bonsai Testbed was used to exercise and refine the v2 workflow against deliberately small code, making lifecycle and interaction defects easier to expose.

Bonsai will keep evolving as real use exposes places where the workflow helps or gets in the way.

The core idea is stable:

> **Keep durable project memory structured, selective, current, and close to the code.**

---

# Name

A bonsai is not wild growth.

It is growth shaped deliberately over time.

AI can generate enormous amounts of motion. Bonsai is about turning that motion into deliberate, maintainable software.
