# AI Design Prompt (Web Synthesis)

## Purpose

We have been brainstorming a project in this chat. Now, transition into the role of a strict
Technical Writer and Systems Architect. Your task is to synthesize our conversation into a clean,
durable project memory system optimized for future implementation by a local IDE-based AI agent.

## Output Protocol

Generate the foundational project documents as distinct Markdown code blocks so I can easily copy
and paste them into my local file system.

You must generate:

1. `requirements.md`
2. `architecture.md`
3. `plan.md`
4. `state.md`

Generate optional documents ONLY if our design explicitly demands them:

* `plan_phase_<N>.md`
  *(Only when the initial active phase has already been discussed in enough execution detail that a
  phase-level plan will materially improve the first implementation session. Otherwise, leave
  detailed phase planning to the implementation workflow when the phase becomes active.)*

    * **Two-Pass Contract-First Semantics:** When a generated phase plan uses two-pass
      contract-first execution, Pass A should normally produce both:

        * the reviewable API / structural contract, and
        * tests or usage examples that make the intended behavior concrete for human review.

  Pass A should end at a human review gate. Pass B should implement against the
  approved contract and tests.
* `architecture/architecture_<SUBSYSTEM>.md`
  *(If a subsystem has deep, isolated complexity that should not bloat the top-level architecture.)*
* `requirements/requirements_<AREA>.md`
  *(If a product area has deep, isolated requirement complexity that should not bloat the top-level requirements.)*

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

## Synthesis Rules

* **No Hallucinations:** Base the outputs strictly on our chat history. Do not invent features,
  requirements, constraints, or architectural decisions we did not discuss.
* **Identify Gaps:** If a section of a template cannot be filled using our chat, list it under
  `Open Questions` in the appropriate file.
* **Format:** Adhere strictly to the dense, pipe-delimited `[Meta]` templates provided. Do not add
  conversational filler outside the code blocks.
* **Plan Initialization:** In `plan.md`, define the initial roadmap, the first active phase, and
  whether that phase should use single-pass or two-pass execution.
* **Phase-Plan Restraint:** Do not generate `plan_phase_<N>.md` merely because a phase is active,
  complex in the abstract, or two-pass. Generate it only when our design discussion already contains
  enough execution-level sequencing, review gates, or validation detail to justify preserving a
  phase-level plan before implementation begins. Otherwise, leave the phase plan absent so the
  implementation agent can create it closer to execution when repository reality is available.
* **State Initialization:** In `state.md`, initialize:

    * The current phase
    * The active phase plan file, if one exists
    * The current phase pass
    * The exact first implementation step, expressed at the correct execution unit: use the full current pass through its next review gate for two-pass phases, or the first bounded implementation step for single-pass phases.
    * The success condition for that step
    * The recommended AI effort level
* **Two-Pass State Initialization:** When the first active phase uses two-pass
  contract-first execution, initialize `state.md` so that the exact first
  implementation step runs the full current pass through its next explicit
  human review gate, unless our design discussion explicitly requires a smaller
  stopping point.

  For an initial Pass A, this usually means:

    * define the reviewable API / contract shape,
    * create behavior-focused tests that demonstrate intended usage and edge cases,
    * stop for human review before Pass B implementation.

## Inputs

[USER WILL PASTE THE BLANK COMPRESSED TEMPLATES BELOW THIS LINE]
