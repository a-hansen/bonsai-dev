# Handoff

## Purpose

Close an authorized exact next step for the active project or map workspace, reconcile current execution truth,
preserve a clean resume point, report the actual result, and present the applicable continuation gate.

A handoff is not a session log. It does not control the host application: Bonsai cannot terminate, clear, reset,
or create a session.

## When to Load

Load this skill when:

- an exact next step is complete;
- a project phase, pass, contract, map action, or other workflow reaches a natural boundary;
- the human requests a handoff; or
- the current session is ending and durable resume state must be reconciled.

Do not claim the step complete or present continuation choices until this workflow has finished reconciliation.

## Required Inputs

Read only what the handoff needs:

- the current-session active workspace type, name, and home;
- the approved basis and exact next step;
- the completed changes and actual check results;
- `<workspace-home>/agent_plan.md` and `<workspace-home>/agent_state.md`;
- the active detailed plan named by state, when applicable;
- an approved dry-run baseline, when present;
- meaningful unreviewed out-of-scope observations, when any were noticed;
- qualifying contextual code-map follow-up candidates supplied by authorized project work, when any were noticed;
  and
- the invoking workflow or gate.

For a project, also load affected final truth and project phase, contract, or review state only when applicable.
For a map, load mapping scope, generated-output, and source/map identity evidence only through compatible
map-workspace behavior when applicable.

For a project, load `icebox.md` only when reviewing or maintaining a human-selected observation. Load
`templates/icebox_template.md` only when the human authorizes the first preserved observation or its structure is
needed for a newly authorized entry.

Treat project final truth, project `icebox.md`, and human-owned map calibration as human-owned. Treat workspace
execution memory and applicable agent context as agent-owned. Generated maps remain workflow output rather than
execution memory. Current working-tree contents remain the human's baseline; do not enumerate unrelated changes.

## Completion Reconciliation

1. Verify the completed work against its approved basis, plan or contract when applicable, exact next step, and
   success condition.
   Distinguish checks actually run from checks deferred or unavailable. A failed required check is not completion.
2. If an approved dry-run baseline exists, compare actual touch points, results, checks, and applicable protected
   truth impact with it. A material deviation returns to the owning correction, planning, contract, map-scope, or
   final-truth gate.
3. Reconcile common workspace execution memory whose current truth changed:
   - update `agent_plan.md` when roadmap status, active roadmap area, or workspace-scope completion truth changed;
   - update the active detailed plan when its work, review state, or completion truth changed;
   - update `agent_state.md` with one current execution condition, current objective, exact next step, success
     condition, readiness, active detailed-plan identity when applicable, and unresolved blockers;
   - remove the completed next step and replace it with the actual next step;
   - remove blockers only when evidence shows they are resolved;
   - remove obsolete active files, stale commentary, expired review state, superseded assumptions, and expired
     dry-run baselines; and
   - retain only information a later session needs to resume the active workspace safely.
4. Branch on the supplied active workspace type and perform exactly one applicable workspace-specific
   reconciliation below. A missing or unsupported type, or a mismatch between current-session identity and the
   loaded workspace entry, is `Blocked`; do not guess or fall back to the other branch.
5. Recompute the exact next step, success condition, blockers, and execution readiness from the reconciled common
   and workspace-specific truth. A plan's existence alone is not authorization. If no one safe exact next action
   exists, preserve the applicable completion, review, or blocker gate rather than inventing continuation.
6. Determine whether the completed work reaches the completion boundary of an authorized standard prompt, skill,
   or template addition, removal, rename, or material responsibility change. When it does, delegate affected
   category-guide reconciliation and validation to `skills/artifact_index.md` before claiming the lifecycle
   change complete. For an intermediate step in an approved multi-step lifecycle change, preserve reconciliation
   as required upcoming work and do not misrepresent the larger change as complete. Routine internal edits and
   runtime map changes do not trigger this workflow.
7. When the work established or disproved qualifying durable operational knowledge, delegate its maintenance to
   `skills/agent_context.md`. Do not dump troubleshooting history into context during handoff.
8. For a project, handle any qualifying contextual code-map follow-up candidates under the dedicated rules below.
   Keep them distinct from generic out-of-scope observations and do not load `skills/code_maps.md` unless the human
   accepts one of them.
9. Handle any unreviewed out-of-scope observations under the rules below.
10. Present the completion summary and applicable handoff gate through `skills/menu.md`, then stop for the human's
    choice.

## Project-Specific Reconciliation

Use this branch only when the active workspace type is `project`:

1. Classify actual project final-truth impact:
   - `None`: approved human-owned truth already covers the result;
   - `Clarification`: intended behavior is unchanged, but affected truth should be stated more precisely;
   - `Revision`: intended behavior, constraints, architecture, or system boundaries changed.
2. For `Clarification` or `Revision`, name the affected human-owned documents and delegate to
   `skills/final_truth_update.md`. Do not silently edit final truth or claim revised work complete before the
   required update and approval. Return through the Handoff Gate Return rules afterward.
3. Reconcile project-only roadmap and execution state:
   - update project phase status, mode, phase-plan status, pass, contract state, or completion truth when changed;
   - update the active phase plan when its step, pass, review, or completion truth changed;
   - when a phase completed, first mark that phase complete and inspect the approved roadmap for any pending,
     active, or otherwise unfinished phase that still belongs to the current body of work;
   - when unfinished roadmap work remains, identify and activate the next applicable phase; unless an applicable
     already-approved detailed plan for that phase exists, record `Phase planning required` and make planning that
     phase the next action rather than deriving execution authority from roadmap text;
   - when an applicable already-approved detailed plan exists, derive the next review, blocker, or execution gate
     from that approved plan;
   - when no unfinished approved roadmap work remains, record body-of-work completion and only then permit
     `Execution Readiness: Complete`.
4. Apply project phase-planning, contract, review, final-truth, and roadmap-exhaustion gates without weakening them
   through shared continuation. Roadmap-level phase text alone is not execution authority for a newly activated
   later phase.

## Map-Specific Reconciliation

Use this branch only when the active workspace type is `map`:

1. Reconcile the current mapping scope, active scoped map plan when one exists, generated map output touched by the
   completed action, source/map identity concerns, and whether generated output is sufficiently reconciled for the
   completed mapping scope.
2. Delegate source inspection, generated-output reconciliation, map/source identity, scoped map-plan behavior, and
   map-specific completion to compatible `skills/code_maps.md` behavior. If that workflow is absent or still
   depends on legacy map state instead of the shared workspace model, report the map workflow as unavailable and
   preserve a concrete blocker; do not fabricate reconciliation inline.
3. Permit `Execution Readiness: Complete` only when the current selected mapping scope has no unfinished work and
   generated output is sufficiently reconciled for that scope. A later source change, maintenance request, or
   expanded scope may reactivate the workspace.
4. Do not classify ordinary map work through project final truth, phases, phase plans, contract state, body-of-work
   exhaustion, or project icebox semantics. A map action that actually proposes a project final-truth change must
   stop at that separate project's applicable final-truth gate.

## Project Code-Map Follow-Ups

Use this section only for an active `project` workspace when the owning implementation workflow supplies a
qualifying contextual mapping candidate discovered from evidence already required by the completed authorized
project work.

Do not search source, enumerate the map store, inspect map coverage, or manufacture a mapping opportunity during
handoff. Handoff presents and routes candidates; `skills/code_maps.md` owns map identity, source alignment,
workspace reactivation or creation, mapping proposals, generated output, and map execution.

Classify each supplied candidate as one of:

- **Create Code Map:** substantial existing source lacks a useful map;
- **Extend Code Map:** reusable, non-obvious, architecturally significant knowledge learned during the project work
  is not adequately represented by an existing compatible map; or
- **Refresh Code Map:** source changed by the completed project work materially affects knowledge represented by a
  known relevant map.

Before presentation:

1. discard a candidate whose own supplied evidence no longer supports the proposed lifecycle intent;
2. combine closely related candidates into one bounded recommendation;
3. keep Create, Extend, and Refresh distinct when they concern materially different source identities or mapping
   focuses;
4. do not turn a candidate into the project's exact next implementation step, phase work, final truth, or icebox
   content merely because it is useful; and
5. do not persist a declined or deferred recommendation into project execution memory solely to remember that it
   was offered.

Present a qualifying recommendation concisely after project completion reconciliation and before the ordinary
handoff continuation menu. Include only:

- the lifecycle action: Create, Extend, or Refresh;
- the implicated source or existing map;
- one bounded proposed mapping focus;
- for Create or Extend, the reusable knowledge that was costly or non-obvious to establish and why preserving it
  would help future work; or
- for Refresh, the concrete structural source change and mapped concern believed to be stale.

Then load `skills/menu.md` and offer only applicable choices such as:

1. proceed with the proposed map action in the current session;
2. prepare the proposed map action for fresh-session continuation;
3. review or change the proposed mapping focus; and
4. defer the map follow-up and return to the project handoff.

Acceptance is authorization to enter the mapping workflow, not authorization to mutate generated output
immediately. Delegate to `skills/code_maps.md`, which must resolve the source/map identity, compatible map
workspace, mapping proposal, and bounded mapping-unit gate under its normal rules.

When the human chooses current-session mapping, the accepted map action may establish or reactivate a map workspace
and replace the active project workspace for subsequent map execution in that session. Project execution memory
must already be reconciled before that transition.

When the human chooses fresh-session mapping, first delegate to `skills/code_maps.md` far enough to establish or
reactivate the applicable map workspace and one safe exact mapping action. Only after canonical map state records
that action may normal map handoff produce the fresh-session auto-execute pointer. Do not construct an `Active map:`
pointer from a project-only recommendation that has not yet been resolved into durable map workspace state.

When the human defers, leave generated maps and map workspaces unchanged and return to the refreshed project
handoff. Do not repeatedly present the same recommendation again during the same completed work merely because it
remains technically possible.

Contextual map follow-ups are not generic out-of-scope observations. Do not include them in the observation count,
write them to project `icebox.md`, or require icebox review before the project can continue.

## Out-of-Scope Observations

Do not automatically write observations to project `icebox.md`, workspace execution memory, final truth, map
calibration, generated output, or agent context.

At the natural gate:

- when none exist, omit observation commentary;
- when meaningful unreviewed observations exist, report only
  `Out-of-scope observations available: <N>.`;
- do not reveal or persist details until the human chooses review; and
- never imply that preservation authorizes implementation.

For a project, when the human chooses review, present observations concisely and one at a time or as a small
numbered set. For each observation, ask whether to:

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

For a map, do not create or update a project-style `icebox.md`. Offer to leave the observation unpersisted or
discuss another explicitly authorized action. If it changes mapping scope or belongs in generated output, return
to the compatible map workflow for its normal scope or output decision rather than treating observation review as
authorization.

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
- for a project, approved versus actual final-truth impact and updates proposed or completed, or `None`;
- for a map, mapping-scope, source/map identity, and generated-output reconciliation when applicable;
- for a project, a qualifying contextual code-map follow-up only when one is being surfaced at this handoff;
- dry-run comparison, when applicable;
- deviations or `None`; and
- a project icebox update only when the human previously authorized it.

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

When one concrete agent-performable exact next action is established, no observations await review, and no
contextual code-map follow-up currently owns the immediate decision gate, normally supply:

1. Continue with `<actual next step>` in the current session.
2. Continue with `<actual next step>` in a fresh session and automatically execute it.
3. Review or change the next step.
4. Exit for now.

When a contextual project code-map follow-up is being surfaced, present its dedicated decision gate first. If the
human defers or declines it, recompute and return to this ordinary project handoff menu without changing the
already-reconciled project next step. If the human accepts it, route through `skills/code_maps.md` as described
above.

An agent-performable next action is not limited to `Ready to execute` implementation. It also includes a concrete
planning action under `Phase planning required`, such as planning a newly activated later phase, when no human
approval or other independent decision is required before that planning work can begin. The planning result still
stops at its required approval gate.

When the current session was itself entered through fresh-session continuation and no substantive work has
occurred since that entry, omit the fresh-session continuation choice rather than immediately suggesting another
new session. Keep this as session-local interaction context; do not persist it in project execution memory. If the
human explicitly asks for a fresh-session prompt, provide it. After substantive work or a later natural handoff,
current-session and fresh-session continuation may again be peer choices.

When an agent-performable exact next action exists and observations await review, insert a choice to review the
`<N>` observations before **Exit for now**. Do not include Dry Run routinely.

When readiness is `Complete`, `Blocked`, `Design required`, or `Awaiting human review`, omit substantive
continuation choices. For a project, `Complete` requires roadmap exhaustion for the current body of work. For a
map, `Complete` requires exhaustion of the current selected mapping scope and sufficient generated-output
reconciliation. `Phase planning required` does not by itself suppress project continuation: use the standard
continuation menu when its exact next action is agent-performable planning, and use a specialized gate when a
human decision is currently required. A fresh session never bypasses a blocker, design requirement, approval,
review, final-truth, contract, map-scope decision, or other mandatory human gate.

If the next action owns a named mandatory human-decision gate, present that gate instead of a normal continuation
menu.

An explicit current-session continuation choice authorizes the concrete exact next action to begin immediately in
the current session. An explicit fresh-session auto-execute choice authorizes a new session to reconstruct
canonical durable state and execute the exact next action it establishes without stopping at the startup gate.
That startup authorization applies to one action only and does not authorize whatever action follows it.
It expires when that reconstructed action completes or reaches its next natural gate. Keep both workspace identity
and auto-execute authorization in current-session interaction context; never write either into `agent_plan.md`,
`agent_state.md`, developer context, or agent context.

## Fresh-Session Continuation

Print a fresh-session prompt after the human chooses fresh-session continuation, chooses **Exit for now**, or
explicitly requests a prompt. Starting the new host session remains the human's action.

Derive the qualifier from the active workspace type:

- for a project, omit the qualifier only when startup without it would deterministically resolve the same project
  under `start.md`; otherwise append only `Active project: <project>.` using the directory name;
- for a map, always append `Active map: <map>.` using the directory name because ordinary startup never infers a
  map workspace.

When the human chooses the standard fresh-session continuation option, the copyable prompt must be exactly one of:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate.
```

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate. Active project: <project>.
```

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate. Active map: <map>.
```

The prompt authorizes only the one exact next action established after startup reconstructs canonical durable
state. It does not carry the rendered next-step text across sessions, create durable authorization state, or
authorize subsequent actions. If startup reconstruction instead finds a blocker, inconsistency, required human
approval or review, design requirement, or no safe exact next action, stop at that applicable gate rather than
forcing execution.

When the human chooses **Exit for now**, introduce the ordinary canonical pointer with:

```text
You can resume later with:
```

Then use the ordinary canonical pointer:

```text
Read .bonsai/start.md and follow its instructions.
```

or, when project selection must be explicit:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

or, for every map workspace:

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

When the human explicitly asks for an ordinary fresh-session startup pointer without auto-execution, use the same
ordinary canonical pointer without requiring the **Exit for now** lead-in.

Do not append a workspace path, phase, mapping scope, pass, readiness, rendered next step, approval state, dry-run
state, workflow name, required skills, blockers, or a prior-session summary. Put resume-critical facts in
`agent_state.md` before presenting the pointer.

For fresh-session continuation, tell the human to start a new session with the pointer and stop. For **Exit for
now**, present the resume lead-in and pointer, then stop. Do not claim that Bonsai started, reset, or ended a
session.

## Stop Conditions

Stop at the applicable gate when:

- required validation or reconciliation is incomplete;
- final-truth impact requires review;
- execution memory conflicts or cannot state one safe next step;
- a subordinate action creates a new mandatory gate;
- a contextual project code-map follow-up decision has been presented;
- the completion summary and handoff menu have been presented; or
- the human chooses fresh-session continuation, review, change, discussion, or **Exit for now**.

Do not begin the next step until the human explicitly authorizes it through the current-session continuation
choice or through a valid fresh-session startup request generated by the fresh-session auto-execute choice.
