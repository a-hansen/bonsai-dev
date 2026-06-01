# Final-Truth Update Skill

## Purpose

Keep Bonsai's approved project memory aligned with the product being built.

This skill handles cases where completed or proposed work affects final-truth documents such as requirements, architecture, roadmap, phase plans, or state.

## Required Inputs

- Current approved project memory.
- The approved basis for the work.
- The proposed, completed, or discovered change.
- The classified final-truth impact:
    - `None`
    - `Clarification`
    - `Revision`

## Final-Truth Documents

Final-truth documents include project memory that should describe the system as it is intended to exist after successful implementation.

Common examples:

- `requirements.md`
- `architecture.md`
- `plan.md`
- `plan/plan_phase_<N>.md`
- `state.md`
- project-specific design or contract documents, when approved as project truth

Framework instructions and skills are not project truth.

Developer-local context is not project truth.

## Impact Classification

### None

Use `None` when the approved final-truth documents already cover the work.

The agent may proceed without proposing project-memory changes.

### Clarification

Use `Clarification` when intended behavior is unchanged, but an approved final-truth document should be stated more precisely.

Clarifications may include:

- making an implicit approved decision explicit
- tightening ambiguous wording
- adding a missing constraint that is already implied by approved direction
- correcting stale wording that no longer matches approved project memory

Clarifications should be proposed clearly and may be applied when the user approves them or has explicitly authorized the update.

### Revision

Use `Revision` when the work changes intended behavior, architecture, constraints, project boundaries, roadmap meaning, or rebuild-relevant design.

Revisions require approval before substantive implementation continues.

The agent must not treat implementation as complete when unresolved revision-level final-truth changes remain.

## Procedure

1. Identify the approved basis for the work.

2. Compare the proposed or completed work against that basis.

3. Classify the final-truth impact as `None`, `Clarification`, or `Revision`.

4. Identify affected final-truth documents.

5. For `None`, report no final-truth update required.

6. For `Clarification`, propose the exact document updates unless the user has already authorized the update.

7. For `Revision`, stop substantive implementation and present the required final-truth update for approval.

8. After approved updates are made, update `state.md` so the next session starts from the revised project truth.

## Approval Behavior

For unresolved `Clarification`, present:

1. Apply the clarification.
2. Revise the clarification.
3. Discuss before deciding.
4. Leave final truth unchanged for now.

For unresolved `Revision`, present:

1. Apply the proposed final-truth revision and continue only after approval.
2. Revise the proposed final-truth update.
3. Discuss before deciding.
4. Return to the prior planning or execution gate.

Do not offer to proceed with substantive implementation while a required `Revision` remains unresolved.

## Forbidden Changes

- Do not silently change requirements or architecture.
- Do not bury revision-level changes in `state.md` only.
- Do not treat implementation behavior as approved project truth until final-truth documents are updated and approved.
- Do not use developer-local preferences as project truth.
- Do not update framework skills as a substitute for updating project memory.

## Validation

Before completing this skill, verify:

- The impact classification is stated.
- Affected documents are identified or explicitly listed as `None`.
- Required approvals are clear.
- `state.md` reflects the approved next step when the workflow changes.

## Stop Conditions

Stop when:

- A revision-level final-truth update needs approval.
- The affected document is unclear.
- The proposed update would change project scope.
- The user chooses to discuss or revise before approval.