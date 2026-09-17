# Bonsai Implementation

## Purpose

Stable implementation kernel after `start.md` resolves Bonsai Home, repository home, optional active workspace type/name/home, project/map candidates, and the natural-language startup request.

- No active workspace: own repository entry/routing.
- Active workspace: determine minimum current execution condition; load only triggered context/workflows; preserve human gates.
- Bootstrap identity and workspace candidates are inputs only; do not persist them here.

## Authority and Ownership

- **Human-owned project final truth:** `requirements.md`, `architecture.md`, applicable layered final-truth documents, plus artifacts explicitly designated by the human.
- **Human-owned map input:** may include `map_calibration.md`.
- Never change durable human-owned meaning without human authorization.
- **Agent-owned execution memory:** workspace `agent_plan.md`, `agent_state.md`, and applicable detailed plans. Project plans: `plan/agent_plan_phase_<N>.md`; map plans: scoped plans under `plan/`. Owning workflows keep these current, not historical.
- Developer/agent context, execution plans, generated maps, and icebox content never replace/revise project final truth or map calibration. Generated maps guide navigation; source is authoritative.
- Bonsai prescribes no software interfaces, abstractions, dependency rules, construction patterns, or test philosophy. Follow approved project truth and relevant repository guidance.

## Repository Entry Routing

If active workspace is unresolved, remain at the repository entry gate: do not classify `Design required` or inspect project/map memory.

If the retained startup request explicitly asks for **Manage Code Maps** or a specific code-map lifecycle action, delegate directly to `skills/code_maps.md` with no active workspace; repository entry is the invoking return gate.

Otherwise load `skills/menu.md` and show a primary menu headed equivalently to `Choose what you want to work with:`:

1. each established immediate project workspace, stable lexical order, individually numbered;
2. **Manage Code Maps**;
3. **Exit for now**;
4. **See more options** only if secondary repository actions apply, normally **Manage Projects** and, when applicable, **Create Bonsai Home**.

**Manage Code Maps** is a peer primary action, never hidden behind **See more options** at repository entry.

Project selection requires the directory still exists under `<repository-home>/.bonsai/projects/` and both `agent_plan.md` and `agent_state.md` remain accessible. The containing `projects/` path establishes type. Set it active in current-session context only, do not persist selection, then perform read-only startup orientation.

**Manage Code Maps** delegates with active workspace unset and retains repository entry as invoking gate.

If no projects exist, omit project choices; **Manage Code Maps** remains available and **Manage Projects** may remain secondary. Mapping does not require project creation.

A startup request requiring workspace execution but supplying no resolvable workspace never authorizes guessing one. Present repository entry or the applicable identity error first.

## Read-Only Startup Orientation

Applies only after an active workspace is structurally established.

`<workspace-home>` must be the supplied concrete directory under exactly one of:

```text
<repository-home>/.bonsai/projects/<active-workspace>
<repository-home>/.bonsai/maps/<active-workspace>
```

The containing `projects/` or `maps/` path is authoritative for workspace type. The supplied active type must match that structural kind. Mismatch = `Blocked`; do not reinterpret/fallback or infer type from workspace contents.

Before workspace-specific classification:

1. Read required `agent_state.md`.
2. Read required `agent_plan.md`; compare overlapping common truth: roadmap area/statuses, applicable execution mode and detailed-plan identity/status, readiness, blockers, exact-next-step authority, completion claims.
3. If either required shared execution-memory file became missing/inaccessible after bootstrap or repository-entry selection, classify `Blocked`; do not reconstruct it from other artifacts.
4. Read a detailed plan only if state names it or it is needed to establish the current planning/contract/review/execution/blocker gate. Never scan `plan/` to guess.
5. Derive readiness/exact next step from minimum loaded state. Never repair missing execution memory from chat history, generated maps, unrelated files, or the other workspace type's model.
6. Load additional truth, source guidance, developer/agent context, maps, or skills only when required by workspace type, exact step, startup request, impact assessment, or inconsistency.

Orientation is read-only: no memory repair or workspace artifact creation.

Normally stop at the startup gate. An explicit natural-language startup request may authorize **one exact next action** without that stop only after canonical durable state is reconstructed and one safe exact action is confirmed. It never bypasses independent design, approval, review, final-truth, contract, or blocker gates, and never authorizes a subsequent action.

### Project workspace orientation

For `project`:

1. Compare active phase, all phase statuses, execution mode, phase-planning/execution-basis approval, applicable phase-plan identity/status and pass, readiness, and exact-next-step authority.
2. Read the active phase plan only if named by state or needed for planning/contract/review. A newly current later phase requires planning unless an applicable approved detailed phase plan already exists; roadmap phase/next-step text alone is not execution authority.
3. Before body-of-work completion, verify the approved roadmap has no unfinished phase in that body of work.
4. Load deeper project truth/source/context/maps/skills only as current work or inconsistency requires.
5. Classify anticipated final-truth impact: `None`, `Clarification`, or `Revision`.

| Condition | Classification / rule |
| --- | --- |
| New/empty project; no usable durable design | `Design required` |
| Durable design lacks required initial Phase 1 plan | `Phase planning required` |
| Later current phase lacks applicable approved execution basis | `Phase planning required`; roadmap text is insufficient |
| Reviewed artifact awaits approval | `Awaiting human review` |
| State/plan/phase-plan truth conflicts | `Blocked`; report fields, do not choose |
| `Complete` claimed while current-body roadmap has unfinished phase | `Blocked` |
| No active phase while an unfinished next phase is identifiable, absent recorded blocker/required gate | `Blocked`; do not repair at startup |
| Other required execution memory missing/insufficient | Explicit blocker/readiness gate; never reconstruct from chat, directory contents, maps, or context |
| One exact step + approved basis + no remaining gate | `Ready to execute` |
| No unfinished approved roadmap phase or implementation step | `Complete` |

A project plan alone never authorizes execution.

### Map workspace orientation

For `map`, use common workspace state plus map behavior only. Do not apply project phases/final truth, phase-plan approval, contract-first passes, project design readiness, or project body-of-work completion.

Require `agent_state.md` and `agent_plan.md`; read a scoped `plan/` file only if state identifies it or the current map action requires it. `Blocked` if either required file is missing, a named detailed plan is absent, roadmap/state conflict, or completion claim is unsupported. Report the concrete deficiency; never reconstruct from `map_state.md`, generated output, project memory, or directory contents.

Before active map execution/reconciliation, require the owning map workflow to support structurally identified map workspaces, `agent_plan.md`, `agent_state.md`, and optional scoped plans. If it still depends on `workspace.md`, legacy `map_state.md`, or otherwise cannot:

- report map workflow unavailable at the current gate;
- do not invoke it, fabricate lifecycle state, or substitute project behavior.

Map execution/handoff updates require separately authorized lifecycle work.

When compatible, `skills/code_maps.md` owns source inspection, generated-map work, map/source identity, scoped execution, and map completion. `Complete` applies only to the current selected scope after roadmap/generated-output reconciliation; later source/scope changes may reactivate it.

## Lazy Routing

Load only triggered workflows/facets. Repository entry may delegate without an active workspace.

| Trigger | Delegate |
| --- | --- |
| Human gate or contextual secondary menu | `skills/menu.md` |
| Project phase planning/mode resolution/phase-plan correction; exact step governed by active phase plan or approved phase contract; Pass A; contract review | `skills/phase_execution.md` |
| Human-selected Dry Run | `skills/dry_run.md` |
| Exact-step completion/session handoff | `skills/handoff.md` |
| Project final-truth clarification/revision | `skills/final_truth_update.md` |
| An upcoming operational choice that may be governed by durable context, or a qualifying operational discovery | `skills/agent_context.md` |
| Category-guide reconciliation for authorized standard prompt/skill/template add/remove/rename/material responsibility change | `skills/artifact_index.md` |
| **Manage Code Maps**; compatible active-map execution; explicit code-map request; map-guided navigation/alignment; accepted contextual map action | `skills/code_maps.md` |

Resolve skills under current Bonsai Home. Missing triggered owner = workflow unavailable: preserve request/required state; do not invent a substitute/placeholder, bypass the gate, or claim success. **Project Management** is the sole inline workflow below.

### Agent context

When triggered, `skills/agent_context.md` owns scoped loading/application/qualification/maintenance. Agent context informs operations but never overrides human-owned developer context, project final truth, map calibration, authoritative source, or authorization boundaries.

If applicable context defines how to invoke an authorized operation in the current environment, use it; literal command text in agent-owned planning memory is not immutable. Applying an existing correct rule is read-only and alone does not justify context rewrite or final-truth workflow.

### Artifact-index reconciliation

Authorized standard prompt/skill/template add/remove/rename/material responsibility change requires category-guide reconciliation before lifecycle completion. Load `skills/artifact_index.md` when reconciliation is current or at completion boundary.

An approved multi-step change may defer this until affected artifacts stabilize, but cannot complete with inaccurate guides. Routine internal edits/runtime map changes do not trigger it; guide maintenance cannot broaden the underlying change.

### Contextual code-map paths during project work

Code-map editing is not routine project startup or an automatic consequence of source changes. **Manage Code Maps** remains first-class repository entry without a workspace.

Authorized project work may surface, but never silently authorize:

- **Create Code Map:** substantial existing source lacks a useful map.
- **Extend Code Map:** already-required source inspection establishes reusable, non-obvious, architecturally significant knowledge inadequately mapped; offer one bounded focus.
- **Refresh Code Map:** an authorized material source change affects knowledge in a known relevant map; offer the bounded affected concern.

A **known relevant map** is already project-selected, loaded/used in current work, or cheaply identifiable from current source identity without enumerating/inspecting the full store.

Only already-legitimate evidence may trigger these paths. Do not inspect unrelated source for mapping opportunities or continuously scan maps for drift. Routine local edits, narrow fixes, private refactors, formatting, tests, and changes not materially affecting mapped knowledge create no refresh pressure.

If declined/deferred, leave any still-applicable manual map action under normal secondary options; do not repeatedly interrupt the same work or create placeholder state.

Load `skills/code_maps.md` only after acceptance, when a project facet requires map-guided navigation/alignment, for explicit map lifecycle work, or for compatible active-map execution. It owns source/store identity; create/extend/refresh/rebuild semantics; map loading/generation; lifecycle gates; context delegation; return/transition behavior.

## Developer Context Layering

Developer context is optional human-owned guidance. Load only when the exact step/requested workflow needs a relevant facet such as implementation style, testing, build/toolchain, runtime, source-control sensitivity, or AI interaction preferences. Startup/file existence alone is insufficient.

When triggered, read existing layers broad to specific:

```text
<bonsai-home>/developer_context.md
<repository-home>/.bonsai/developer_context.md
```

Same resolved file: read once. Repository-specific guidance wins on the same subject. No project-level developer-context scope; missing optional context is harmless.

Apply only relevant guidance. Approved project truth, map calibration, and source remain authoritative in their scopes; agent context cannot override them. Material conflict with direct evidence: report it, do not silently edit human-owned context or guess an unsafe choice.

Normal implementation never writes/normalizes/merges developer-context files or copies agent discoveries into them. Never accept, reproduce, or preserve credentials, tokens, private keys, or other secrets as context; surface the issue without exposing the value.

Potential durable operational memory routes through `skills/agent_context.md` using its narrowest-reusable-scope rules. Never retain/route to v1 `tooling.md`.

Preserve the complete natural-language startup request; interpret normally after identity resolution, without formal grammar. A directly requested secondary workflow may be promoted at the current gate. Unrecognized prose remains part of the request.

## Dry Run Availability and Promotion

At a gate authorizing one approved exact execution step, provide optional Dry Run to `skills/menu.md`; default it under **See more options**. Load `skills/dry_run.md` only if selected.

Promote Dry Run to the primary menu only when previewing mechanics would materially reduce risk because of concrete execution characteristics: destructive/difficult-to-reverse work, bulk mutation/migration, multi-repository mutation, external/out-of-workspace writes, runtime/environment replacement, deployment/promotion, unusually hard rollback, or material uncertainty in write/touch set.

When promoted, give `skills/menu.md` a concise mechanics-based reason. Importance, size, or architectural significance alone is insufficient. Promotion is optional, never an approval gate.

Never offer Dry Run as a bypass while design, phase planning, artifact approval, contract review, final-truth resolution, blocker resolution, or another required human decision still precedes execution.

## Startup Summary and Gate

Applies only after workspace selection; repository entry uses its own gate and never manufactures workspace readiness.

Report:

- workspace type/name and current roadmap area;
- project: current phase, execution mode, applicable phase-plan status, and pass only for actual two-pass contract-first execution;
- map: current scope and applicable active scoped plan;
- readiness and exact next step/required action;
- project final-truth impact + affected documents when not `None`;
- blockers/inconsistencies;
- triggered skills/context;
- retained startup-request routing when applicable.

Load `skills/menu.md` and present the gate owned by the current condition.

If one concrete agent-performable exact next action exists with approved basis and no independent human decision gate, choices may authorize it, correct/discuss it, or exit. `Phase planning required` qualifies when the exact action is planning; approval of the resulting plan/execution basis remains a separate mandatory gate.

For an approved executable step, apply Dry Run rules first. Put only applicable secondary workflows behind **See more options**, rendered as the standalone navigation choice defined by `skills/menu.md`; never inline/summarize secondary actions in the primary menu.

`Complete`, concrete blocker/inconsistency, `Design required`, `Awaiting human review`, unavailable active-map workflow, or any other human-decision state must not offer substantive bypass action.

Normally stop at startup gate. A preserved startup request may authorize the exact next action only as defined in Read-Only Startup Orientation: execute under its owner, reconcile, stop at the next gate, and never carry authorization forward.

## Project Management

Inline subordinate workflow, normally under **See more options**. Use host filesystem tools; resolve only immediate directories under `<repository-home>/.bonsai/projects/`. A project workspace is established only when both `agent_plan.md` and `agent_state.md` exist and are accessible; its `projects/` path establishes type.

- **List Projects:** stable lexical names of established project workspaces; no mutable current-project inference. Number only when asking for selection.
- **Switch Project:** enumerate established project workspaces in stable lexical order; for multiple choices, number them and accept the number. Require the selected directory plus readable `agent_plan.md` and `agent_state.md`; activate only in current-session context; rerun read-only orientation; never persist selection.
- **Create Project:** require human-supplied, unused single directory name. Reject empty, `.`/`..`, absolute path, drive prefix, path separators, control characters, or targets outside project area. Preflight exact target, present name for explicit confirmation, then stop before mutation. After confirmation create the directory plus only the minimum agent-owned `agent_plan.md` and `agent_state.md` needed to establish the project workspace as `Design required`. Do not invent requirements, architecture, product design, implementation design, phases, or executable work. Switch only if the human separately chooses to.

If design must be synthesized, direct the human to Web UI `<bonsai-home>/prompts/create_project.md` or accept explicitly human-provided project memory. Never invoke that Web UI workflow inside the coding session or treat referral as completed design.

After list/switch/create/decline/cancel, apply `skills/menu.md` subordinate-return rules: recompute/restore invoking gate unless state now requires another. From repository entry with no project selected, return there with refreshed candidates.

## Authorized Execution

After authorization of one concrete exact action:

- Execute only that step; load only required truth/source guidance/context/maps/skills.
- Before environment/toolchain-sensitive commands, apply relevant operational context. A context-resolved invocation preserving the approved operation/check does not alter the step, require phase-plan correction, or create final-truth impact merely because literal command text differs from agent planning memory.
- Current working tree is the human's intended baseline. Do not require clean state, revert/normalize unrelated work, or report unrelated pre-existing changes unless they block safe completion.
- Follow workspace/repository conventions. Require evidence for non-obvious framework/platform behavior; do not invent it.
- Never silently broaden scope. Material change to approved scope, contract, architecture, requirements, or planned outcomes stops at the owning gate.
- Project `Revision` stops substantive implementation until affected final truth is approved via `skills/final_truth_update.md`; `Clarification` uses the same gate and may not hide changed intent.
- Map work uses project final-truth procedure only if it actually proposes project final-truth change; map calibration remains protected by its map workflow.
- A check failure materially changing approved approach/success condition must be reported and stopped, not improvised around.

### Mapping follow-up candidates

During authorized project work, retain only lightweight session-local evidence that arises naturally from already-required work:

- **Create:** substantial existing source lacks a useful map and preserved navigation would materially help future work.
- **Extend:** reusable, non-obvious, architecturally significant knowledge had to be established and is inadequately represented in an existing compatible map.
- **Refresh:** authorized source changes materially affect knowledge represented by a known relevant map.

For **Extend**, retain only implicated source/map, one bounded focus, costly/non-obvious reusable knowledge, and why useful beyond this project. For **Refresh**, retain only map, bounded affected concern, and concrete change evidence.

Non-blocking candidates never stop the authorized step. Do not load map editing, reactivate a map workspace, inspect unrelated coverage, or broaden discovery to refine them.

At the next natural project handoff, give qualifying candidates to `skills/handoff.md`, separate from generic observations; combine closely related candidates. They are not icebox items and are not written into project execution memory merely because noticed.

A mapping issue making current work unsafe is a blocker, not a deferred candidate.

### Out-of-scope observations

For an adjacent bug, debt item, refactor, missing test, or other observation outside the exact step and not a mapping candidate:

1. do not fix/broaden scope without human authorization;
2. do not auto-write it to execution memory or `icebox.md`;
3. continue authorized work when safe;
4. at the next natural gate, report only that meaningful observations exist and their count.

Anything preventing safe completion is a blocker.

## Reconciliation and Handoff

Do not claim an exact step complete until `skills/handoff.md` reconciles:

- completed work/checks against approved basis;
- actual project final-truth impact when applicable;
- current `agent_plan.md`, `agent_state.md`, and applicable detailed plan;
- resolved blockers, obsolete state, new exact next step;
- project phase completion: remaining approved roadmap plus next phase with planning/already-approved-plan gate, or confirmed roadmap exhaustion;
- map work: scope, roadmap progress, source/map identity, generated-output reconciliation through compatible handoff behavior;
- project work: qualifying Create/Extend/Refresh candidates from already-required evidence, separate from generic observations;
- qualifying operational discoveries via `skills/agent_context.md`;
- affected framework category guides via `skills/artifact_index.md` when qualifying standard-artifact lifecycle change reaches completion boundary;
- observation handling and next gate.

Completion reports list only files changed for the authorized step and checks actually performed; never unrelated workspace changes.

Subordinate workflows return to refreshed invoking gate unless they create a new required gate or materially change execution state.

Bonsai may record fresh-session readiness; it cannot terminate, reset, clear, or create a host session.

## Boundaries

- Normal routing owns no arbitrary durable writes.
- Never edit human-owned final truth without explicit authorization.
- Never use menu selection, missing skill, Dry Run, or fresh session to bypass a required gate.
- Keep volatile roadmap/detailed-plan/readiness/blocker/next-step details in workspace execution memory; keep project-only phase/pass/approval details in project execution memory. Put neither in the fresh-session prompt.
- Never persist/mutate reusable maps merely because project work exposed Create/Extend/Refresh. Accepted mapping work enters `skills/code_maps.md` under normal map identity, workspace, and bounded mapping-unit rules.
