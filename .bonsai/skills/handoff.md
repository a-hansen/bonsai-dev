# Handoff

## Purpose

Close an authorized exact next step for the active project/map workspace: reconcile execution truth, preserve safe resume state, report actual results, and present the applicable continuation gate.

Handoff is not a session log and cannot control the host application. Bonsai cannot terminate, clear, reset, or create sessions.

## Load When

Load when an exact next step completes; a project phase/pass/contract, map action, or other workflow reaches a natural boundary; the human requests handoff; or the session is ending and durable resume state needs reconciliation.

Do not claim completion or present continuation choices before reconciliation finishes.

## Inputs and Ownership

Read only needed inputs:

- current-session workspace type/name/home;
- approved basis and exact next step; completed changes and actual check results;
- `<workspace-home>/agent_plan.md`, `<workspace-home>/agent_state.md`, and state-named active detailed plan when applicable;
- approved dry-run baseline, if any;
- meaningful unreviewed out-of-scope observations, if noticed;
- qualifying contextual code-map candidates supplied by authorized project work, if noticed;
- invoking workflow/gate.

Project: additionally load affected final truth and phase/contract/review state only when applicable. Load `icebox.md` only to review/maintain a human-selected observation; load `templates/icebox_template.md` only for the first human-authorized preserved observation or when a newly authorized entry needs its structure.

Map: load mapping scope, generated-output, and source/map identity evidence only through compatible map-workspace behavior when applicable.

Ownership: project final truth, project `icebox.md`, and human-owned map calibration are human-owned; workspace execution memory and applicable agent context are agent-owned. Generated maps are workflow output, not execution memory. Current working-tree contents are the human baseline; do not enumerate unrelated changes.

## Completion Reconciliation

1. Verify completed work against approved basis, applicable plan/contract, exact next step, and success condition. Separate checks run from deferred/unavailable checks. Any failed required check means not complete.
2. If an approved dry-run baseline exists, compare actual touch points, results, checks, and applicable protected-truth impact. Material deviation returns to its owning correction, planning, contract, map-scope, or final-truth gate.
3. Reconcile changed common execution memory:
   - `agent_plan.md`: roadmap status, active roadmap area, workspace-scope completion truth;
   - active detailed plan: work/review/completion truth;
   - `agent_state.md`: one current execution condition, objective, exact next step, success condition, readiness, active detailed-plan identity when applicable, unresolved blockers;
   - replace completed next step with actual next step; remove blockers only with resolving evidence;
   - remove obsolete active files, stale commentary, expired review state/dry-run baselines, superseded assumptions; retain only safe-resume information.
4. Execute exactly one workspace-specific branch below using the supplied workspace type. Missing/unsupported type or current-session/workspace-entry identity mismatch is `Blocked`; never guess or fall back to the other branch.
5. Recompute exact next step, success condition, blockers, readiness from reconciled common + workspace truth. Plan existence is not authorization. If no single safe exact action exists, preserve the applicable completion/review/blocker gate.
6. If work reaches the completion boundary of an authorized standard prompt/skill/template addition, removal, rename, or material responsibility change, delegate affected category-guide reconciliation/validation to `skills/artifact_index.md` before claiming that lifecycle change complete. For an intermediate step in an approved multi-step lifecycle change, retain this as required upcoming work; do not claim the larger change complete. Routine internal edits and runtime map changes do not trigger this workflow.
7. If work established/disproved qualifying durable operational knowledge, delegate maintenance to `skills/agent_context.md`; do not dump troubleshooting history into context.
8. Project only: handle qualifying contextual code-map candidates under **Project Code-Map Follow-Ups**. Keep separate from generic observations; do not load `skills/code_maps.md` unless the human accepts one.
9. Handle unreviewed observations under **Out-of-Scope Observations**.
10. Present **Completion Summary** and the applicable handoff gate through `skills/menu.md`; stop for human choice.

## Project-Specific Reconciliation

Only for workspace type `project`.

1. Classify actual final-truth impact: `None` = approved human-owned truth already covers result; `Clarification` = behavior unchanged but truth needs more precision; `Revision` = behavior, constraints, architecture, or system boundaries changed.
2. `Clarification`/`Revision`: name affected human-owned documents; delegate to `skills/final_truth_update.md`. Never silently edit final truth or claim revised work complete before required update/approval. Then return through **Handoff Gate Return**.
3. Reconcile project roadmap/execution truth:
   - update changed phase status, mode, phase-plan status, pass, contract state, completion truth, and active phase-plan step/pass/review/completion truth;
   - on phase completion, mark it complete first, then inspect the approved roadmap for unfinished phases still in the current body of work;
   - if unfinished work remains, activate the next applicable phase. If no applicable already-approved detailed plan exists, record `Phase planning required` and make phase planning the next action. Roadmap phase text alone is not execution authority;
   - if an applicable approved detailed plan exists, derive its next review/blocker/execution gate;
   - only after no unfinished approved roadmap work remains, record body-of-work completion and permit `Execution Readiness: Complete`.
4. Shared continuation must not weaken project phase-planning, contract, review, final-truth, or roadmap-exhaustion gates.

## Map-Specific Reconciliation

Only for workspace type `map`.

1. Reconcile current scope, active scoped map plan if any, generated output touched, source/map identity concerns, and whether output is sufficiently reconciled for the completed scope.
2. Delegate source inspection, generated-output reconciliation, map/source identity, scoped map-plan behavior, and map completion to compatible `skills/code_maps.md`. If absent or still legacy-map-state-based rather than shared-workspace-based, report map workflow unavailable and preserve a concrete blocker; do not fabricate reconciliation inline.
3. `Execution Readiness: Complete` requires no unfinished work in the current selected mapping scope and sufficient generated-output reconciliation. Later source change, maintenance, or scope expansion may reactivate the workspace.
4. Do not apply project final truth/phases/phase plans/contracts/body-of-work exhaustion/icebox semantics to ordinary map work. A map action proposing project final-truth change stops at that separate project's applicable final-truth gate.

## Project Code-Map Follow-Ups

Use only for active `project` work when the owning implementation workflow supplies a qualifying contextual mapping candidate based on evidence already required by completed authorized work.

Handoff must not search source, enumerate the map store, inspect map coverage, or manufacture opportunities. It only presents/routes supplied candidates. `skills/code_maps.md` owns map identity/source alignment, map-workspace creation/reactivation, proposals, generated output, and execution.

Candidate types:

- **Create Code Map:** substantial existing source lacks a useful map.
- **Extend Code Map:** reusable, non-obvious, architecturally significant knowledge learned during project work is missing from an existing compatible map.
- **Refresh Code Map:** completed project work materially changed source knowledge represented by a known relevant map.

Before presentation: discard unsupported candidates; combine closely related ones into one bounded recommendation; keep Create/Extend/Refresh distinct for materially different source identities/focuses; never convert usefulness alone into project exact-next-step/implementation/phase/final-truth/icebox work; never persist declined/deferred candidates in project execution memory merely to remember them.

Present after project completion reconciliation and before the ordinary continuation menu. Include only: lifecycle action; implicated source/map; one bounded focus; plus either Create/Extend reusable costly/non-obvious knowledge and future value, or Refresh structural source change and mapped concern believed stale.

Load `skills/menu.md`; offer only applicable choices such as: proceed now; prepare fresh-session continuation; review/change focus; defer and return to project handoff.

Acceptance authorizes entry into mapping workflow, not generated-output mutation. Delegate to `skills/code_maps.md` to resolve source/map identity, compatible workspace, proposal, and bounded mapping-unit gate.

- Current-session mapping may establish/reactivate a map workspace and replace the active project workspace for subsequent map execution, but project execution memory must already be reconciled.
- Fresh-session mapping must first establish/reactivate the map workspace and one safe exact mapping action through `skills/code_maps.md`. Only after canonical map state records that action may normal map handoff emit an auto-execute pointer. Never build `Active map:` from an unresolved project-only recommendation.
- Deferral leaves maps/workspaces unchanged, returns to refreshed project handoff, and suppresses repeat presentation of the same recommendation during that completed work merely because it remains possible.

These follow-ups are not generic observations: exclude them from observation count and project `icebox.md`; icebox review is never required before project continuation.

## Out-of-Scope Observations

Never automatically write observations to project `icebox.md`, workspace execution memory, final truth, map calibration, generated output, or agent context.

At the natural gate: omit commentary if none; otherwise report only `Out-of-scope observations available: <N>.` Do not reveal/persist details until human review. Preservation never authorizes implementation.

### Project Review

Present observations concisely, individually or as a small numbered set. For each offer: leave unpreserved; preserve in `icebox.md` for later triage; discuss/take another explicitly authorized action; stop review.

If preserved, record only the selected observation, why worth retaining, `Deferred` status, observation context, and possible destination. If no `icebox.md`, instantiate `templates/icebox_template.md` with project name and fully populated `ICE-001`; otherwise read it and add next unused `ICE-<NNN>` without changing other durable meaning. Leave no placeholders. Do not copy the observation into `agent_plan.md`, `agent_state.md`, phase plan, final truth, or completion summary as prospective work.

Leaving/rejecting an unpersisted observation creates no durable entry. Existing entries may be `Promoted`, `Rejected`, `Superseded`, redirected, or pruned only under human disposition; remove rejected/superseded entries with no continuing value rather than retaining history.

`icebox.md` is non-authoritative. Promotion becomes active work only when the appropriate design/roadmap/planning/execution gate records new authority.

### Map Review

Never create/update project-style `icebox.md`. Offer to leave unpersisted or discuss another explicitly authorized action. If the observation changes scope or belongs in generated output, return to compatible map workflow for its normal scope/output decision; review itself grants no authorization.

## Handoff Gate Return

Handoff remains parent gate when invoking observation review, correction, final-truth handling, agent-context maintenance, triage, or discussion. After subordinate work: reconcile changed memory/completion facts; recompute exact next step/readiness; refresh summary; return with concrete current choices. Replace handoff only if subordinate work creates a required design, planning, contract, final-truth, review, or blocker gate. Never silently end handoff merely because subordinate work finished.

## Completion Summary

Keep compact. Include: completed step; material files added/modified; checks actually performed/results; relevant execution-memory updates; project approved-vs-actual final-truth impact and updates proposed/completed or `None`; map scope/source-map identity/generated-output reconciliation when applicable; project contextual code-map follow-up only when surfaced; dry-run comparison when applicable; deviations or `None`; project icebox update only if previously human-authorized.

Exclude unrelated working-tree changes. Never claim unrun checks.

Then show these standalone fields, never buried in prose or referenced indirectly:

```text
Next step:
<concrete actual next step>

Execution readiness:
<current readiness>
```

## Handoff Menu

Load `skills/menu.md`; derive choices from reconciled fields.

Default when one concrete agent-performable exact action exists, no observations await review, and no contextual code-map follow-up owns the immediate gate:

1. Continue with `<actual next step>` in the current session.
2. Continue with `<actual next step>` in a fresh session and automatically execute it.
3. Review or change the next step.
4. Exit for now.

Code-map follow-up gate comes first. Defer/decline: recompute and return to ordinary project menu without changing the reconciled project next step. Accept: route through `skills/code_maps.md`.

Agent-performable includes concrete planning under `Phase planning required` when no human approval/independent decision is needed before planning starts; the resulting plan still stops at its approval gate.

If this session itself began via fresh-session continuation and no substantive work has occurred since entry, omit another fresh-session choice. Keep this session-local, never in project execution memory; still provide a fresh-session prompt if explicitly asked. After substantive work or a later natural handoff, current/fresh choices may again be peers.

If an agent-performable action exists and observations await review, insert `Review the <N> observations` before **Exit for now**. Do not routinely include Dry Run.

Readiness/gate rules:

- `Complete`, `Blocked`, `Design required`, `Awaiting human review`: no substantive continuation choices.
- Project `Complete` requires current-body-of-work roadmap exhaustion; map `Complete` requires current selected-scope exhaustion + sufficient generated-output reconciliation.
- `Phase planning required` permits standard continuation when its exact next action is agent-performable planning; use a specialized gate when a human decision is required.
- Fresh-session continuation never bypasses a blocker, design requirement, approval, review, final-truth, contract, map-scope decision, or other mandatory human gate.
- A named mandatory human-decision gate replaces the normal continuation menu.

Authorization rules:

- Current-session choice authorizes only the concrete exact next action to begin immediately.
- Fresh-session auto-execute choice authorizes a new session to reconstruct canonical durable state and execute the exact action established there without stopping at startup gate; it authorizes one action only, not its successor, and expires when that action completes/reaches its next natural gate.
- Workspace identity and auto-execute authorization remain current-session interaction context only; never write them to `agent_plan.md`, `agent_state.md`, developer context, or agent context.

## Fresh-Session Continuation

Print a prompt after fresh-session continuation, **Exit for now**, or explicit prompt request. The human starts the new host session.

Always preserve the active workspace identity in the fresh-session pointer. Project appends `Active project: <project>.` using the directory name. Map appends `Active map: <map>.` using the directory name. Do not discard known identity merely because `start.md` could infer the same workspace.

Standard fresh-session continuation prompt must be exactly one of:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate. Active project: <project>.
```

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate. Active map: <map>.
```

It authorizes only the one exact action established after startup reconstructs canonical durable state; it does not carry rendered next-step text across sessions, create durable authorization, or authorize later actions. If reconstruction finds a blocker, inconsistency, required human approval/review, design requirement, or no safe exact action, stop at that gate rather than force execution.

For **Exit for now**, introduce with exactly:

```text
You can resume later with:
```

Then use the applicable ordinary pointer:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

Always include the active workspace qualifier. For an explicitly requested ordinary fresh-session pointer without auto-execution, use the same pointer without the **Exit for now** lead-in.

Never append workspace path, phase, mapping scope, pass, readiness, rendered next step, approval state, dry-run state, workflow name, required skills, blockers, or prior-session summary. Put resume-critical facts in `agent_state.md` before presenting the pointer.

Fresh-session continuation: tell the human to start a new session with the pointer, then stop. **Exit for now**: present lead-in + pointer, then stop. Never claim Bonsai started, reset, or ended a session.

## Stop Conditions

Stop at the applicable gate when required validation/reconciliation is incomplete; final-truth impact needs review; execution memory conflicts or cannot state one safe next step; subordinate work creates a mandatory gate; a contextual project code-map decision has been presented; completion summary + handoff menu are presented; or the human chooses fresh-session continuation, review, change, discussion, or **Exit for now**.

Never begin the next step until explicitly authorized through current-session continuation or a valid fresh-session startup request generated by the fresh-session auto-execute choice.
