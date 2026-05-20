# AI Design Session (Web Synthesis)

## Purpose

We have been brainstorming a project in this chat. Now, transition into the role of a strict
Technical Writer and Systems Architect.

Your task is to synthesize our conversation into a clean, durable Bonsai project memory system
optimized for future implementation by a local IDE-based AI agent.

---

## Output Protocol

Generate the foundational project documents as distinct Markdown code blocks so I can easily copy
and paste them into my local file system.

You must generate:

1. `requirements.md`
2. `architecture.md`
3. `plan.md`
4. `state.md`

Generate optional documents ONLY if our design explicitly demands them:

* `plan/plan_phase_<N>.md`
  *(Only when the initial active phase has already been discussed in enough execution detail that a
  phase-level plan will materially improve the first implementation session. Otherwise, leave
  detailed phase planning to the implementation workflow when the phase becomes active.)*

    * **Two-Pass Contract-First Semantics:** When a generated phase plan uses two-pass
      contract-first execution, Pass A should normally produce both:

        * the reviewable API / structural contract, and
        * tests or usage examples that make the intended behavior concrete for human review.

      Pass A should end at a human review gate. Pass B should implement against the approved
      contract and tests.

* `architecture/architecture_<SUBSYSTEM>.md`
  *(If a subsystem has deep, isolated complexity that should not bloat the top-level architecture.)*

* `requirements/requirements_<AREA>.md`
  *(If a product area has deep, isolated requirement complexity that should not bloat the top-level
  requirements.)*

Do not generate any other project documents unless the user explicitly requests them.

---

## Blocking Clarifications Before Synthesis

Before generating project documents, ask concise clarification questions if any
implementation-shaping foundation is materially unspecified in our discussion.

Ask rather than guess when needed for:

* Primary language or runtime version
* Build tool / package manager
* Test framework
* Repository or module layout, when it affects the plan
* Execution environment, when it constrains implementation

Do not hide missing foundational decisions behind vague assumptions such as
“standard tooling,” “conventional test framework,” or “normal project layout.”

If a missing decision can reasonably shape architecture, phase planning, or the
first implementation step, ask first.

Do not generate project documents while required foundational clarifications remain unanswered,
unless the user explicitly instructs you to proceed despite the uncertainty.

If the user explicitly asks you to proceed without resolving a foundational uncertainty:

* Do not silently choose an answer.
* Preserve the uncertainty prominently in the relevant generated document under
  `Foundational Open Questions`.
* Reflect any implementation consequence in `plan.md` and `state.md` when it affects the roadmap,
  the first phase, or the exact first implementation step.

---

## Synthesis Rules

* **No Hallucinations:** Base the outputs strictly on our chat history. Do not invent features,
  requirements, constraints, or architectural decisions we did not discuss.
* **Identify Gaps:** If a section of a template cannot be filled using our chat, list it under
  `Open Questions` in the appropriate file. Include every materially relevant gap; keep the questions
  concise and prioritized by importance rather than limiting them to an arbitrary count.
* **Foundational Gaps:** Use `Foundational Open Questions` only for unresolved decisions that can
  materially shape architecture, roadmap, execution mode, or the first implementation step.
  Use ordinary `Open Questions` for non-blocking uncertainty.
* **Format:** Adhere strictly to the dense, pipe-delimited `[Meta]` templates provided below.
  Do not add conversational filler outside the code blocks.
* **Project Memory Quality:** Write the generated documents as durable project memory, not as a
  transcript summary. Preserve the final intended product shape, settled design direction, active
  uncertainty, and useful implementation handoff state.
* **Telegraphic Density:** Be compact, specific, and high-signal. Prefer structured statements over
  explanatory prose.
* **No Placeholder Leakage:** Do not leave template placeholders such as `<Project name>`,
  `[List]`, or `<Requirement>` in generated documents. Replace them with real content or, when the
  underlying point is genuinely unresolved, preserve that uncertainty in the relevant questions
  section.

---

## How to Use the Inline Templates Below

The templates embedded later in this document are the required structural schemas for the generated
project files.

Use them as follows:

1. **Select the correct template for each output file.**
   * Use the top-level requirements template for `requirements.md`.
   * Use the top-level architecture template for `architecture.md`.
   * Use the top-level plan template for `plan.md`.
   * Use the state template for `state.md`.
   * Use an area requirements template only when generating
     `requirements/requirements_<AREA>.md`.
   * Use a subsystem architecture template only when generating
     `architecture/architecture_<SUBSYSTEM>.md`.
   * Use a phase plan template only when generating
     `plan/plan_phase_<N>.md`.

2. **Instantiate templates; do not merely repeat them.**
   * Replace every placeholder with synthesized project-specific content.
   * Preserve the document structure, heading order, metadata line style, and dense field format.
   * Do not output the blank templates themselves.

3. **Do not generate optional documents merely because templates exist.**
   * Optional templates are available only when the project discussion clearly justifies those files.
   * If no optional file is warranted, omit it entirely.

4. **Keep cross-document references internally consistent.**
   * If `requirements.md` points to `requirements/requirements_<AREA>.md`, that file must also be generated.
   * If `architecture.md` points to `architecture/architecture_<SUBSYSTEM>.md`, that file must also be generated.
   * If `plan.md` points to `plan/plan_phase_<N>.md`, that file must also be generated.
   * If no linked optional file is generated, the corresponding field must say `None`.

5. **Keep execution state aligned.**
   * `plan.md` and `state.md` must agree on:
     * active phase,
     * phase status,
     * phase execution mode,
     * whether an active phase plan file exists.
   * If a phase plan is generated, `state.md` must reference it.
   * If no phase plan is generated, `state.md` must say `None`.

6. **Use question sections rather than weakening the document.**
   * Do not soften a statement with vague language when the design is actually unresolved.
   * State known decisions plainly.
   * Put unresolved items in `Foundational Open Questions` or `Open Questions`, whichever applies.

7. **Respect ownership boundaries.**
   * Requirements and architecture documents are human-owned durable truth.
   * Plan and state documents are agent-maintained execution memory.
   * Do not let implementation conveniences rewrite product intent or target architecture.

---

## Plan Initialization

In `plan.md`, define:

* The initial roadmap
* The first active phase
* The execution mode of the first active phase, when it can be responsibly determined from the design discussion

Use:

* **Single-pass execution**, when the first phase:
    * implements already-approved behavior,
    * is bounded and localized,
    * has a clear implementation direction,
    * does not materially shape downstream design, and
    * can be safely reviewed after code and tests are produced.

* **Two-pass contract-first execution**, when the first phase:
    * introduces or materially reshapes a public API,
    * defines or changes a schema, persistent format, protocol, extension contract, or integration surface,
    * establishes an important abstraction or subsystem boundary,
    * changes rebuild-relevant structure that later phases will rely on,
    * creates a high-leverage design surface where human review before full implementation is valuable, or
    * is otherwise likely to become costly to reverse after implementation begins.

If the first phase's execution mode cannot be responsibly determined from the design discussion,
set it to `To determine at activation` rather than guessing. In that case, ensure `state.md`
makes execution-mode resolution part of the implementation startup path before substantive work begins.

---

## Phase-Plan Restraint

Do not generate `plan/plan_phase_<N>.md` merely because a phase is active,
complex in the abstract, or two-pass.

Generate it only when our design discussion already contains enough execution-level sequencing,
review gates, or validation detail to justify preserving a phase-level plan before implementation begins.

Otherwise, leave the phase plan absent so the implementation agent can create it closer to execution
when repository reality is available.

---

## State Initialization

In `state.md`, initialize:

* The current phase
* The active phase plan file, if one exists
* The current phase pass
* The phase execution mode, or `To determine at activation` when that is the honest result of synthesis
* The exact first implementation step, expressed at the correct execution unit:
    * use the full current pass through its next review gate for two-pass phases,
    * use the first bounded implementation step for single-pass phases,
    * use phase-mode resolution and any required phase-plan drafting when the mode remains unresolved
* The success condition for that step
* The recommended AI effort level

---

## Two-Pass State Initialization

When the first active phase uses two-pass contract-first execution, initialize `state.md`
so that the exact first implementation step runs the full current pass through its next explicit
human review gate, unless our design discussion explicitly requires a smaller stopping point.

For an initial Pass A, this usually means:

* define the reviewable API / contract shape,
* create behavior-focused tests that demonstrate intended usage and edge cases,
* stop for human review before Pass B implementation.

---

# Inline Output Templates

Use the following templates as the required structure for generated project documents.

---

## Template: `requirements.md`

```markdown
# AI Requirements

**Project:** <Project name>  
**[Meta: Human-owned | Current Product Truth | Bounded Scope | No Implementation Detail]**

## Product Goal & Problem

**Goal:** <What it is and why it exists>  
**Problem Solved:** <What problem it solves, for whom, and why that matters>  
**Primary Users:** [List target users]

## Core Outcomes & Workflows

**Core Outcomes:** [List 3-5 high-level capabilities]

### Workflows

* **<Workflow Name>:** [Trigger] -> [Step 1, Step 2, ...] -> [Success state] (Failures: [List conditions])
* **<Workflow Name>:** [Trigger] -> [Step 1, Step 2, ...] -> [Success state] (Failures: [List conditions])

## Functional Requirements

*If a product area has deep, isolated requirement complexity that should not bloat this top-level
requirements document, create `requirements/requirements_<AREA>.md` and link it here.*

* **FR-1 <Name>:** <Requirement> (Acceptance: [Observable conditions]) | **Details:** <Link to area requirements file or `None`>
* **FR-2 <Name>:** <Requirement> (Acceptance: [Observable conditions]) | **Details:** <Link to area requirements file or `None`>

## Domain Rules & Constraints

* **Core Concepts:** [Concept]: <Definition / Rules> | [Concept]: <Definition / Rules>
* **Behavioral Rules:** [List strict rules]
* **System Constraints:** [List strict constraints]
* **Quality Requirements:** [Usability: X] | [Reliability: Y] | [Performance: Z] | [Integrity: W]

## Exclusions & Accepted Decisions

* **Out of Scope / Non-Goals:** [List specific excluded items]
* **Accepted Decisions:** [List finalized product decisions]
* **Foundational Open Questions:** [Unresolved product-shaping questions that materially affect scope, architecture, roadmap, or the first implementation step, if any]
* **Open Questions:** [List unresolved questions, prioritized by importance]

## Definition of Done

Requirements are satisfied when: [List completion conditions]
```

---

## Template: `requirements/requirements_<AREA>.md`

```markdown
# AI Requirements - <Area Name>

**[Meta: Human-owned | Durable Product-Area Truth | Bounded Scope | No Implementation Detail]**  
**Project:** <Project name> | **Parent:** `../requirements.md`

## Area Goal & Intent

**Area Goal:** <What this product area exists to accomplish>  
**Product Intent:** <What this area is optimizing for from a user or product perspective>

## Scope & Boundaries

* **Owns:** [List product behaviors, workflows, and decisions covered by this area]
* **Does Not Own:** [List adjacent behaviors or product concerns that belong elsewhere]

## Core Outcomes & Workflows

**Core Outcomes:** [List the key user-visible outcomes for this area]

* **<Workflow Name>:** [Trigger] -> [Step 1, Step 2, ...] -> [Success state] (Failures: [List conditions])
* **<Workflow Name>:** [Trigger] -> [Step 1, Step 2, ...] -> [Success state] (Failures: [List conditions])

## Functional Requirements

* **FR-<AREA>-1 <Name>:** <Requirement> (Acceptance: [Observable conditions])
* **FR-<AREA>-2 <Name>:** <Requirement> (Acceptance: [Observable conditions])

## Domain Rules & Constraints

* **Core Concepts:** [Concept]: <Definition/Rules> | [Concept]: <Definition/Rules>
* **Behavioral Rules:** [List strict user-visible or product-level rules]
* **System Constraints:** [List product constraints that shape this area without prescribing implementation]
* **Quality Requirements:** [Usability: X] | [Reliability: Y] | [Performance: Z] | [Integrity: W]

## Relationships to Other Product Areas

* **Depends On:** [Related requirement area or top-level product concept] - <Why>
* **Must Stay Separate From:** [Adjacent area or concern] - <Boundary reason>

## Exclusions & Accepted Decisions

* **Out of Scope / Non-Goals:** [List specific excluded items for this area]
* **Accepted Decisions:** [List finalized product decisions for this area]
* **Open Questions:** [Active product questions, prioritized by importance]

## Definition of Done

This product area is complete when: [List completion conditions]
```

---

## Template: `architecture.md`

```markdown
# AI Architecture

**Project:** <Project name>  
**[Meta: Human-owned | Target Implementation Truth | Rebuild-Grade | No Execution Plans]**

## Architectural Goal & Overview

**Goal:** <Optimization target, e.g., modularity, speed, isolation>  
**System Overview:** <Short 4-8 line description of major moving parts>  
**Principles:** [List core architectural principles]

## Major Subsystems

*If a subsystem has deep complexity, create `architecture/architecture_<SUBSYSTEM>.md` and link
it here.*

* **<Subsystem Name>:** <Purpose> | **Owns:** [Responsibilities] | **Must Not Own:** [Boundaries] |
  **Dependencies:** [List] | **Details:** <Link to subsystem file or `None`>
* **<Subsystem Name>:** <Purpose> | **Owns:** [Responsibilities] | **Must Not Own:** [Boundaries] |
  **Dependencies:** [List] | **Details:** <Link to subsystem file or `None`>

## Canonical Domain Model & Data

* **<Concept>:** <Purpose> | **Owned by:** <Subsystem> | **Properties:** [List] |
  **Lifecycle:** [Rules]
* **State & Persistence:** [List data categories, where they live, persistence rules, and ownership boundaries]

## Flow & Dependencies

* **Allowed / Key Flows:** <Trigger> -> <Path 1, 2, 3> -> <Output> (Failure handling: [Rules])
* **Dependency Rules:** **Allowed:** [Directions] | **Forbidden:** [Directions]

## Cross-Cutting Constraints

* **Extension Model:** [Extension points and rules]
* **Error / Recovery:** [Failure domains and recovery rules]
* **Concurrency:** [Execution model and threading rules]
* **Security / Integrity:** [Boundaries and trust domains]
* **Observability:** [Logging, metrics, and diagnostics expectations]
* **Assumptions:** [Build / Runtime assumptions]

## Guardrails & Rejections

* **Implementation Guardrails:** [Strict technical boundaries to prevent regression]
* **Explicitly Rejected:** [Approach] - [Why rejected]
* **Foundational Open Questions:** [Unresolved architecture-shaping questions that materially affect the target design, if any]
* **Open Questions:** [Active architecture questions, prioritized by importance]
```

---

## Template: `architecture/architecture_<SUBSYSTEM>.md`

```markdown
# AI Architecture - <Subsystem Name>

**[Meta: Human-owned | Durable Subsystem Truth | Rebuild-Grade]**  
**Project:** <Project name> | **Parent:** `../architecture.md`

## Role & Intent

**Role:** <3-6 lines on what this subsystem does in the overall architecture>  
**Architectural Intent:** <What this specific design is optimizing for>

## Boundaries

* **Owns:** [List specific responsibilities]
* **Must Not Own:** [List explicit boundary exclusions]

## Interfaces & Domain

* **Interface: <Name>:** <Purpose> | **Consumers:** [List] | **Rules:** [List]
* **Domain: <Concept>:** <Purpose> | **Properties:** [List] | **Lifecycle:** [Rules]

## Data Flow & Persistence

* **State / Persistence:** [List state categories, where they live, and persistence/ownership rules]
* **Key Flow: <Name>:** <Trigger> -> <Step 1, 2, 3> -> <Output> (Failure: [Handling rule])
* **Key Flow: <Name>:** <Trigger> -> <Step 1, 2, 3> -> <Output> (Failure: [Handling rule])

## Dependencies

* **Allowed Depends On:** [Dependency] - <Why>
* **Forbidden Depends On:** [Forbidden Dependency] - <Why>

## Cross-Cutting Rules

* **Lifecycle:** [Startup/Runtime/Shutdown behavior]
* **Concurrency:** [Threading, locking, and execution rules]
* **Error/Recovery:** [Subsystem-specific fault tolerance]
* **Extension/Config:** [Extension points and configuration model]
* **Security/Integrity:** [Trust boundaries and validation]
* **Observability:** [Logging, metrics, and diagnostics expectations]
* **Assumptions:** [Build or runtime assumptions]

## Guardrails

* **Implementation Guardrails:** [List strict rules preventing regression]
* **Rejected Approaches:** [Approach] - [Why rejected]
* **Open Questions:** [Active design questions, prioritized by importance]
* **Fitness Criteria:** [Condition] | [Condition]
```

---

## Template: `plan.md`

```markdown
# AI Plan

**Project:** <Project name>  
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** <Short statement of execution strategy, sequencing logic, and how phases reduce
risk>

## Roadmap

### Phase Summaries

1. **<Phase 1 Name>:** <Objective> | **Mode:** <To determine at activation / Single-pass / Two-pass contract-first> |
   **Status:** <Pending / Active / Awaiting Review / Blocked / Complete> |
   **Plan:** <`plan/plan_phase_<N>.md` or `None`>
2. **<Phase 2 Name>:** <Objective> | **Mode:** <To determine at activation / Single-pass / Two-pass contract-first> |
   **Status:** <Pending / Active / Awaiting Review / Blocked / Complete> |
   **Plan:** <`plan/plan_phase_<N>.md` or `None`>

## Active Phase Detail

*(Use ONLY if the active phase does not have a separate `plan/plan_phase_<N>.md` file. Otherwise
write: "See active phase plan file.")*

* **Goal:** <Concrete phase outcome>
* **Ordered Steps:**
    1. <Step>
    2. <Step>
* **Validation:** [List phase-level tests, checks, or review gates]
* **Done When:** [List completion conditions]

## Deferred & Completed

* **Deferred:** [List intentionally postponed items]
* **Completed:** [Phase Name] -> Unlocked: [What it enabled]

## Maintenance Rules

* Keep this file focused on the durable execution roadmap, not current-session handoff details.
* Current session status, exact next action, blockers, current pass state, and recommended AI level belong in `state.md`.
* Keep phase status, execution mode, and active phase plan references consistent with `state.md`.
* When `state.md` records a phase-level or pass-level transition, verify whether this roadmap also requires a corresponding update.
* Add a separate `plan/plan_phase_<N>.md` when a phase requires deep sequencing, two-pass execution,
  multiple meaningful review or validation gates, or enough detail that it would bloat this file.
* When a `plan/plan_phase_<N>.md` file exists, treat it as the authoritative detailed plan for that phase.
  Do not partially duplicate phase-level sequencing here.
* If an active phase plan file exists but is incomplete, stale, or inconsistent with current approved
  project direction, update that phase plan rather than expanding `Active Phase Detail`.
* Use `Mode: To determine at activation` when the execution mode should be resolved closer to implementation
  rather than guessed prematurely.
* Compress completed phase detail aggressively once it no longer helps execution.
```

---

## Template: `plan/plan_phase_<N>.md`

```markdown
# AI Plan - Phase <N>: <Phase Name>

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**
**Project:** <Project name> | **Parent:** `plan.md`
**Status:** <Not started | Active | Awaiting Review | Blocked | Complete>
**Mode:** <Single-pass | Two-pass contract-first>

## Objective & Scope

**Objective:** <Concrete outcome this phase must produce>
**Inputs:** [Requirements Section] | [Architecture Section] | [Prior Phase Output]
**In Scope:** [List items]
**Out of Scope / Do Not Do Yet:** [List items]
**Expected Deliverables:** [List deliverables]

## Ordered Work

*(Note: If Single-Pass, delete Pass A and use only Pass B / Implementation steps.)*

### Pass A: Contract (Review Gate)

* **Step A1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step A2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

Pass A should normally produce:

* the reviewable API, structural contract, or design surface being established, and
* behavior-focused tests, usage examples, or equivalent review artifacts that make the intended
  behavior concrete before full implementation.

**Stop here for Human Review of the contract and review artifacts before Pass B.**

### Pass B: Implementation (Or Single-Pass)

* **Step B1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step B2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

## Validation & Done Criteria

* **Validation Strategy:** [List specific tests, manual checks, and verifications]
* **Definition of Done:** [List completion conditions. For two-pass, include "Faithful to approved contract"]

## Context & Wrap-up

* **Dependencies:** [List known dependencies]
* **Risks:** [List known risks]
* **Open Questions:** [Active execution questions, prioritized by importance]
* **Completion Summary:** *(Fill when done)* **Outcome:** [Results] |
  **Unlocked:** [Next capability]

## Maintenance Rules

* Treat this file as the authoritative detailed execution plan for this phase.
* Keep `plan.md` at roadmap level. Do not duplicate phase-level sequencing there.
* Keep `state.md` aligned with this file for:
    * current pass,
    * exact next step,
    * review-gate status,
    * blockers,
    * phase completion state.
* When a pass boundary, review gate, blocker state, or phase status changes, verify whether
  `state.md` and `plan.md` require corresponding updates.
* If this phase plan becomes incomplete, stale, or inconsistent with current approved project
  direction, correct it before substantive phase execution continues.
* Compress completed phase detail when it no longer helps execution, while preserving enough
  summary to explain the outcome and what it unlocked.
```

---

## Template: `state.md`

```markdown
# AI State

**Project:** <Project name>  
**[Meta: Agent-maintained | Current Session Baton Pass | Volatile Operational Truth | Keep Minimal]**

## Current Execution State

**Current Phase:** <Phase Name>  
**Active Phase Plan File:** <`plan/plan_phase_<N>.md` or `None`>  
**Current Phase Pass:** <Not applicable | Pass A (Contract) | Awaiting Review | Pass B (Implementation)>  
**Phase Execution Mode:** <Single-pass | Two-pass contract-first | To determine at activation>  
**Current Objective:** <Single concrete objective>

* **Snapshot / Recent Work:** <2-3 lines on the current reality and the most recent meaningful work completed>
* **Active Files:** [List 3-7 resume-critical files only; not a list of every recently touched file]
* **Blockers / Risks:** [List active blockers, uncertainties, or review dependencies]

**Exact Next Step:** <Action>  
**Success Condition:** <What must be true when the next step is complete>  
**Recommended AI Level:** <Fast / Medium / Thinking / Max> - <Reason>

## Maintenance Rules

* Overwrite stale state instead of accumulating history.
* Keep this file short enough to read at every implementation-session startup.
* Use `Active Files` only for files the next implementation session is likely to resume in immediately.
* Do not use `Active Files` as a touched-files list, change log, or broad working-set inventory.
* Do not duplicate roadmap summaries from `plan.md`.
* Do not duplicate detailed phase sequencing from `plan/plan_phase_<N>.md`.
* Keep phase execution mode consistent with `plan.md` and any active `plan/plan_phase_<N>.md`.
* When recording a phase-level or pass-level transition, verify whether `plan.md` or the active phase plan also requires a corresponding update.
* Update after each meaningful execution step, review gate, blocker change, phase transition, pass transition, active phase plan change, or execution mode change.
```
