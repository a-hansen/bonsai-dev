# Phase Execution Skill

## Purpose

Govern phase planning, execution-mode selection, phase-plan lifecycle, contract-first two-pass work, and the
review gates between them.

This skill is subordinate to `prompts/implementation.md`. It manages execution memory and gates; it does not
create product architecture or implementation abstractions.

## When to Load

Load this skill when:

- a new project's Phase 1 plan must be drafted or corrected;
- a later phase genuinely needs detailed planning;
- phase execution mode is unresolved;
- an exact step is governed by an active phase plan or approved phase contract;
- Pass A or contract review is active; or
- phase-plan, pass, approval, or roadmap state is inconsistent.

## Required Inputs

Read only the project material needed for the current decision:

- `agent_plan.md`;
- `agent_state.md`;
- the active `plan/agent_plan_phase_<N>.md`, when present or needed to establish the gate;
- relevant requirements, architecture, and other approved final truth;
- the recorded exact next step; and
- `templates/plan_phase_template.md` only when drafting a new detailed phase plan.

Treat missing or conflicting required memory as a planning requirement, review state, or blocker. Do not rebuild
project truth from chat history, unrelated project files, maps, or context.

## Execution Terminology and Readiness

Use `Single-pass Implementation` for ordinary implementation. Reserve `Pass A (Contract)`, `Contract Review`, and
`Pass B (Implementation)` for an actual two-pass contract-first phase. Never call single-pass work Pass B.

Use the readiness vocabulary defined by the implementation kernel:

- incomplete required planning: `Phase planning required`;
- a drafted plan or contract awaiting approval: `Awaiting human review`;
- an approved exact step with no remaining gate: `Ready to execute`;
- a concrete conflict or impediment: `Blocked`.

The existence of a plan is not execution authorization.

## Select the Execution Mode

Use **Single-pass** by default when the phase can be implemented and reviewed without separately approving a
durable contract.

Use **Two-pass contract-first** only when the phase establishes or materially changes a durable surface that
independently merits human approval before implementation proceeds beneath it. Examples include an externally
consumed API, schema, persistent format, protocol, extension contract, or durable integration surface.

Do not select two-pass merely because work is large, complex, spans files, creates classes, changes internal
organization, needs tests, or would benefit from ordinary code review. An already approved contract does not need
a duplicate Bonsai contract gate unless the phase establishes or materially changes another review-worthy seam.

When mode is unresolved, report the recommendation and a one-sentence rationale at the current gate. Do not
resolve it or change memory until the human authorizes planning.

## Respect Approved Boundaries

When activating a phase, drafting or correcting its plan, or entering Pass A, record only boundaries supported by
approved project truth or necessary to interpret an approved durable contract. Consider, when relevant:

- implementation areas in and out of scope;
- durable APIs, schemas, protocols, formats, extension points, and integrations;
- explicitly prescribed dependency direction; and
- explicitly forbidden coupling.

Do not invent modules, interfaces, layers, adapters, builders, injection seams, dependency rules, or other
structure to make planning or a contract gate appear formal. A concrete type, native schema, or other direct
artifact can be the correct contract surface.

If a required approved boundary is unclear, classify the issue as phase-plan correction, final-truth
clarification, final-truth revision, or an out-of-scope observation. Delegate clarification and revision to
`skills/final_truth_update.md` before proceeding.

## Create and Maintain Phase Plans

Detailed phase plans are agent-owned execution memory, not product or architecture truth. Create
`plan/agent_plan_phase_<N>.md` from `templates/plan_phase_template.md`; instantiate every field and remove all
template instructions, placeholders, and inapplicable mode structure.

### Initial Phase

Every newly synthesized project must have a reviewed Phase 1 plan before substantive Phase 1 implementation.
Draft it from repository reality, approved final truth, and the roadmap. Set its plan status to `Ready for Review`,
reconcile `agent_plan.md` and `agent_state.md`, set readiness to `Awaiting human review`, and stop at the Phase Plan
Approval Gate.

This mandatory initial gate reviews execution intent. It does not by itself justify two-pass execution.

### Later Phases

Create a later detailed plan only when it materially improves execution and resumption, such as when the phase:

- needs ordered sequencing too detailed for `agent_plan.md`;
- uses two-pass contract-first execution;
- has multiple meaningful review or validation gates; or
- has approved constraints that must remain visible across several bounded steps.

Do not create one merely because the phase touches multiple files or is internally complex. When no detailed plan
is warranted, keep roadmap/state concise and record the approved exact step directly.

### Missing, Stale, or Inconsistent Plans

- A missing Phase 1 plan makes drafting it the exact next step.
- A missing later plan that is genuinely required makes drafting it the exact next step.
- An incomplete, stale, or inconsistent active plan must be corrected before substantive execution.
- An unresolved mode must be resolved before the phase becomes executable.

After drafting or materially correcting a required plan, reconcile roadmap and state, then stop for approval. Do
not duplicate detailed sequencing into `agent_plan.md`.

### Required Plan Content

Include only applicable execution detail:

- objective, bounded scope, and explicit out-of-scope work;
- approved boundaries and durable contracts;
- ordered work and meaningful gates;
- validation strategy and definition of done;
- human review focus, risks, dependencies, and active questions.

Use `None` or `Not prescribed` where appropriate. Do not invent content to fill the template. A single-pass plan
must contain only its implementation structure; a two-pass plan must contain Pass A, its review stop, and Pass B.

For a code contract, plan Pass A around the smallest useful native source surface plus tests or examples that
materially clarify behavior. Require the source and contract-test surface to compile before review. Behavioral
tests may intentionally fail or remain disabled until Pass B when the plan states that clearly.

## Phase Plan Approval Gate

Before presenting the gate, report:

- final-truth impact: `None`, `Clarification`, or `Revision`;
- affected final-truth documents when impact is not `None`;
- any required final-truth action;
- material approved-boundary impact; and
- human review focus.

An unresolved revision delegates to `skills/final_truth_update.md` and cannot offer implementation as a bypass.
Otherwise load `skills/menu.md` and supply these primary choices:

1. Approve the named phase plan.
2. Request revisions to the phase plan.
3. Discuss concerns before deciding.
4. Return to roadmap-level planning.

Stop for the human choice. Approval authorizes the plan, not immediate execution. On approval:

1. set the plan status to `Approved`;
2. reconcile `agent_plan.md`, `agent_state.md`, and the phase plan;
3. record the concrete exact next step, pass, and `Ready to execute` state; and
4. stop at the Continuation Gate before beginning the newly approved work.

## Pass A and Contract Review

Use Pass A only for an approved two-pass phase. Produce the smallest useful native review surface and preserve the
approved boundaries needed to interpret it. Tests, examples, signatures, schemas, and message examples belong in
Pass A only when they materially clarify the contract.

For a code contract:

- source-level APIs or structural skeletons may establish placement, names, types, signatures, visibility,
  failure surfaces, and necessary structural relationships;
- concrete classes with intentionally unimplemented methods are valid;
- substantive behavior remains for Pass B;
- contract source and contract-test source must compile before review;
- behavior tests may fail or be disabled when implementation is intentionally absent, but their status must be
  reported and their expectations must not be weakened to make Pass A green; and
- prose is primary only when the important semantics cannot be reviewed clearly in native artifacts.

Classify actual final-truth impact, reconcile execution memory, and stop at `Contract Review`. An unresolved
revision first delegates to `skills/final_truth_update.md`. Otherwise load `skills/menu.md` and supply:

1. Approve the contract.
2. Request revisions to the contract.
3. Discuss concerns before deciding.
4. Return to the phase plan.

After approval, record it, set the pass to `Pass B (Implementation)`, compute the concrete exact next step, set
readiness appropriately, and stop at the Continuation Gate. Do not begin Pass B in the same authorization step.

## Implementation Discipline

During single-pass implementation or Pass B:

- execute only the approved exact step and scope;
- preserve approved final truth, contracts, and applicable boundaries;
- follow project conventions and only the source guidance and context relevant to the work; and
- stop if implementation requires an unapproved contract or final-truth change.

For an approved code contract, Pass A tests preserve behavior rather than immutable test source. Pass B may change
fixtures, fakes, helpers, imports, construction, and other test plumbing without renewed contract review when the
approved scenarios, inputs, observable outcomes, and failure expectations remain materially unchanged. Stop for
contract review before weakening, removing, contradicting, or materially changing an approved expectation.

Before Pass B completes, enable every approved expectation and make all approved contract tests pass.

## Phase Completion Transition

Completing a phase closes that phase only. It does not by itself complete the current body of work.

When a phase reaches its approved definition of done:

1. mark that phase complete in its applicable phase plan and roadmap truth;
2. inspect the approved roadmap for pending, active, or otherwise unfinished phases that still belong to the
   current body of work;
3. if unfinished roadmap work remains, identify and activate the next applicable phase and derive that phase's
   actual gate:
   - use `Phase planning required` when a required detailed plan must still be drafted or corrected;
   - use `Awaiting human review` when a required plan, contract, or other review artifact already awaits approval;
   - use `Blocked` when a concrete inconsistency or impediment prevents safe activation or planning;
   - use `Ready to execute` only when the next phase has one authorized exact next step and no required gate
     remains;
4. record the next phase, applicable plan/pass state, readiness, and exact next step consistently across
   `agent_plan.md`, `agent_state.md`, and the applicable phase plan; and
5. only when no unfinished approved roadmap work remains in the current body of work may Bonsai clear the current
   phase as part of body-of-work completion and set `Execution Readiness: Complete`.

Activating the next phase records lifecycle truth; it does not authorize substantive execution. The applicable
planning, review, continuation, or blocker gate still controls what may happen next.

Do not persist `Current Phase: None` as a completion shortcut while an identifiable unfinished roadmap phase
remains. If roadmap state is too inconsistent to identify the next applicable phase safely, preserve the conflict
as `Blocked` rather than treating the body of work as complete.

## Execution-Memory Reconciliation

Keep `agent_plan.md`, `agent_state.md`, and the active phase plan consistent whenever phase, mode, plan status,
pass, review state, blocker state, readiness, or exact-next-step truth changes. Remove superseded state instead of
appending history. Correct stale plans before further implementation and compress completed phase detail when it
no longer helps resumption.

When a phase completes, apply the Phase Completion Transition before deriving readiness. A completed phase with
later unfinished roadmap work must leave the body of work in a non-`Complete` state.

At an exact-step or gate completion boundary, delegate to `skills/handoff.md` before claiming completion.

## Continuation Gate

When an approval leaves an executable next step, load `skills/menu.md` and present current-session and
fresh-session continuation as peers:

1. Continue with the concrete next step in the current session.
2. Continue with the concrete next step in a fresh session.
3. Review or change the next step.
4. Do not continue right now.

Record all resume-critical truth before presenting this gate. If fresh-session continuation is selected, starting
the session remains a human action. Provide:

```text
Read .bonsai/start.md and follow its instructions.
```

Add `Active project: <project>` only when startup identity rules would not otherwise resolve the same project.
Then stop. A fresh session never bypasses planning, review, final-truth, or blocker gates.

## Stop Conditions

Stop for human direction when:

- mode is unresolved and planning has not been authorized;
- a required plan is missing, stale, or inconsistent;
- a drafted or materially corrected plan awaits approval;
- a required approved boundary or durable contract is unclear;
- Pass A has produced its review surface;
- work requires final-truth clarification or revision;
- work would weaken or materially change an approved contract; or
- the requested action exceeds the approved plan, contract, or exact next step.

