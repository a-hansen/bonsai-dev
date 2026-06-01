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
* `icebox.md`, when present.
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

## Icebox Placement

Out-of-scope observations must be recorded in `icebox.md`, not as durable Icebox sections inside `plan.md`, `state.md`, active phase plans, handoff summaries, or other project-memory documents.

A phase plan may mention that icebox items were captured during the phase, but the durable entries must live in `icebox.md`.

At handoff, if an active phase plan contains a durable `Icebox` section, migrate those entries to `icebox.md` and replace the phase-plan section with a brief note such as:

```text
Out-of-scope observations captured during this phase were moved to `../icebox.md`.
```

Do not treat migrated icebox entries as approved backlog, requirements, architecture, roadmap, or authorized next work.

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

When the handoff offers a clean-session option, provide this exact copyable prompt format:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

Replace `<project>` with the active Bonsai project key or project memory directory name.

Do not add project path, recorded exact next step, approval status, dry-run status, workflow name, phase name, pass name, gate instructions, required skills, stop conditions, previous-session summary, or next-session instructions to the copyable prompt.

Those details must be recorded in `state.md` before handoff. The next session must discover them through the normal `implementation_prompt.md` startup/read-only pass.

The clean-session prompt is only a pointer into Bonsai. It is not a handoff summary.

### Canonical Prompt Self-Check

Before presenting a clean-session prompt, verify that the prompt contains only:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

The clean-session prompt must not contain:

* The exact next step.
* Phase name or phase number.
* Pass name.
* Approval status.
* Dry-run status.
* Stop condition.
* Required skills.
* Project path.
* Summary of previous work.
* Instructions copied from `state.md`.

If any of that information seems useful for the next session, update `state.md` instead.

The clean-session prompt is a pointer, not a handoff packet.

## Handoff Choices

Unless the recorded next step requires a named gate, present:

1. Terminate this session and continue in a clean session using the canonical startup prompt.
2. Proceed to the recorded next step in this session.
3. Show a dry run for the recorded next step in this session.
4. Discuss or correct the result or next step.

If option 1 is presented, include the clean-session prompt before or immediately after the choices.

When presenting option 1, show only the canonical startup prompt. Do not append explanatory context inside the copyable prompt block.

Any explanatory context must appear in the completion summary or handoff summary outside the copyable prompt.

If the recorded next step requires a named gate, present that gate instead of immediate proceed choices.

## Stop Conditions

Stop after presenting the completion summary, handoff choices, and clean-session prompt when applicable.

Do not continue into the next step unless the user explicitly chooses to proceed in the current session.
