# Step Completion Procedure

## Purpose

Close an approved exact next step, reconcile the result against its approved basis, update required Bonsai maintenance artifacts, and hand off the next step cleanly.

## When to Read

Read this file before declaring an exact next step complete or presenting a completion handoff.

This procedure is subordinate to `implementation_prompt.md`. Apply its final-truth reconciliation rules and maintenance discipline throughout.

## Completion Procedure

After completing the exact next step:

1. Verify the completed work against the approved basis:

    * Approved contract, phase plan, or recorded exact next step.
    * Approved dry-run baseline, when one exists.
    * Approved final-truth impact.

2. Classify the actual final-truth impact:

    * `None`: Approved final truth already covers the completed work.
    * `Clarification`: Intended behavior is unchanged, but a final-truth document should be stated more precisely.
    * `Revision`: Completed or required work changes intended behavior, constraints, architecture, or system boundaries.

3. Resolve final-truth handling:

    * If actual impact is `None`, report `None`.
    * If actual impact is `Clarification`, propose the affected document update unless it was completed under explicit human instruction.
    * If actual impact is `Revision`, do not treat revised work as complete until the affected final-truth documents are updated and approved.

4. Update required Bonsai maintenance artifacts according to `implementation_prompt.md`, including as applicable:

    * `plan.md`
    * `state.md`
    * Active `plan/plan_phase_<N>.md`
    * `icebox.md`
    * Shared maps

5. If work followed an approved dry run, compare actual results, checks, touch points, and final-truth impact against the approved execution baseline. Remove or replace stale active baseline content in `state.md` after completion or redirection.

6. Record the exact next step and recommend a clean session for it.

## Completion Summary

Output a compact completion summary containing:

* Completed step.
* Material changes.
* Checks/results.
* Relevant Bonsai artifact updates.
* Approved versus actual final-truth impact.
* Final-truth updates proposed or completed, or `None`.
* Dry-run baseline comparison, when applicable.
* Deviations or `None`.
* Icebox update, when `icebox.md` changed, including the kind of observation preserved without implying approval.
* Recorded exact next step.

Do not claim completion without reporting the checks actually performed and their results.

## Handoff Choices

Unless the recorded next step requires a named gate, present:

1. Terminate this session; continue in a clean session.
2. Proceed to the recorded next step in this session.
3. Show a dry run for the recorded next step in this session.
4. Discuss or correct the result or next step.

If the recorded next step requires a named gate, present that gate instead of immediate proceed choices.
