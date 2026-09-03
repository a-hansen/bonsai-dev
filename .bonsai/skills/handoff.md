# Handoff

## Purpose

Close an authorized exact next step, reconcile current execution truth, preserve a clean resume point, report the
actual result, and present the applicable continuation gate.

A handoff is not a session log. It does not control the host application: Bonsai cannot terminate, clear, reset,
or create a session.

## When to Load

Load this skill when:

- an exact next step is complete;
- a phase, pass, contract, or workflow reaches a natural boundary;
- the human requests a handoff; or
- the current session is ending and durable resume state must be reconciled.

Do not claim the step complete or present continuation choices until this workflow has finished reconciliation.

## Required Inputs

Read only what the handoff needs:

- the approved basis and exact next step;
- the completed changes and actual check results;
- affected project final truth;
- `<project-home>/agent_plan.md` and `<project-home>/agent_state.md`;
- the active `plan/agent_plan_phase_<N>.md`, when applicable;
- an approved dry-run baseline, when present;
- meaningful unreviewed out-of-scope observations, when any were noticed; and
- the invoking workflow or gate.

Load `icebox.md` only when reviewing or maintaining a human-selected observation. Load
`templates/icebox_template.md` only when the human authorizes the first preserved observation or its structure is
needed for a newly authorized entry.

Treat project final truth and `icebox.md` as human-owned. Treat execution memory and applicable agent context as
agent-owned. Current working-tree contents remain the human's baseline; do not enumerate unrelated changes.

## Completion Reconciliation

1. Verify the completed work against its approved contract, plan, exact next step, and success condition.
   Distinguish checks actually run from checks deferred or unavailable. A failed required check is not completion.
2. If an approved dry-run baseline exists, compare actual touch points, results, checks, and final-truth impact
   with it. A material deviation returns to the owning correction, planning, contract, or final-truth gate.
3. Classify actual final-truth impact:
   - `None`: approved human-owned truth already covers the result;
   - `Clarification`: intended behavior is unchanged, but affected truth should be stated more precisely;
   - `Revision`: intended behavior, constraints, architecture, or system boundaries changed.
4. For `Clarification` or `Revision`, name the affected human-owned documents and delegate to
   `skills/final_truth_update.md`. Do not silently edit final truth or claim revised work complete before the
   required update and approval. Return through the Handoff Gate Return rules afterward.
5. Determine whether the completed work reaches the completion boundary of an authorized standard prompt, skill,
   or template addition, removal, rename, or material responsibility change. When it does, delegate affected
   category-guide reconciliation and validation to `skills/artifact_index.md` before claiming the lifecycle
   change complete. For an intermediate step in an approved multi-step lifecycle change, preserve reconciliation
   as required upcoming work and do not misrepresent the larger change as complete. Routine internal edits and
   runtime map changes do not trigger this workflow.
6. When the work established or disproved qualifying durable operational knowledge, delegate its maintenance to
   `skills/agent_context.md`. Do not dump troubleshooting history into context during handoff.
7. Reconcile all agent-owned execution memory whose current truth changed:
   - update `agent_plan.md` when roadmap, phase status, mode, or completion truth changed;
   - update the active phase plan when its step, pass, review, or completion truth changed;
   - update `agent_state.md` with one current execution condition, exact next step, readiness, and unresolved
     blockers;
   - when a phase completed, first mark that phase complete and inspect the approved roadmap for any pending,
     active, or otherwise unfinished phase that still belongs to the current body of work;
   - when unfinished roadmap work remains, identify and activate the next applicable phase, then derive and record
     its planning, review, blocker, or execution gate instead of recording body-of-work completion;
   - when no unfinished approved roadmap work remains, record body-of-work completion and only then permit
     `Execution Readiness: Complete`; and
   - remove an expired dry-run baseline after completion, abandonment, material change, or redirection.
8. Clean `agent_state.md` before reporting:
   - remove the completed next step and replace it with the actual next step;
   - remove blockers only when evidence shows they are resolved;
   - remove obsolete active files, stale commentary, expired review state, and superseded assumptions;
   - replace prior snapshot text with current resume truth rather than appending history; and
   - retain only information a later session needs to resume safely.
9. Recompute execution readiness from reconciled durable state. A plan's existence alone is not authorization.
   `Complete` is valid only when the approved roadmap is exhausted for the current body of work. If an
   identifiable unfinished roadmap phase remains, the handoff must establish that phase's applicable next gate
   and must not surface body-of-work completion.
10. Handle any unreviewed out-of-scope observations under the rules below.
11. Present the completion summary and applicable handoff gate through `skills/menu.md`, then stop for the human's
    choice.

## Out-of-Scope Observations

Do not automatically write observations to `icebox.md`, execution memory, final truth, or agent context.

At the natural gate:

- when none exist, omit observation commentary;
- when meaningful unreviewed observations exist, report only
  `Out-of-scope observations available: <N>.`;
- do not reveal or persist details until the human chooses review; and
- never imply that preservation authorizes implementation.

When the human chooses review, present observations concisely and one at a time or as a small numbered set. For
each observation, ask whether to:

1. leave it unpreserved;
2. preserve it in `icebox.md` for later triage;
3. discuss or take another explicitly authorized action; or
4. stop reviewing.

If preservation is selected:

1. capture only the selected observation, why it is worth retaining, its current `Deferred` status, the context
   in which it was observed, and a possible destination;
2. if `icebox.md` is absent, instantiate `templates/icebox_template.md` with the project name and the fully
   populated first entry `ICE-001`;
3. if it exists, read it and add the next unused `ICE-<NNN>` entry without changing other durable meaning;
4. leave no template placeholders in the project file; and
5. do not copy the observation into `agent_plan.md`, `agent_state.md`, a phase plan, final truth, or the completion
   summary as prospective work.

Leaving or rejecting an unpersisted observation creates no durable entry. Existing icebox entries may be marked
`Promoted`, `Rejected`, or `Superseded`, redirected, or pruned only under the human's disposition. Remove rejected
or superseded entries when they have no continuing value instead of retaining history for completeness.

`icebox.md` remains non-authoritative. Promotion becomes active work only after the appropriate design, roadmap,
planning, or execution gate records that new authority.

## Handoff Gate Return

The handoff remains the parent gate when it invokes observation review, correction, final-truth handling, agent
context maintenance, triage, or discussion.

After subordinate work completes:

1. reconcile any execution memory or completion facts that changed;
2. recompute the exact next step and execution readiness;
3. refresh the completion summary;
4. return to the handoff with concrete current choices; and
5. replace the handoff only when the subordinate action created a new required design, planning, contract,
   final-truth, review, or blocker gate.

Do not silently end the parent handoff merely because subordinate work finished.

## Completion Summary

Keep the report compact and include:

- completed step;
- material files added or modified for that step;
- checks actually performed and their results;
- relevant execution-memory updates;
- approved versus actual final-truth impact;
- final-truth updates proposed or completed, or `None`;
- dry-run comparison, when applicable;
- deviations or `None`; and
- an icebox update only when the human previously authorized it.

Exclude unrelated working-tree changes. Do not claim checks that were not run.

Then present these as standalone fields:

```text
Next step:
<concrete actual next step>

Execution readiness:
<current readiness>
```

Do not bury either field in a paragraph or refer indirectly to a "recorded next step."

## Handoff Menu

Load `skills/menu.md` and supply concrete choices derived from the reconciled fields.

When the next step is executable and no observations await review:

1. Continue with `<actual next step>` in the current session.
2. Continue with `<actual next step>` in a fresh session.
3. Review or change the next step.
4. Do not continue right now.

When the next step is executable and observations await review, insert a choice to review the `<N>` observations
before the stop choice.

Current-session and fresh-session continuation are peers. Do not recommend one over the other. Do not include Dry
Run routinely.

When readiness is `Complete`, `Blocked`, `Design required`, `Phase planning required`, or `Awaiting human review`,
omit both executable continuation choices. `Complete` may be supplied here only after completion reconciliation
has confirmed roadmap exhaustion for the current body of work. Present the concrete applicable gate or
non-execution choices. A fresh session never bypasses a blocker, design requirement, planning requirement, or
review gate.

If the next action owns a named mandatory gate, present that gate instead of a normal continuation menu.

Only an explicit current-session continuation choice authorizes the next step to begin.

## Fresh-Session Continuation

Print a fresh-session prompt only after the human chooses fresh-session continuation or explicitly requests the
prompt. Starting the new host session remains the human's action.

First determine whether startup without an explicit project would deterministically resolve the same active
project under `start.md`:

- if yes, use only the canonical pointer;
- if no, append only `Active project: <project>.` using the active project directory name.

The copyable prompt must be exactly one of:

```text
Read .bonsai/start.md and follow its instructions.
```

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

Do not append the project path, phase, pass, readiness, next step, approval state, dry-run state, workflow name,
gate instructions, required skills, blockers, or a prior-session summary. Put resume-critical facts in
`agent_state.md` before presenting the pointer.

After the self-check, tell the human to start a new session with the pointer and stop. Do not claim that Bonsai
started, reset, or ended a session.

## Stop Conditions

Stop at the applicable gate when:

- required validation or reconciliation is incomplete;
- final-truth impact requires review;
- execution memory conflicts or cannot state one safe next step;
- a subordinate action creates a new mandatory gate;
- the completion summary and handoff menu have been presented; or
- the human chooses fresh-session continuation, review, change, discussion, or no continuation.

Do not begin the next step until the human explicitly chooses current-session continuation.
