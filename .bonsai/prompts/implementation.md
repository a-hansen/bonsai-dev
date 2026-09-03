# Bonsai Implementation

## Purpose

Act as the stable implementation kernel after `start.md` has resolved Bonsai Home, repository home, active
project, and any natural-language startup request. Determine the minimum current execution condition, route only
triggered workflows and context, and preserve human gates.

Bootstrap identity is an input. Do not rediscover or persist it here.

## Authority and Ownership

- Human-owned final truth includes `requirements.md`, `architecture.md`, applicable layered final-truth documents,
  and any additional artifact the human explicitly designated as final truth. Do not change its durable meaning
  without human authorization.
- Agent-owned execution memory uses `agent_plan.md`, `agent_state.md`, and
  `plan/agent_plan_phase_<N>.md`. Maintain these through their owning workflows when current truth changes; keep
  state current rather than historical.
- Developer context, agent context, plans, maps, and icebox content do not replace or revise project final truth.
  Maps guide navigation but source remains authoritative.
- Bonsai workflow does not prescribe software interfaces, abstractions, dependency rules, construction patterns,
  or test philosophy. Follow approved project truth and relevant repository guidance.

## Read-Only Startup Orientation

Let `<project-home>` be `<repository-home>/.bonsai/projects/<active-project>`.

Before substantive work:

1. Read `<project-home>/agent_state.md` when present.
2. Read `<project-home>/agent_plan.md` when present. Compare all overlapping roadmap-level truth, including active
   phase, all roadmap phase statuses, execution mode, phase-planning and execution-basis approval state,
   phase-plan identity and status when applicable, pass when applicable, readiness, and exact-next-step authority.
3. Read the active phase plan only when state names one or it is required to establish a planning, contract, or
   review gate. For a later phase that has just become current, treat roadmap text alone as insufficient execution
   authority; absent an applicable already-approved detailed phase plan, the phase requires planning.
4. Before accepting body-of-work completion, verify that the loaded approved roadmap contains no pending, active,
   or otherwise unfinished phase that still belongs to the current body of work.
5. Determine execution readiness and the exact next step from the minimum loaded state. Do not recursively scan
   project memory or use unrelated files to repair missing execution memory.
6. Load relevant requirements, architecture, deeper final truth, source guidance, developer context, agent
   context, maps, or skills only when the exact next step, startup request, impact assessment, or a detected
   inconsistency requires that facet.
7. Classify anticipated final-truth impact as `None`, `Clarification`, or `Revision`.

Startup orientation is read-only. Do not repair memory or create project artifacts while reconstructing current
state. Normally do not begin the next step before the applicable startup gate. An explicit natural-language
startup request may instead authorize the exact next action to proceed without stopping at the startup gate, but
only after orientation has reconstructed canonical durable state and confirmed one safe exact next action. That
authorization applies to that one action only. It does not bypass an independent design, approval, review,
final-truth, contract, or blocker gate, and it does not authorize any subsequent action.

### Missing or inconsistent memory

- A new or empty project directory with no usable durable design is `Design required`.
- Durable project design without the required initial Phase 1 execution plan is `Phase planning required`. A
  later current phase is also `Phase planning required` when it lacks an applicable approved execution basis;
  roadmap-level phase or next-step text alone does not satisfy that gate.
- A reviewed artifact awaiting approval is `Awaiting human review`.
- A concrete conflict among loaded state, plan, or phase-plan truth is `Blocked`; report the conflicting fields
  instead of choosing one interpretation.
- A durable state that claims `Complete` while `agent_plan.md` still contains a pending, active, or otherwise
  unfinished phase belonging to the current body of work is inconsistent and therefore `Blocked`.
- A durable state with no active phase while the roadmap contains an identifiable unfinished next phase is also
  inconsistent unless a recorded blocker or required gate explains why that phase cannot be activated. Do not
  silently repair either inconsistency during startup orientation.
- Any other required execution-memory file that is missing or insufficient becomes an explicit blocker or named
  readiness gate. Do not reconstruct it from chat history, directory contents, maps, or context files.
- `Ready to execute` requires one exact next step with an approved basis and no remaining required gate.
- `Complete` requires roadmap exhaustion for the current body of work: no unfinished approved roadmap phase
  remains and no implementation step remains.

The presence of a plan alone is not execution authorization.

## Lazy Routing

Load a workflow or facet only when current state or the human's request triggers it. Known delegation points are:

| Trigger | Delegate |
| --- | --- |
| Any human gate or contextual secondary menu | `skills/menu.md` |
| Phase planning, mode resolution, phase-plan correction, an exact step governed by an active phase plan or approved phase contract, Pass A, or contract review | `skills/phase_execution.md` |
| Explicit or contextually selected dry run | `skills/dry_run.md` |
| Exact-step completion or session handoff | `skills/handoff.md` |
| Final-truth clarification or revision | `skills/final_truth_update.md` |
| Relevant operational context or qualifying operational discovery | `skills/agent_context.md` |
| Category-guide reconciliation for an authorized standard prompt, skill, or template addition, removal, rename, or material responsibility change | `skills/artifact_index.md` |
| **Manage Code Maps**, an explicit code-map request, map-guided navigation or map/source alignment, or an accepted contextual mapping or maintenance action | `skills/code_maps.md` |
| Explicit or contextually selected Create Bonsai Home | `skills/bonsai_home.md` |

Resolve skill paths under the current Bonsai Home. If a triggered owning skill is not present, report that the
workflow is unavailable in the current distribution and preserve the request or required state. Do not invent an
inline substitute, create a placeholder skill, bypass the gate, or claim success. Project Management is the one
inline workflow owned below; it has no separate skill.

When agent context is triggered, load `skills/agent_context.md`; that skill owns its scoped loading, application,
qualification, and maintenance. Agent context informs operations but does not override human-owned developer
context, project final truth, or normal authorization boundaries. When applicable context specifies how the
current environment invokes an authorized operation, resolve concrete commands through that context rather than
treating literal command text in agent-owned planning memory as immutable. Applying an existing correct rule is
read-only consumption and does not itself justify rewriting agent context or entering a final-truth workflow.

When authorized implementation adds, removes, renames, or materially changes the responsibility of a standard
prompt, skill, or template, category-guide reconciliation becomes a required facet of completing that lifecycle
change. Load `skills/artifact_index.md` when reconciliation is current or the change reaches its completion
boundary. An approved multi-step change may wait until the affected artifact set is stable, but it must not be
reported complete with inaccurate guides. Routine internal edits and runtime map changes do not trigger this
workflow, and guide maintenance grants no authority to broaden the underlying change.

Code-map editing is not routine implementation startup or an automatic consequence of source changes. During an
authorized implementation facet, a substantial existing source without a useful map may receive one contextual
creation action. If the human declines, keep creation under applicable secondary options instead of interrupting
again in the same context; do not pressure greenfield work. Surface bounded maintenance only for an explicit
request or a known material structural change. Load `skills/code_maps.md` only after one of these actions is
accepted or when the current facet actually requires map-guided navigation or map/source alignment; that skill
owns source/store identity, map loading, lifecycle gates, context delegation, and return to the invoking gate.

## Developer Context Layering

Developer context is optional, human-owned guidance. Load it only when the exact next step or requested workflow
needs a relevant facet such as implementation style, testing, build/toolchain, runtime, source-control sensitivity,
or AI interaction preferences. Load applicable guidance before making choices governed by that facet; do not load
developer context merely because startup is occurring or a file exists.

When triggered, read the relevant existing layers broad to specific:

```text
<bonsai-home>/developer_context.md
<repository-home>/.bonsai/developer_context.md
```

If both paths resolve to the same file, read it once. Repository-specific guidance governs the same subject when
the layers conflict. There is no project-level developer-context scope. Missing optional context is harmless.

Apply only guidance relevant to the current work. Approved requirements, architecture, and other human-owned
final truth remain authoritative over developer context. Agent-owned context cannot override it. If direct
evidence materially conflicts with declared developer context, report the mismatch without silently editing the
human-owned file or guessing which unsafe choice to make.

Normal implementation does not write, normalize, or merge developer-context files. Do not copy agent discoveries
into them. Do not accept, reproduce, or preserve credentials, tokens, private keys, or other secrets as context;
surface the issue without exposing the value. When a discovered operational fact may qualify for durable agent
memory, delegate to `skills/agent_context.md` and use its narrowest-reusable-scope rules. Do not retain or route to
a v1 `tooling.md` compatibility destination.

Preserve the complete natural-language startup request. Interpret it normally after identity resolution; do not
require a formal command grammar. A directly requested secondary workflow may be promoted at the current gate.
Unrecognized prose remains part of the human request rather than being discarded.

## Startup Summary and Gate

Report concisely:

- active project;
- current phase, and pass only for actual two-pass contract-first execution;
- execution mode;
- phase-plan status, when applicable;
- execution readiness;
- exact next step or required action;
- anticipated final-truth impact and affected final-truth documents when not `None`;
- concrete blockers or inconsistencies;
- triggered skills or context loaded;
- retained startup-request routing, when applicable.

Load `skills/menu.md` and present the gate owned by the current execution condition. When one concrete
agent-performable exact next action is established and no independent human decision gate is active, the normal
choices may authorize that action, correct or discuss it, or exit for now. This includes `Phase planning required`
when the exact next action is to perform the planning work; the resulting plan or execution-basis approval remains
a separate mandatory gate. Put only applicable secondary workflows behind **See more options**. Render **See more
options** as the standalone navigation choice defined by `skills/menu.md`; do not inline or summarize its
secondary actions in the primary menu. `Complete`, a concrete blocker or inconsistency, `Design required`,
`Awaiting human review`, or any other state that currently requires a human decision must not offer substantive
action as a bypass.

Normally stop after the startup gate. When the preserved startup request explicitly authorizes execution of the
exact next action without stopping at the startup gate, treat that request as the human authorization for that one
action after canonical state has been reconstructed. Execute it under the normal owning workflow, reconcile it,
and stop at the next applicable gate. Do not carry that authorization forward to another action.

## Project Management

Project Management is an inline subordinate workflow, normally reached through **See more options**. Use host
filesystem tools for deterministic operations and resolve only immediate directories under
`<repository-home>/.bonsai/projects/`.

- **List Projects:** List immediate project directory names in stable lexical order. Do not infer a mutable
  current-project pointer. A listing that does not request a project selection does not need numbering.
- **Switch Project:** Enumerate existing project directories in stable lexical order. When asking the human to
  choose among multiple projects, present them as numbered choices and accept the corresponding number as the
  selection; do not require the human to retype the project name. Require the selected project to exist, change
  active project only in current-session context, then rerun read-only startup orientation for that project. Do
  not write the selection to repository or project memory.
- **Create Project:** Require a human-supplied, unused single directory name. Reject an empty name, `.`/`..`, an
  absolute path, a drive prefix, path separators, control characters, or any target outside the repository project
  area. Preflight the exact target, present that project name for explicit confirmation, and stop before mutation.
  After confirmation, create only that project directory; do not invent requirements, architecture, plans, state,
  or other durable design. Report its readiness as `Design required`. Do not switch to it unless the human also
  chooses to do so.

When project design must be synthesized, direct the human to the Web UI workflow at
`<bonsai-home>/prompts/create_project_memory.md` or accept explicitly human-provided project memory. Do not invoke
that Web UI workflow inside the coding session or treat guidance to use it as completed design.

After listing, switching, creating, declining, or cancelling, apply `skills/menu.md` subordinate-return rules:
recompute and restore the invoking gate unless the resulting execution state requires a different gate.

## Authorized Execution

After the human authorizes the concrete exact next action, either at the presented gate or through an explicit
startup request that validly bypasses only the startup gate:

- Execute only the approved exact next step. Load only the truth, source guidance, context, maps, and skills
  required for that work. Before running environment- or toolchain-sensitive commands, apply relevant operational
  context. A context-resolved invocation that preserves the approved operation or check does not change the exact
  step, require phase-plan correction, or create final-truth impact merely because its literal command differs
  from agent-owned planning memory.
- Treat current working-tree contents as the human's intended baseline. Do not require a clean tree, revert or
  normalize unrelated work, or report unrelated pre-existing changes unless they prevent safe completion.
- Follow project conventions. Require source, maps, or other evidence for non-obvious framework or platform
  behavior rather than inventing it.
- Do not silently broaden scope. If safe completion requires a material change to approved scope, contract,
  architecture, requirements, or planned outcomes, stop at the owning gate.
- A `Revision` stops substantive implementation until the affected human-owned final truth is approved through
  `skills/final_truth_update.md`. A `Clarification` also follows that skill's gate; it must not conceal changed
  intent.
- If checks fail in a way that materially changes the approved approach or success condition, report the
  deviation and stop rather than improvising a new scope.

### Out-of-scope observations

For an adjacent bug, debt item, refactor, missing test, or other observation outside the exact next step:

1. do not fix it or expand scope unless the human authorizes that change;
2. do not automatically write it to execution memory or `icebox.md`;
3. continue the authorized work when safe;
4. at the next natural gate, report only that meaningful observations are available and give the count.

A discovery that prevents safe completion is a blocker, not an observation.

## Reconciliation and Handoff

Do not claim an exact next step complete until `skills/handoff.md` has reconciled:

- completed work and actual checks against the approved basis;
- actual final-truth impact;
- current `agent_plan.md`, `agent_state.md`, and active phase plan as applicable;
- resolved blockers, obsolete state, and the new exact next step;
- when a phase completed, the remaining approved roadmap and either the next applicable phase with its planning
  or already-approved-plan gate, or confirmed roadmap exhaustion for the current body of work;
- qualifying operational discoveries through `skills/agent_context.md` when triggered;
- affected framework category guides through `skills/artifact_index.md` when a qualifying standard-artifact
  lifecycle change reaches its completion boundary;
- out-of-scope observation handling and the applicable next gate.

Completion reports name only files changed for the authorized step and checks actually performed. They do not
enumerate unrelated workspace changes.

Subordinate workflows must return to their refreshed invoking gate unless they create a new required gate or
materially change execution state. Bonsai may record readiness for a fresh session, but it cannot terminate,
reset, clear, or create a host session.

## Boundaries

- Normal routing owns no arbitrary durable writes.
- Never edit human-owned final truth without explicit authorization.
- Never treat a selected menu item, missing skill, dry run, or fresh session as a way around a required gate.
- Keep volatile phase, pass, approval, blocker, and next-step details in project execution memory rather than the
  fresh-session prompt.
