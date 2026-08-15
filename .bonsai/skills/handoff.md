# Handoff Skill

## Purpose

Close an approved exact next step, reconcile the result against its approved basis, update required Bonsai
execution-memory artifacts, and record the next step cleanly.

A handoff is not a historical session summary. It preserves only what the next implementation session needs
and reports enough completed-work detail for the human to verify the result.

Bonsai cannot clear, terminate, reset, or create the human's session.

## Required Inputs

Before producing a handoff, inspect the relevant approved basis for the work:

* Approved contract, phase plan, or recorded exact next step.
* Approved dry-run baseline, when one exists.
* Approved final-truth impact, when one exists.
* Current `state.md`.
* Active `plan/plan_phase_<N>.md`, when applicable.
* Human-owned final-truth documents affected by the completed work.
* `icebox.md` only when the completed step explicitly involved a previously preserved observation.
* `.bonsai/templates/icebox_template.md` when the human chooses to preserve an observation and `icebox.md`
  does not yet exist.

## Handoff Procedure

After completing the exact next step:

1. Verify the completed work against the approved basis.

2. Classify actual impact on human-owned final truth:

    * `None`: Approved human-owned final truth already covers the completed work.
    * `Clarification`: Intended behavior is unchanged, but human-owned final truth should be stated more precisely.
    * `Revision`: Completed or required work changes intended behavior, constraints, architecture, or system boundaries.

3. Resolve final-truth handling:

    * If actual impact is `None`, report `None`.
    * If actual impact is `Clarification`, propose the affected human-owned document update unless it was completed
      under explicit human instruction.
    * If actual impact is `Revision`, do not treat revised work as complete until affected human-owned final-truth
      documents are updated and approved.

4. Update required Bonsai execution-memory artifacts according to `implementation_prompt.md`, including as applicable:

    * `plan.md`
    * `state.md`
    * active `plan/plan_phase_<N>.md`
    * shared maps

5. If work followed an approved dry run, compare actual results, checks, touch points, and final-truth impact
   against the approved execution baseline. Remove the active baseline from `state.md` after completion,
   abandonment, or redirection.

6. Recompute and record the exact next step and execution readiness in `state.md` from the reconciled current truth.

7. Clean `state.md` before handoff:

    * remove the completed next step,
    * remove resolved blockers,
    * remove obsolete active files,
    * remove stale commentary,
    * replace old snapshot text with current reality,
    * remove expired dry-run baseline content,
    * retain only resume-critical information.

8. If meaningful out-of-scope observations were noticed but not human-triaged, do not automatically preserve
   them. Report only that observations are available for review and give the count.

9. Present the completion summary and handoff gate. Do not begin the next step unless the human explicitly chooses
   current-session continuation. If the human chooses fresh-session continuation, provide the canonical prompt and stop.

## Out-of-Scope Observation Handling

Do not automatically write out-of-scope observations to `icebox.md`.

At handoff:

* If no meaningful out-of-scope observations exist, say nothing about them.
* If meaningful observations exist and have not been reviewed, report:
  `Out-of-scope observations available: <N>.`
* If the human asks to review them, present them concisely and concretely.
* After presenting an observation, ask:

  `Should this observation be preserved for later triage?`

  1. Leave it unpreserved for now.
  2. Preserve it in `icebox.md`.
  3. Discuss before deciding.
  4. Other.

* If the human explicitly chooses to preserve or defer an observation, write it to `icebox.md`.
* If `icebox.md` does not yet exist, create it from `.bonsai/templates/icebox_template.md`, instantiate the
  project name and first `ICE-<NNN>` entry, and do not leave template placeholders in the project file.
* If the human rejects or leaves an unpersisted observation unpreserved, let it disappear rather than creating
  historical baggage.
* Do not put durable observation lists in `state.md`, `plan.md`, phase plans, or handoff summaries.

Existing human-triaged `icebox.md` entries remain non-authoritative and are not automatically promoted into
future work.

Observation review is subordinate to the handoff gate that invoked it. If the human chooses another action
while reviewing an observation, such as immediate correction, clarification, or triage, complete that authorized
subordinate workflow and then apply the Gate Return rule below.

## Gate Return Rule

A handoff remains the active parent gate when it invokes a subordinate workflow such as:

* observation review,
* immediate correction of an observation,
* final-truth clarification,
* final-truth revision,
* triage, or
* discussion that results in an authorized workflow change.

After the subordinate workflow completes:

1. Reconcile `state.md`, `plan.md`, and any active phase plan whose current truth changed.
2. Recompute the exact next step and execution readiness from the reconciled project memory.
3. Refresh any completion-summary facts that changed.
4. Return to the invoking handoff gate with concrete current choices.
5. If the subordinate workflow materially changed execution or created a new required gate, present that new gate
   instead of the prior handoff menu.

Do not silently stop after completing a subordinate action. In particular, fixing an out-of-scope observation
immediately does not end the handoff that surfaced it.

## Completion Summary

Output a compact completion summary containing:

* Completed step.
* Material changes.
* Checks/results.
* Relevant Bonsai execution-memory updates.
* Approved versus actual final-truth impact.
* Final-truth updates proposed or completed, or `None`.
* Dry-run baseline comparison, when applicable.
* Deviations or `None`.
* Icebox update only when the human had previously authorized preservation.

Then present these as standalone fields, never embedded inside another paragraph or summary item:

```text
Next step:
<actual next step>

Execution readiness:
<status>
```

The next-step text must state the concrete action. Do not describe it indirectly as the "recorded next step."

Do not claim completion without reporting the checks actually performed and their results.

### Changed Files Reporting

At completion, report files added or modified as part of the completed step. Do not enumerate unrelated
pre-existing working-tree changes unless they affected execution or require human attention.

## Handoff Menu

After the completion summary, present:

`What would you like to do next?`

Use concrete action text derived from the current `Next step` field.

When out-of-scope observations are available and the recorded next step is executable:

1. Continue with `<concise actual next step>` in the current session.
2. Continue with `<concise actual next step>` in a fresh session.
3. Review or change the next step.
4. Review the `<N>` out-of-scope observation(s).
5. Do not continue right now.

When no out-of-scope observations are available and the recorded next step is executable:

1. Continue with `<concise actual next step>` in the current session.
2. Continue with `<concise actual next step>` in a fresh session.
3. Review or change the next step.
4. Do not continue right now.

Do not mark either continuation choice as recommended. Bonsai identifies the next project action, but the human
chooses whether to perform it in the current session or a fresh one.

If there is no executable next step because execution readiness is `Complete`, `Blocked`, `Design required`,
`Phase planning required`, or `Awaiting human review`, omit both continuation choices and present the concrete
applicable gate or non-execution choices instead. Never imply that a fresh session bypasses a required gate or
blocker.

If the current next step requires a named gate, present that named gate instead of a normal continuation menu.

Do not routinely include a dry-run option. The human can request one at an applicable execution gate, and Bonsai
may suggest one only when unusual execution risk or ambiguity makes it materially useful.

## Fresh Session Continuation

Fresh-session continuation is a first-class human choice when an executable next step exists. Do not print the
canonical prompt merely because a handoff occurred. Print it only after the human selects the fresh-session
continuation choice or otherwise explicitly asks for a fresh-session prompt.

When selected, do not execute the next step in the current session. Tell the human that starting the new session
is their action and provide:

```text
Start a fresh session yourself using:

Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

Then stop.

Replace `<project>` with the active Bonsai project key or project memory directory name.

Do not add project path, exact next step, approval status, dry-run status, workflow name, phase name, pass name,
gate instructions, required skills, stop conditions, previous-session summary, or next-session instructions to
the copyable prompt.

Those details must already be recorded in `state.md`. The new session discovers them through the normal
startup/read-only pass.

The clean-session prompt is only a pointer into Bonsai. It is not a handoff packet, and Bonsai does not claim to
start the session itself.

### Canonical Prompt Self-Check

Before presenting a fresh-session prompt, verify that the copyable prompt contains only:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

If additional information seems important for the next session, update `state.md` instead.

## Stop Conditions

Stop after presenting the completion summary and applicable handoff or named gate.

Do not continue into the next step unless the human explicitly chooses current-session continuation. If the human
chooses fresh-session continuation, provide the canonical prompt and stop without executing the next step.

When a subordinate workflow is invoked from the handoff, stop at that subordinate workflow's required human gate
when necessary. After the subordinate workflow completes, return to the invoking handoff gate unless a different
required gate has replaced it.

Do not describe the stop as terminating, clearing, resetting, or starting a session.
