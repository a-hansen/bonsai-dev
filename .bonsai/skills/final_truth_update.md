# Final-Truth Update Skill

## Purpose

Keep Bonsai's human-owned project truth aligned with the product and target architecture being built.

This skill handles cases where proposed, discovered, or completed work clarifies or changes approved
requirements, architecture, or another explicitly designated human-owned final-truth document.

Normal updates to `plan.md`, phase plans, and `state.md` are execution-memory maintenance and do not by
themselves constitute a final-truth clarification or revision.

This skill is often subordinate to another workflow gate. Completing a clarification or revision does not
silently end the gate that invoked it.

## Required Inputs

* Current approved human-owned project truth.
* The approved execution basis for the work.
* The proposed, completed, or discovered change.
* The classified final-truth impact:
    * `None`
    * `Clarification`
    * `Revision`
* The invoking workflow or gate, when this skill was entered from another gate.

## Human-Owned Final-Truth Documents

Human-owned final truth describes the intended product and target system after successful implementation.

Common examples:

* `requirements.md`
* `architecture.md`
* `requirements/requirements_<AREA>.md`
* `architecture/architecture_<SUBSYSTEM>.md`
* project-specific design or contract documents explicitly designated by the human as durable project truth

The following are not human-owned final truth:

* `plan.md`
* `plan/plan_phase_<N>.md`
* `state.md`
* `icebox.md`
* framework instructions and skills
* developer-local context
* repository maps

Those files may need maintenance as a consequence of an approved clarification or revision, but that
maintenance is not itself the final-truth change.

## Impact Classification

### None

Use `None` when approved human-owned final truth already covers the work.

The agent may proceed without proposing a final-truth update.

Normal execution-memory maintenance may still be required.

### Clarification

Use `Clarification` when intended behavior and architecture are unchanged, but an approved human-owned
final-truth document should be stated more precisely.

Clarifications may include:

* making an implicit approved decision explicit,
* tightening genuinely ambiguous wording,
* adding a missing constraint already implied by approved direction, or
* correcting stale wording that no longer matches other approved human-owned project truth.

A clarification must not be used to disguise a behavioral or architectural change.

### Revision

Use `Revision` when the work changes intended behavior, architecture, constraints, product boundaries,
system boundaries, or another rebuild-relevant human-owned design decision.

Revisions require approval before substantive implementation continues.

The agent must not treat implementation as complete when unresolved revision-level human-owned final-truth
changes remain.

## Procedure

1. Identify the approved execution basis for the work.
2. Identify the invoking workflow or gate, when one exists.
3. Compare the proposed or completed work against current human-owned final truth.
4. Classify the impact as `None`, `Clarification`, or `Revision`.
5. Identify the affected human-owned final-truth documents.
6. For `None`, report that no final-truth update is required.
7. For `Clarification`, propose the exact human-owned document updates unless the human has already explicitly
   authorized them.
8. For `Revision`, stop substantive implementation and present the required human-owned final-truth update for
   approval.
9. After approved human-owned updates are made, reconcile execution memory as needed:
    * `plan.md`
    * active phase plan
    * `state.md`
10. Recompute the exact next step and execution readiness from the reconciled current truth.
11. If this skill was invoked from another gate, return to that gate with the refreshed next step and readiness.
12. If the approved update materially changes the workflow or creates a new required gate, present that new gate
    instead of returning to the prior gate.

Do not stop merely because the final-truth files were successfully updated. A completed subordinate
final-truth action must hand control back to its invoking workflow unless a new required gate supersedes it.

## Approval Behavior

For unresolved `Clarification`, present:

1. Apply the clarification.
2. Revise the clarification.
3. Discuss before deciding.
4. Leave human-owned final truth unchanged for now.

For unresolved `Revision`, present:

1. Apply the proposed final-truth revision and continue only after approval.
2. Revise the proposed final-truth update.
3. Discuss before deciding.
4. Return to the prior planning or execution gate.

Do not offer substantive implementation while a required `Revision` remains unresolved.

When the human approves and the update is applied, use the Return-to-Invoking-Gate rule below rather than
ending the workflow at the final-truth completion report.

## Return-to-Invoking-Gate Rule

Final-truth handling may be invoked from, for example:

* a startup gate,
* a handoff,
* out-of-scope observation review,
* a phase-plan review,
* a contract review,
* a material-deviation gate, or
* another explicit correction or triage workflow.

After the final-truth action completes:

1. Reconcile current execution memory.
2. Recompute the exact next step.
3. Recompute execution readiness.
4. Re-evaluate whether any required gate now exists.
5. Return to the invoking gate with refreshed concrete choices if no new gate supersedes it.

Example: if a handoff observation reveals stale wording in `requirements.md` and `architecture.md`, and the
human explicitly chooses to correct those files immediately as a `Clarification`, apply the approved correction,
reconcile state, recompute the next step and readiness, then return to the handoff menu. Do not stop simply because
the clarification was completed.

## Execution-Memory Consequences

An approved clarification or revision may require corresponding execution-memory updates.

Examples:

* roadmap sequencing may change in `plan.md`,
* an active phase plan may need correction,
* execution readiness may change in `state.md`,
* the exact next step may change, or
* an approved contract may become stale.

These updates maintain workflow consistency. They do not expand the set of human-owned final-truth documents.

## Forbidden Changes

* Do not silently change requirements or architecture.
* Do not bury revision-level product or architecture changes in `state.md`, `plan.md`, or a phase plan.
* Do not treat implementation behavior as approved human-owned project truth until the required final-truth
  documents are updated and approved.
* Do not treat an agent-maintained phase plan as product or architecture authority.
* Do not use developer-local preferences as project truth.
* Do not update framework skills as a substitute for updating project memory.
* Do not let completion of this subordinate skill silently discard the parent workflow gate.

## Validation

Before completing this skill, verify:

* The impact classification is stated.
* Affected human-owned final-truth documents are identified or explicitly listed as `None`.
* Required approvals are clear.
* Execution-memory consequences have been reconciled when the update was applied.
* `state.md` reflects the current exact next step and execution readiness after reconciliation.
* The invoking gate is known when this skill was entered from another workflow.
* The workflow returns to the invoking gate unless a new required gate supersedes it.

## Stop Conditions

Stop at this skill's own human gate when:

* a revision-level final-truth update needs approval,
* the affected human-owned document is unclear,
* the proposed update would change project scope and has not been approved, or
* the human chooses to discuss or revise before approval.

After an approved final-truth action is completed, do not end the parent workflow. Return to the invoking gate
unless the reconciled state requires a different gate.
