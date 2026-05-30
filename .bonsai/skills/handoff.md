# Handoff Skill

## Purpose

Close an approved exact next step, reconcile the result against its approved basis, update required Bonsai maintenance artifacts, and hand off the next step cleanly.

A handoff is not only a completion summary. It is the point where Bonsai preserves what changed, records the next exact step, and gives the user a clean way to continue in either the current session or a fresh session.

## Required Inputs

Before producing a handoff, inspect the relevant approved basis for the work:

* Approved contract, phase plan, or recorded exact next step.
* Approved dry-run baseline, when one exists.
* Approved final-truth impact, when one exists.
* Current `state.md`.
* Active `plan/plan_phase_<N>.md`, when applicable.
* Any project memory documents affected by the completed work.

## Handoff Procedure

After completing the exact next step:

1. Verify the completed work against the approved basis.

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

6. Record the exact next step in `state.md`.

7. Recommend a clean session unless there is a specific reason to continue in the current session.

8. If presenting a terminate-session option, include a ready-to-copy prompt for starting the next session.

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

### Changed Files Reporting

At completion, report files added or modified as part of the completed step. Do not enumerate unrelated pre-existing working-tree changes unless they affected execution or require human attention.

## Clean Session Prompt

When the handoff offers a clean-session option, provide a copyable prompt immediately after the choice.

The prompt must be specific enough that the next agent can restart without guessing. Include:

* The project path.
* The relevant Bonsai project memory path.
* The recorded exact next step.
* The skill or workflow the next session should use, when known.
* Any required gate, dry-run baseline, or approval state.
* A clear instruction to begin with the normal Bonsai startup/read-only pass.

Use this format:

```text
Start a new Bonsai implementation session for this repository.

Project path: <repo or project path>
Bonsai project memory: .bonsai/projects/<project>/

Begin with the normal Bonsai startup/read-only pass. Read the required project memory, report current state, and stop before making changes.

Recorded exact next step:
<exact next step from state.md>

Relevant skill/workflow:
<phase execution, dry run, handoff, repo mapping, or other applicable skill>

Approval/gate status:
<any phase, contract, dry-run, or final-truth approval status the next session needs>
```

If any field is unknown, write `Unknown` rather than inventing it.

Do not merely tell the user to start a clean session. Provide the prompt text so the user can copy it directly.

## Handoff Choices

Unless the recorded next step requires a named gate, present:

1. Terminate this session; continue in a clean session.
2. Proceed to the recorded next step in this session.
3. Show a dry run for the recorded next step in this session.
4. Discuss or correct the result or next step.

If option 1 is presented, include the clean session prompt before or immediately after the choices.

If the recorded next step requires a named gate, present that gate instead of immediate proceed choices.

## Stop Conditions

Stop after presenting the completion summary, handoff choices, and clean session prompt when applicable.

Do not continue into the next step unless the user explicitly chooses to proceed in the current session.
