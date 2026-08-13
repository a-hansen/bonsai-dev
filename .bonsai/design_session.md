# AI Design Session (Web Synthesis)

## Purpose

We have been brainstorming a project in this chat. Now, transition into the role of a strict
Technical Writer and Systems Architect.

Your task is to synthesize our conversation into a clean, durable Bonsai project memory system
optimized for future implementation by a local IDE-based AI agent.

Bonsai governs project-memory and execution workflow. It must preserve the user's approved design
without imposing unrelated coding style, testing style, abstraction preferences, framework patterns,
or other software-engineering conventions that belong to project guidance, developer context, or
external skills.

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

    * **Two-Pass Contract-First Semantics:** Use two-pass contract-first execution only when the phase
      establishes or changes a contract or design surface that independently merits human approval
      before implementation.

      Pass A should normally produce:

        * the reviewable contract, API shape, schema, protocol surface, extension contract, persistent
          format, or other approved design surface being established, and
        * tests, usage examples, schemas, signatures, examples, or other review artifacts only when
          they materially clarify the intended contract and are appropriate for the project.

      Pass A does not require interfaces, builders, adapters, abstraction layers, new module seams,
      or other implementation indirection merely because Bonsai uses the word `contract`.

      If approved architecture already defines module or dependency boundaries relevant to the
      contract, preserve and make those boundaries reviewable. Do not invent additional boundaries
      solely to satisfy the gate.

      Pass A ends at a human review gate. Pass B implements against the approved contract and
      approved project architecture.

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
* Test framework, when it materially affects the architecture or first implementation step
* Repository or module layout, when it materially affects the architecture or first implementation step
* Execution environment, when it constrains implementation
* Required module boundaries or dependency direction, when they are part of the intended architecture

Do not ask about development-style choices merely because they could influence implementation.
Coding conventions, test philosophy, abstraction preferences, local SDK paths, recurring AI
preferences, and similar developer-specific concerns belong in project guidance,
`.bonsai/developer_context.md`, or external skills unless they materially shape the approved product
or architecture.

Do not hide missing foundational decisions behind vague assumptions such as
“standard tooling,” “conventional test framework,” “normal project layout,” or “clean modular design.”

If a missing decision can reasonably shape architecture, roadmap, execution mode, or the
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

## Module Boundary Clarification

Clarify module boundaries only when they materially affect target architecture, a durable public
contract, dependency direction, or the first implementation phase.

When module shape is already part of the intended design, capture:

* **Major modules:** Human-digestible implementation areas the architecture is intended to preserve.
* **Public seams:** Externally consumed APIs, schemas, protocols, extension points, entry points, or
  other durable contracts, when any.
* **Dependency direction:** Explicit dependency constraints that are part of the intended design.
* **Forbidden coupling:** Only coupling explicitly rejected by the approved design.

Do not require a project to define public interfaces, internal seams, dependency layers, adapters,
builders, or abstraction boundaries merely because it contains multiple implementation concerns.

If the user does not know a module shape that materially affects architecture, propose the smallest
candidate needed to resolve the architectural question and ask for approval.

If module shape is intentionally deferred, preserve that under `Foundational Open Questions` or make
the necessary discovery part of the first phase.

---

## Synthesis Rules

* **No Hallucinations:** Base the outputs strictly on our chat history. Do not invent features,
  requirements, constraints, or architectural decisions we did not discuss.
* **Identify Gaps:** If a section of a template cannot be filled using our chat, list it under
  `Open Questions` in the appropriate file. Include every materially relevant gap; keep the questions
  concise and prioritized by importance rather than limiting them to an arbitrary count.
* **Foundational Gaps:** Use `Foundational Open Questions` only for unresolved decisions that can
  materially shape architecture, roadmap, execution mode, module boundaries, dependency direction, or
  the first implementation step. Use ordinary `Open Questions` for non-blocking uncertainty.
* **Human-Digestible Architecture:** Preserve module, subsystem, protocol, persistence, domain,
  adapter, UI, or dependency boundaries when they are part of the approved intended design.
  Do not manufacture additional architecture to make the project appear more modular.
* **Workflow Neutrality:** Bonsai must not prescribe interfaces, builders, dependency-injection
  patterns, class structure, testing philosophy, mocking strategy, or other coding style unless those
  choices are part of approved project truth.
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
        * whether an active phase plan file exists,
        * phase-plan approval state when a phase plan exists.

    * If a phase plan is generated, `state.md` must reference it.
    * If no phase plan is generated, `state.md` must say `None`.
    * `state.md` must make execution readiness explicit.

6. **Use question sections rather than weakening the document.**

    * Do not soften a statement with vague language when the design is actually unresolved.
    * State known decisions plainly.
    * Put unresolved items in `Foundational Open Questions` or `Open Questions`, whichever applies.

7. **Respect ownership boundaries.**

    * Requirements and architecture documents are human-owned durable truth.
    * Plan, phase plans, and state documents are agent-maintained execution memory.
    * Developer-local preferences, SDK paths, machine-specific setup, recurring AI session preferences,
      coding style, test style, and local build/runtime quirks belong in
      `.bonsai/developer_context.md`, project guidance, or external skills rather than project memory.
    * Do not generate `.bonsai/developer_context.md` unless the user explicitly asks for developer-local
      context.
    * Do not let implementation conveniences rewrite product intent or target architecture.

---

## Plan Initialization

In `plan.md`, define:

* The initial roadmap
* The first active phase
* The execution mode of the first active phase, when it can be responsibly determined from the design discussion
* The active phase-plan approval state when a separate phase plan exists

Use:

* **Single-pass execution**, as the normal mode when the phase can be implemented and reviewed without
  first approving a separate durable contract.

* **Two-pass contract-first execution**, when the phase establishes or materially changes a contract
  that independently merits human approval before implementation, such as:

    * an externally consumed API,
    * a schema or persistent format,
    * a protocol or message contract,
    * an extension/plugin contract,
    * an integration surface,
    * another durable design surface that downstream code or external consumers will rely on.

Do not select two-pass contract-first execution merely because the phase:

* is large or complex,
* introduces new classes or packages,
* contains multiple implementation concerns,
* creates internal helper abstractions,
* would benefit from ordinary code review,
* touches more than one module,
* needs tests.

If a durable contract that governs the phase has already been explicitly approved outside the current Bonsai
pass, do not create a redundant contract gate merely because implementation depends on that contract. Use
single-pass execution unless the phase is establishing or materially changing another review-worthy durable contract.

If the first phase's execution mode cannot be responsibly determined from the design discussion,
set it to `To determine at activation` rather than guessing. In that case, ensure `state.md`
makes execution-mode resolution part of the implementation startup path before substantive work begins.

---

## Phase-Plan Restraint

Do not generate `plan/plan_phase_<N>.md` merely because a phase is active,
complex in the abstract, or uses multiple files.

Generate it only when our design discussion already contains enough execution-level sequencing,
review gates, scope constraints, contract detail, or validation detail to justify preserving
a phase-level plan before implementation begins.

A two-pass phase normally requires a phase plan because its contract review gate must be explicit.

Otherwise, leave the phase plan absent so the implementation workflow can create one closer to
execution, when repository reality is available.

When a phase plan is generated during synthesis:

* Set its `Plan Status` to `Ready for Review`, not `Approved`.
* Set `state.md` execution readiness to `Awaiting human review`.
* Make review of that phase plan the exact next step.

---

## State Initialization

In `state.md`, initialize:

* The current phase
* The active phase plan file, if one exists
* The phase-plan approval state, if one exists
* The current phase pass
* The phase execution mode, or `To determine at activation` when that is the honest result of synthesis
* Explicit execution readiness
* The exact first implementation step, expressed at the correct execution unit
* The success condition for that step

Use these execution-readiness values:

* `Design required` - product or architecture decisions must be resolved first.
* `Phase planning required` - durable design is sufficient, but execution planning must occur first.
* `Awaiting human review` - a plan, contract, or other required artifact is ready for human review.
* `Ready to execute` - the exact next implementation step has an approved basis and no planning gate remains.
* `Blocked` - execution cannot safely continue until a stated blocker is resolved.
* `Complete` - no further implementation step is currently required.

For a two-pass phase, the first executable Pass A step should cover the approved contract work
through its next review gate unless the design explicitly requires a smaller unit.

For a single-pass phase, set `Current Phase Pass: Single-pass Implementation` and use the first bounded
implementation step. Reserve `Pass A (Contract)`, `Contract Review`, and `Pass B (Implementation)` for
actual two-pass contract-first phases. A single-pass phase must never be represented as Pass B.

When execution mode remains unresolved, use mode resolution and any required phase-plan drafting as
the exact next step.

---

## Two-Pass State Initialization

When the first active phase uses two-pass contract-first execution, initialize `state.md`
so that the exact first implementation step runs the current pass through its next explicit human
review gate, unless our design discussion explicitly requires a smaller stopping point.

For an initial Pass A, this usually means:

* define the reviewable contract or durable design surface,
* preserve relevant approved architecture boundaries,
* create tests, usage examples, schema examples, signatures, or other review artifacts only when they
  materially clarify that contract and fit project conventions,
* stop for human review before Pass B implementation.

Pass A does not require adding interfaces or other implementation indirection unless the approved
design itself requires them.

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

**Goal:** <Primary architectural optimization target>  
**System Overview:** <Short 4-8 line description of major moving parts>  
**Principles:** [List approved architectural principles]

## Major Subsystems

*If a subsystem has deep complexity, create `architecture/architecture_<SUBSYSTEM>.md` and link
it here.*

* **<Subsystem Name>:** <Purpose> | **Owns:** [Responsibilities] | **Must Not Own:** [Approved boundaries or `None`] |
  **Dependencies:** [Approved dependencies or `None`] | **Details:** <Link to subsystem file or `None`>
* **<Subsystem Name>:** <Purpose> | **Owns:** [Responsibilities] | **Must Not Own:** [Approved boundaries or `None`] |
  **Dependencies:** [Approved dependencies or `None`] | **Details:** <Link to subsystem file or `None`>

## Module Boundaries & Dependency Shape

* **Human-Digestible Modules:** [Approved major modules/layers/packages, or `Not prescribed`]
* **Module Ownership:** [Approved ownership rules, or `Not prescribed`]
* **Public Seams:** [Externally or durably consumed seams and contracts, or `None`]
* **Dependency Direction:** **Allowed:** [Approved directions or `Not prescribed`] | **Forbidden:** [Explicitly forbidden directions or `None`]
* **Boundary Rules:** [Approved architectural boundaries only, or `None`]
* **Review Anchors:** [Files, schemas, examples, interfaces, entry points, or other artifacts that make important approved design surfaces inspectable, or `None`]

## Canonical Domain Model & Data

* **<Concept>:** <Purpose> | **Owned by:** <Subsystem or `Not prescribed`> | **Properties:** [List] |
  **Lifecycle:** [Rules]
* **State & Persistence:** [List data categories, persistence rules, and ownership boundaries]

## Flow & Dependencies

* **Allowed / Key Flows:** <Trigger> -> <Path 1, 2, 3> -> <Output> (Failure handling: [Rules])
* **Dependency Rules:** **Allowed:** [Approved directions or `Not prescribed`] | **Forbidden:** [Explicitly forbidden directions or `None`]

## Cross-Cutting Constraints

* **Extension Model:** [Approved extension points and rules, or `None`]
* **Error / Recovery:** [Failure domains and recovery rules]
* **Concurrency:** [Execution model and threading rules, if prescribed]
* **Security / Integrity:** [Boundaries and trust domains]
* **Observability:** [Logging, metrics, and diagnostics expectations, if prescribed]
* **Assumptions:** [Build / Runtime assumptions]

## Guardrails & Rejections

* **Implementation Guardrails:** [Strict approved technical constraints, or `None`]
* **Architecture Guardrails:** [Rules required to preserve approved architecture, or `None`]
* **Explicitly Rejected:** [Approach] - [Why rejected]
* **Foundational Open Questions:** [Unresolved architecture-shaping questions that materially affect the target design or first implementation phase, if any]
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
* **Must Not Own:** [Explicit approved exclusions, or `None`]

## Interfaces & Domain

* **Public Contract: <Name>:** <Purpose> | **Consumers:** [List] | **Rules:** [List]
* **Domain: <Concept>:** <Purpose> | **Properties:** [List] | **Lifecycle:** [Rules]

If no durable public contract is part of this subsystem's approved architecture, state
`Public Contracts: None`. Do not invent interfaces merely to populate this section.

## Data Flow & Persistence

* **State / Persistence:** [List state categories, where they live, and persistence/ownership rules]
* **Key Flow: <Name>:** <Trigger> -> <Step 1, 2, 3> -> <Output> (Failure: [Handling rule])
* **Key Flow: <Name>:** <Trigger> -> <Step 1, 2, 3> -> <Output> (Failure: [Handling rule])

## Dependencies

* **Allowed Depends On:** [Approved dependency] - <Why>
* **Forbidden Depends On:** [Explicitly forbidden dependency] - <Why>

If dependency direction is not architecturally prescribed, state that rather than inventing a rule.

## Cross-Cutting Rules

* **Lifecycle:** [Startup/Runtime/Shutdown behavior]
* **Concurrency:** [Threading, locking, and execution rules, if prescribed]
* **Error/Recovery:** [Subsystem-specific fault tolerance]
* **Extension/Config:** [Approved extension points and configuration model, or `None`]
* **Security/Integrity:** [Trust boundaries and validation]
* **Observability:** [Logging, metrics, and diagnostics expectations, if prescribed]
* **Assumptions:** [Build or runtime assumptions]

## Guardrails

* **Implementation Guardrails:** [Approved strict rules preventing architectural regression, or `None`]
* **Architecture Guardrails:** [Rules preserving explicitly approved subsystem responsibility and contracts, or `None`]
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

**Build Strategy:** <Short statement of execution strategy, sequencing logic, and how phases reduce risk>

## Roadmap

### Phase Summaries

1. **<Phase 1 Name>:** <Objective> |
   **Mode:** <To determine at activation / Single-pass / Two-pass contract-first> |
   **Status:** <Pending / Active / Awaiting Review / Blocked / Complete> |
   **Plan:** <`plan/plan_phase_<N>.md` or `None`> |
   **Plan Status:** <None / Draft / Ready for Review / Approved / Superseded>
2. **<Phase 2 Name>:** <Objective> |
   **Mode:** <To determine at activation / Single-pass / Two-pass contract-first> |
   **Status:** <Pending / Active / Awaiting Review / Blocked / Complete> |
   **Plan:** <`plan/plan_phase_<N>.md` or `None`> |
   **Plan Status:** <None / Draft / Ready for Review / Approved / Superseded>

## Active Phase Detail

*(Use ONLY if the active phase does not have a separate `plan/plan_phase_<N>.md` file. Otherwise
write: "See active phase plan file.")*

* **Goal:** <Concrete phase outcome>
* **Execution Readiness:** <Design required / Phase planning required / Awaiting human review / Ready to execute / Blocked / Complete>
* **Scope:** [Implementation areas this phase may touch, if known]
* **Approved Constraints:** [Relevant architectural or dependency constraints, or `None`]
* **Ordered Steps:**
    1. <Step>
    2. <Step>
* **Validation:** [List phase-level checks or review gates]
* **Done When:** [List completion conditions]

## Deferred & Completed

* **Deferred:** [List intentionally postponed roadmap items]
* **Completed:** [Phase Name] -> Unlocked: [What it enabled]

## Maintenance Rules

* Keep this file focused on the durable execution roadmap, not current-session handoff details.
* Current session status, exact next action, blockers, current pass state, and active dry-run baseline belong in `state.md`.
* Keep phase status, execution mode, phase-plan references, and phase-plan approval state consistent with `state.md`.
* When `state.md` records a phase-level or pass-level transition, verify whether this roadmap also requires a corresponding update.
* Add a separate `plan/plan_phase_<N>.md` when a phase requires detailed sequencing, a durable contract review gate,
  multiple meaningful review or validation gates, or enough execution detail that it would bloat this file.
* Do not create a phase plan merely to document ordinary implementation decomposition.
* When a `plan/plan_phase_<N>.md` file exists, treat it as the authoritative detailed execution plan for that phase.
  Do not partially duplicate phase-level sequencing here.
* If an active phase plan file exists but is incomplete, stale, or inconsistent with current approved
  project direction, update that phase plan rather than expanding `Active Phase Detail`.
* Use `Mode: To determine at activation` when execution mode should be resolved closer to implementation
  rather than guessed prematurely.
* A phase plan marked `Draft` or `Ready for Review` is not implementation authorization.
* A phase plan marked `Approved` has completed its planning gate. If no other blocker or contract gate remains,
  `state.md` should make the next executable step explicit and mark execution readiness accordingly.
* Compress completed phase detail aggressively once it no longer helps execution.
```

---

## Template: `plan/plan_phase_<N>.md`

```markdown
# AI Plan - Phase <N>: <Phase Name>

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**  
**Project:** <Project name> | **Parent:** `../plan.md`  
**Phase Status:** <Not started | Active | Awaiting Review | Blocked | Complete>  
**Plan Status:** <Draft | Ready for Review | Approved | Superseded>  
**Mode:** <Single-pass | Two-pass contract-first>

## Objective & Scope

**Objective:** <Concrete outcome this phase must produce>  
**Inputs:** [Requirements Section] | [Architecture Section] | [Prior Phase Output]  
**In Scope:** [List items]  
**Out of Scope / Do Not Do Yet:** [List items]  
**Expected Deliverables:** [List deliverables]

## Execution Constraints

* **Implementation Scope:** [Known modules/subsystems/packages/layers this phase may create or modify, or `Not prescribed`]
* **Approved Boundaries:** [Relevant architecture boundaries or `None`]
* **Public Contracts:** [APIs, schemas, protocols, persistent formats, extension points, or other durable contracts this phase establishes or changes, or `None`]
* **Human Review Focus:** [What the reviewer must inspect before the next gate, or `None`]

Do not invent internal seams, interfaces, abstraction layers, dependency rules, or module boundaries merely
to populate this section.

## Ordered Work

*(If Single-Pass, delete Pass A and rename the implementation section to `### Implementation`. Do not use a Pass B label for single-pass work.)*

### Pass A: Contract (Review Gate)

Use Pass A only when this phase establishes or materially changes a contract that independently merits
human approval before implementation.

* **Step A1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step A2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

Pass A should produce:

* the reviewable contract, API shape, schema, protocol surface, extension contract, persistent format,
  or other durable design surface being established,
* relevant approved architecture constraints needed to interpret that contract, and
* tests, examples, signatures, schemas, or other review artifacts only when they materially clarify
  intended behavior and fit project conventions.

A Bonsai contract gate does not itself require Java interfaces, builders, adapters, dependency
injection, abstraction layers, or similar indirection.

**Stop here for Human Review before Pass B.**

### Pass B: Implementation

* **Step 1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step 2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

## Validation & Done Criteria

* **Validation Strategy:** [Project-appropriate tests, builds, manual checks, examples, or other verification]
* **Architecture Validation:** [Checks required to confirm approved architecture or contracts were preserved, or `None`]
* **Definition of Done:** [List completion conditions. For two-pass, include faithful implementation of the approved contract]

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
    * phase-plan approval state,
    * current pass,
    * exact next step,
    * review-gate status,
    * blockers,
    * phase completion state.
* Preserve approved project architecture and contracts during execution.
* Do not introduce interfaces, abstraction layers, adapters, builders, dependency constraints, or other
  structures merely to satisfy Bonsai workflow.
* Implementation style and test style follow project conventions, approved project memory,
  developer context, and applicable external skills.
* If required behavior conflicts with approved architecture or an approved contract, stop and require
  phase-plan correction, final-truth clarification, or final-truth revision before continuing.
* When a pass boundary, review gate, blocker state, phase status, or plan approval state changes,
  verify whether `state.md` and `plan.md` require corresponding updates.
* If this phase plan becomes incomplete, stale, or inconsistent with current approved project direction,
  correct it before substantive phase execution continues.
* Set `Plan Status: Ready for Review` when drafting is complete and human approval is required.
* Set `Plan Status: Approved` only after explicit human approval.
* Compress completed phase detail when it no longer helps execution, while preserving enough summary
  to explain the outcome and what it unlocked.
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
**Phase Plan Status:** <None / Draft / Ready for Review / Approved / Superseded>  
**Current Phase Pass:** <Not applicable | Phase Planning | Phase Plan Review | Single-pass Implementation | Pass A (Contract) | Contract Review | Pass B (Implementation) | Awaiting Review>  
**Phase Execution Mode:** <Single-pass | Two-pass contract-first | To determine at activation>  
**Execution Readiness:** <Design required | Phase planning required | Awaiting human review | Ready to execute | Blocked | Complete>  
**Current Objective:** <Single concrete objective>

* **Current Snapshot:** <1-2 lines describing only the present implementation reality needed to resume correctly>
* **Active Files:** [List 3-7 resume-critical files only; not every recently touched file]
* **Blockers / Risks:** [Active blockers, uncertainties, or review dependencies only]

**Exact Next Step:** <Action>  
**Success Condition:** <What must be true when the next step is complete>

### Approved Dry-Run Baseline

<`None`, or a compact active baseline containing only the approved basis, intended result, expected touch points, anticipated final-truth impact, and planned checks. Remove it when the work completes, is abandoned, or is redirected.>

## Maintenance Rules

* `state.md` describes current resume state, not session history.
* Keep only information needed for the next agent to resume the project correctly.
* Before every update, remove information that no longer affects resumption.
* Replace stale facts with current truth rather than appending newer versions.
* Remove completed next steps, resolved blockers, obsolete observations, superseded decisions,
  expired dry-run baselines, transient commentary, and files no longer relevant to immediate resumption.
* A fact should remain only if removing it could materially change what the next implementation session does.
* Keep this file short enough to read at every implementation-session startup.
* Use `Current Snapshot` for present reality only. Do not turn it into a recent-work log.
* Use `Active Files` only for files the next implementation session is likely to resume in immediately.
* Do not use `Active Files` as a touched-files list, change log, or broad working-set inventory.
* Do not duplicate roadmap summaries from `plan.md`.
* Do not duplicate detailed phase sequencing from `plan/plan_phase_<N>.md`.
* Keep phase execution mode, phase-plan approval state, and execution readiness consistent with
  `plan.md` and any active phase plan.
* A phase plan in `Draft` or `Ready for Review` state cannot correspond to `Execution Readiness: Ready to execute`
  unless the exact next executable work is independent of that plan.
* When recording a phase-level or pass-level transition, verify whether `plan.md` or the active phase plan
  also requires a corresponding update.
* Update after each meaningful execution step, review gate, blocker change, phase transition, pass transition,
  active phase plan change, execution mode change, or execution-readiness change.
```
