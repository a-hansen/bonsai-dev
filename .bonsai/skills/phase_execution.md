# Phase Execution Skill

## Purpose

Govern phase planning, execution-mode selection, phase-plan lifecycle, contract-first two-pass work, execution memory, and related gates.

Subordinate to `prompts/implementation.md`. Manages execution memory/gates only; does not create product architecture or implementation abstractions.

## Load When

- Phase 1 planning must be drafted/corrected.
- A later phase becomes current and needs planning.
- Execution mode is unresolved.
- An exact step is governed by an active phase plan or approved phase contract.
- Pass A or Contract Review is active.
- Phase-plan, pass, approval, or roadmap state is inconsistent.

## Inputs

Read only what the current decision needs:

- `agent_plan.md`;
- `agent_state.md`;
- active `plan/agent_plan_phase_<N>.md`, when present or needed to establish the gate;
- relevant requirements, architecture, and other approved final truth;
- recorded exact next step;
- `templates/plan_phase_template.md` only when drafting a detailed phase plan.

Missing/conflicting required memory creates a planning requirement, review state, or blocker. Never reconstruct project truth from chat history, unrelated files, maps, or context.

## Execution Semantics

### Mode/pass terms

- Ordinary implementation: `Single-pass Implementation`.
- Two-pass only: `Pass A (Contract)` -> `Contract Review` -> `Pass B (Implementation)`.
- Never call single-pass work Pass B.
- Single-pass has no user-facing pass designation; omit pass fields/labels.

### Readiness

| Condition | Value |
|---|---|
| Required planning incomplete | `Phase planning required` |
| Drafted plan/contract awaiting approval | `Awaiting human review` |
| Approved exact step, no remaining gate | `Ready to execute` |
| Concrete conflict/impediment | `Blocked` |

A plan's existence is not execution authorization.

### Authorization rule

Planning, plan, lightweight-basis, or contract approval authorizes only that artifact/basis. It never starts newly authorized work in the same authorization step. Persist resulting state and stop at the required next gate, normally the Continuation Gate.

Roadmap text, phase titles, or literal next-step commands in agent-owned roadmap/planning memory never substitute for required phase planning or approval.

## Execution Mode

Default **Single-pass** when implementation/review does not need separate approval of a durable contract.

Use **Two-pass contract-first** only when the phase establishes or materially changes a durable surface that independently merits approval before implementation beneath it, e.g. an externally consumed API, schema, persistent format, protocol, extension contract, or durable integration surface.

Do not choose two-pass merely for size, complexity, multiple files, new classes, internal reorganization, tests, or ordinary code review. Do not duplicate a Bonsai contract gate for an already-approved contract unless another review-worthy seam is established/materially changed.

If mode is unresolved, report the recommendation plus one-sentence rationale at the current gate. Do not resolve mode or change memory until the human authorizes planning.

## Approved Boundaries

When activating a phase, drafting/correcting its plan, or entering Pass A, record only boundaries supported by approved project truth or needed to interpret an approved durable contract. As applicable:

- implementation scope/out-of-scope;
- durable APIs, schemas, protocols, formats, extension points, integrations;
- prescribed dependency direction;
- forbidden coupling.

Do not invent modules, interfaces, layers, adapters, builders, injection seams, dependency rules, or similar structure to formalize planning/contract review. A concrete type, native schema, or direct artifact may be the correct contract surface.

If a required approved boundary is unclear, classify it as phase-plan correction, final-truth clarification, final-truth revision, or out-of-scope observation. Delegate clarification/revision to `skills/final_truth_update.md` before proceeding.

## Phase Planning

Every phase needs an approved execution basis before substantive execution.

- **Phase 1:** always detailed plan.
- **New later phase:** normally `Phase planning required` unless an applicable approved detailed plan already exists.
- Later-phase planning first decides detailed vs lightweight basis.
- Lightweight basis contains objective, execution mode, concrete exact next step, validation/success condition, and approved constraints needed for safe execution. It requires human approval before `Ready to execute`; do not create a phase-plan file solely for lightweight planning.

Detailed phase plans are agent-owned execution memory, not product/architecture truth. Create `plan/agent_plan_phase_<N>.md` from `templates/plan_phase_template.md`; instantiate all fields and remove instructions, placeholders, and inapplicable mode structure.

### Phase 1 procedure

For a newly synthesized project, before substantive Phase 1 work:

1. Draft from repository reality, approved final truth, and roadmap.
2. Set plan status `Ready for Review`.
3. Reconcile roadmap/state.
4. Set `Awaiting human review`.
5. Stop at Phase Plan Approval Gate.

This gate reviews execution intent; it does not itself justify two-pass execution.

### Later-phase plan choice

Create a detailed later plan only when it materially improves execution/resumption, such as:

- sequencing is too detailed for `agent_plan.md`;
- two-pass contract-first is used;
- multiple meaningful review/validation gates exist;
- approved constraints must remain visible across several bounded steps.

Multiple files or internal complexity alone are insufficient. If no detailed plan is warranted, use the Lightweight Phase Planning Gate. Roadmap-level design approval does not pre-approve the later-phase execution basis.

### Missing/stale/inconsistent planning

- Missing Phase 1 plan -> drafting it is the exact next step.
- Newly current later phase without applicable approved detailed plan -> phase planning is the exact next step.
- Planning decides detailed plan required -> drafting it becomes the exact next step.
- Incomplete/stale/inconsistent active plan -> correct before substantive execution.
- Unresolved mode or unapproved lightweight basis -> resolve before execution.

After drafting/materially correcting a required detailed plan, reconcile roadmap/state and stop for approval. Do not duplicate detailed sequencing into `agent_plan.md`.

### Detailed plan content

Include only applicable:

- objective, bounded scope, explicit out-of-scope;
- approved boundaries/durable contracts;
- ordered work/meaningful gates;
- validation strategy/definition of done;
- human review focus, risks, dependencies, active questions.

Use `None`/`Not prescribed` where appropriate; never invent template content.

- Single-pass plan: implementation structure only.
- Two-pass plan: Pass A, review stop, Pass B.
- Code-contract Pass A: smallest useful native source surface plus materially clarifying tests/examples. Contract source and contract-test source must compile before review. Behavioral tests may intentionally fail/remain disabled until Pass B only when the plan says so explicitly.

## Lightweight Phase Planning Gate

When no detailed later-phase plan is warranted, report the proposed lightweight basis and load `skills/menu.md`:

1. Approve the named phase execution basis.
2. Request revisions.
3. Discuss concerns.
4. Require a detailed phase plan instead.

Stop for the human choice.

On approval: reconcile `agent_plan.md`/`agent_state.md`; persist the approved lightweight basis; record concrete exact next step and `Ready to execute`; omit pass designation for single-pass; stop at Continuation Gate.

## Phase Plan Approval Gate

Before the gate report:

- final-truth impact: `None`, `Clarification`, or `Revision`;
- affected final-truth documents if not `None`;
- required final-truth action;
- material approved-boundary impact;
- human review focus.

Unresolved revision -> `skills/final_truth_update.md`; implementation is not a bypass. Otherwise load `skills/menu.md`:

1. Approve the named phase plan.
2. Request revisions.
3. Discuss concerns.
4. Return to roadmap-level planning.

Stop for the human choice.

On approval: set plan `Approved`; reconcile `agent_plan.md`, `agent_state.md`, phase plan; record concrete exact next step and `Ready to execute`; record pass only for actual two-pass work; stop at Continuation Gate.

## Pass A and Contract Review

Use Pass A only for an approved two-pass phase. Produce the smallest useful native review surface while preserving approved boundaries needed to interpret it. Include tests/examples/signatures/schemas/message examples only when materially clarifying.

For code contracts:

- APIs/skeletons may establish placement, names, types, signatures, visibility, failure surfaces, required structural relationships;
- concrete classes may contain intentionally unimplemented methods;
- substantive behavior belongs to Pass B;
- contract source and contract-test source must compile before review;
- behavior tests may fail/be disabled while behavior is intentionally absent, but report status and never weaken expectations to make Pass A green;
- prose is primary only when native artifacts cannot clearly express important semantics.

After Pass A: classify actual final-truth impact, reconcile execution memory, stop at `Contract Review`. Unresolved revision first delegates to `skills/final_truth_update.md`; otherwise load `skills/menu.md`:

1. Approve the contract.
2. Request revisions.
3. Discuss concerns.
4. Return to the phase plan.

Stop for the human choice.

On approval: record approval; set `Pass B (Implementation)`; compute concrete exact next step; set readiness appropriately; stop at Continuation Gate. Do not begin Pass B in the approval step.

## Implementation Discipline

During Single-pass Implementation or Pass B:

- execute only approved exact step/scope;
- apply relevant operational context before environment/toolchain-sensitive command syntax; literal commands in agent-owned memory express intent but do not override applicable invocation-context rules;
- preserve approved final truth, contracts, boundaries;
- follow project conventions and only relevant source guidance/context;
- stop if an unapproved contract or final-truth change becomes necessary.

For an approved code contract, Pass A tests preserve behavior, not immutable test source. Pass B may change fixtures, fakes, helpers, imports, construction, and other plumbing without renewed review only while approved scenarios, inputs, observable outcomes, and failure expectations remain materially unchanged. Stop for contract review before weakening, removing, contradicting, or materially changing an approved expectation.

Before Pass B completes, enable every approved expectation and make all approved contract tests pass.

## Phase Completion Transition

Phase completion closes that phase only, not necessarily the current body of work.

When a phase reaches its approved definition of done:

1. Mark it complete in applicable phase plan and roadmap truth.
2. Inspect approved roadmap for unfinished phases in the current body of work.
3. If work remains, identify/activate the next phase and derive its gate:
   - no applicable approved detailed plan -> `Phase planning required`; planning chooses detailed vs lightweight;
   - required plan/contract/review artifact awaits approval -> `Awaiting human review`;
   - concrete inconsistency/impediment -> `Blocked`;
   - applicable approved detailed plan already supplies one authorized exact next step with no gate -> `Ready to execute`.
4. Reconcile next phase, applicable plan/pass state, readiness, and exact next step across `agent_plan.md`, `agent_state.md`, and applicable phase plan.
5. Only when no unfinished approved roadmap work remains may body-of-work completion clear current phase and set `Execution Readiness: Complete`.

Activation records lifecycle truth, not substantive-execution authorization. After establishing the next phase/action:

- agent-performable exact action with no independent human-decision gate -> Continuation Gate, including phase planning while `Phase planning required`;
- approval/review/final-truth/design/blocker action -> corresponding specialized gate.

Planning entered through continuation still stops at its resulting approval gate.

Never persist `Current Phase: None` while an identifiable unfinished roadmap phase remains. If roadmap inconsistency prevents safe next-phase identification, preserve `Blocked`, not complete.

## Execution-Memory Reconciliation

Keep `agent_plan.md`, `agent_state.md`, and active phase plan consistent whenever phase, mode, plan status, pass, review state, blocker state, readiness, or exact-next-step truth changes.

- Remove superseded state; do not append history.
- Correct stale plans before further implementation.
- Compress completed-phase detail when no longer useful for resumption.
- On phase completion, apply Phase Completion Transition before deriving readiness.
- Later unfinished roadmap work means body-of-work state is not `Complete`.
- At exact-step or gate completion boundaries, delegate to `skills/handoff.md` before claiming completion.

## Continuation Gate

Use when exactly one concrete agent-performable next action exists and no independent human-decision gate is active, including an approved executable step or phase-planning action established after a phase boundary.

Record all resume-critical truth, then load `skills/menu.md`. Normally present:

1. Continue the concrete next step in this session.
2. Continue it in a fresh session and automatically execute it.
3. Review/change the next step.
4. Exit for now.

If this session itself entered through fresh-session continuation and no substantive work has occurred since entry, omit choice 2 at the first resulting Continuation Gate unless explicitly requested. Keep that fact session-local.

If fresh-session continuation is selected, starting the session remains a human action. Always preserve the active project identity in the pointer. Provide:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate. Active project: <project>.
```

Do not discard known project identity merely because startup could deterministically infer the same project.

This startup request authorizes exactly one next action after canonical state reconstruction. It may authorize planning when planning is that action; it never authorizes a subsequent action or bypasses required planning approval, review, final-truth, contract, design, or blocker gates. Then stop.

## Stop Conditions

Stop for human direction when:

- mode is unresolved and planning has not been authorized;
- a required plan is missing, stale, or inconsistent;
- a drafted/materially corrected plan awaits approval;
- a required approved boundary or durable contract is unclear;
- Pass A has produced its review surface;
- final-truth clarification/revision is required;
- work would weaken/materially change an approved contract;
- requested action exceeds approved plan, contract, or exact next step.
