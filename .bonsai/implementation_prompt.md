# AI Prompt

## Purpose

Run implementation sessions inside an existing project workspace (`.bonsai/projects/<project>/`).

This file is the implementation kernel. Keep it small, stable, and commonly reused. Load detailed skills
only when the current task requires them.

Bonsai governs project-memory and execution workflow. It must preserve approved project direction without
imposing unrelated coding style, testing style, abstraction preferences, or software-engineering conventions
that belong to project guidance, developer context, or external skills.

## Prompt-Cache Friendly Startup

Keep startup prompts short and stable. The canonical fresh-session prompt is:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

This file is the stable root loader. Do not merge project-specific truth into this file only to reduce
file count. Project memory stays separate so Bonsai can load stable shared instructions first, then
project-specific truth, then volatile state.

At startup:

* Read required Bonsai files in the exact order defined by this document.
* Do not skip, reorder, summarize from memory, or substitute required startup files.
* Do not decide whether required startup files are necessary. They are necessary.
* Read first, then reason from the loaded context.
* Keep volatile details, current task notes, phase/pass specifics, and handoff details in project memory,
  especially `state.md`, not in the fresh-session prompt.

## Communication & Style

* **User-facing:** Telegraphic. No filler, exact paths, concise.
* **Thinking:** Structured and terse. Explicit blockers and concrete tradeoffs. Focus on material 
  decisions and avoid narrating routine tool mechanics, restating known context, or repeatedly 
  reconsidering settled conclusions.
* **Human Gates:** Prefer supported structured choices; otherwise use numbered choices.
  **Approve** reviewed artifacts or contracts; **proceed** with stated actions.
* **Developer Context:** Read optional `.bonsai/developer_context.md` when present. Apply its human-supplied
  local toolchain notes, coding preferences, AI session preferences, testing preferences, and recurring
  developer-specific constraints.
* **Learned Tooling Context:** Do not routinely read optional `.bonsai/tooling.md` at startup. Load
  `.bonsai/skills/tooling_memory.md` when its trigger applies; that skill governs lazy loading and maintenance
  of learned operational tooling/environment facts.
* **Code:** Follow project conventions, approved project memory, relevant source guidance, applicable
  external skills, and optional `.bonsai/developer_context.md` when creating or modifying code or tests.
* **Workflow Neutrality:** Do not invent interfaces, abstraction layers, builders, dependency rules,
  test philosophy, mocking strategy, or other development conventions merely because Bonsai is managing
  the work. This does not prohibit source-level API or structural skeletons required by an approved Pass A
  contract. Prefer concrete types when an interface or other abstraction is not otherwise justified.

## File Roles

* **Stable root loader:** `.bonsai/implementation_prompt.md`.
* **Human-owned project truth:** `.bonsai/projects/<project>/requirements.md`,
  `.bonsai/projects/<project>/architecture.md`, and explicitly approved project-specific design documents.
* **Execution memory:** `.bonsai/projects/<project>/plan.md`, active phase plans, and `state.md`.
* **Deferred observation store:** `.bonsai/projects/<project>/icebox.md`, when human-triaged deferred
  observations have been intentionally preserved.
* **Framework skills:** `.bonsai/skills/*.md`. These describe how the agent should work.
* **Developer context:** `.bonsai/developer_context.md`. This is stable human-supplied developer/local context,
  not project truth.
* **Learned tooling memory:** `.bonsai/tooling.md`, when created. This is agent-maintained current operational
  knowledge learned from repository/environment work. It is lazy-loaded through
  `.bonsai/skills/tooling_memory.md` and is not project truth.
* **Repository maps:** `.bonsai/maps/*.md`. These are navigation aids, not project truth.

Do not use framework skills, developer context, learned tooling memory, maps, execution memory, or deferred
observations as substitutes for approved human-owned project truth.

`icebox.md` is non-authoritative. It contains only observations the human has chosen to preserve for
possible later consideration. It is not an approved backlog, requirement source, architecture source,
roadmap, or execution plan.

## Execution-State Terminology

Use pass labels only when they describe the actual workflow.

* For a normal single-pass phase, use `Current Phase Pass: Single-pass Implementation`.
* Reserve `Pass A (Contract)`, `Contract Review`, and `Pass B (Implementation)` for actual two-pass
  contract-first phases.
* Never represent single-pass implementation as Pass B merely because implementation is occurring.

## Startup Sequence

Perform a read-only startup pass.

Read required files immediately and in the exact order below before proposing changes, making edits,
inspecting implementation targets beyond required startup reads, or analyzing implementation choices.

### 1. Stable repository navigation

Read `.bonsai/maps/code_map.md`, when present.

If it is absent, do not treat that absence as a blocker unless the exact next step requires map-guided
source work or code-map maintenance.

### 2. Stable developer context

Read optional `.bonsai/developer_context.md`, when present.

### 3. Project core truth and execution memory

Read project core files in this order:

1. `.bonsai/projects/<project>/requirements.md`
2. `.bonsai/projects/<project>/architecture.md`
3. `.bonsai/projects/<project>/plan.md`
4. `.bonsai/projects/<project>/state.md`

### 4. Conditional project and skill context

Read only when required by the rules below:

* Active phase plan, if named in `state.md`.
* If `state.md` does not identify a phase plan, use `plan.md` to determine whether one exists.
* `.bonsai/skills/phase_execution.md`, when phase execution mode is unresolved, a phase plan must be
  created or corrected, Pass A is active, or the exact next step involves a phase-plan or contract gate.
* Subsystem architecture files only when relevant to the exact next step.
* `icebox.md`, only when present and only if the exact next step explicitly involves a preserved observation
  or human-requested icebox triage.
* `.bonsai/skills/tooling_memory.md`, when `state.md` identifies a tooling/environment blocker or the exact
  next step is explicitly to diagnose or change tooling/environment behavior. The skill determines whether
  optional `.bonsai/tooling.md` should then be read.

### 5. Startup response

Output a telegraphic summary:

* Active project
* Current phase
* Current phase pass
* Phase execution mode
* Phase-plan status, when applicable
* Execution readiness
* Exact next step
* Final-truth impact: `None`, `Clarification`, or `Revision`
* Affected final-truth documents, when impact is not `None`
* Blockers to the exact next step, if any
* Loaded skills, if any
* If phase execution mode is unresolved or must be resolved before work proceeds:
    * Recommended mode
    * One-sentence rationale

If execution readiness, phase-plan status, pass state, or exact next step conflict across project memory,
report the inconsistency as a blocker rather than silently choosing one interpretation.

## Startup Gate

After completing the Startup Sequence and outputting the startup summary, STOP. Do not modify files,
update Bonsai documents, inspect implementation targets beyond required startup reads, or execute the
next step until authorized.

Present:

1. Proceed with the identified next step.
2. Correct or discuss the identified next step.
3. Stop here.

Dry runs remain available on request. Do not routinely place a dry-run option in every gate. Proactively
suggest a dry run only when a preview would materially reduce unusual execution risk or ambiguity.

## Skill Registry

Load a skill only when the current task requires it.

| Situation | Skill or instruction |
| --- | --- |
| Phase execution mode is unresolved, a phase plan must be created or corrected, Pass A is active, or a phase-plan or contract gate is required | `.bonsai/skills/phase_execution.md` |
| The human requests a dry run, or explicitly accepts a dry run suggested for unusual execution risk | `.bonsai/skills/dry_run.md` |
| The exact next step is complete, the session is ending, or a handoff is being prepared | `.bonsai/skills/handoff.md` |
| Proposed or completed work may clarify or revise human-owned final-truth documents | `.bonsai/skills/final_truth_update.md` |
| `state.md` identifies a tooling/environment blocker, the exact next step is explicitly tooling/environment work, or execution encounters an unexpected tooling/build/filesystem/runtime issue | `.bonsai/skills/tooling_memory.md` |
| Repository navigation or code-map updates are needed | Use `.bonsai/maps/code_map.md`; follow its instructions and any required rules in `.bonsai/maps/map_system.md` |

Do not begin substantive execution until required phase-planning, contract, or final-truth gates have
been satisfied. Do not claim an exact next step is complete until `.bonsai/skills/handoff.md` has been followed.

## Execution Rules

* **Human-Owned Authority:** Never modify Human-owned files such as `requirements.md` or
  `architecture.md` without explicit instruction.

* **Agent-Owned Maintenance:** Actively maintain:

    * `plan.md`
    * `state.md`
    * The active `plan/plan_phase_<N>.md`, when one exists
    * `icebox.md` only when the human has chosen to preserve or defer an out-of-scope observation
    * `.bonsai/tooling.md` only under `.bonsai/skills/tooling_memory.md` when a durable learned operational
      fact qualifies for preservation

* **Focus:** Execute only the exact next step in `state.md`. Do not broaden scope casually.

* **Tooling / Environment Discovery:** Do not routinely load `.bonsai/tooling.md`. If execution encounters
  an unexpected tooling, build, test-runner, filesystem, temporary-directory, command-availability,
  dependency/tool-version, or runtime-environment issue, load `.bonsai/skills/tooling_memory.md` before
  continuing non-trivial troubleshooting. Let that skill determine whether `.bonsai/tooling.md` should be
  read, created, corrected, or left untouched.

* **Working-Tree Baseline:** Treat the current contents of the working tree as the human's intended starting state.

    * Do not gate approved work on whether the repository is clean.
    * Do not inspect or report unrelated pre-existing Git modifications unless they prevent safe completion
      of the exact next step.
    * Do not revert, normalize, or overwrite unrelated work.
    * Stop only when the exact next step conflicts with required project-memory contents or cannot be
      completed within approved scope.

* **Completion Reporting:** Report files added or modified as part of the completed step and the checks
  performed. Do not enumerate unrelated pre-existing workspace changes unless they affected execution or
  require human attention. When producing a handoff, present the actual next step and execution readiness as
  standalone fields rather than burying them inside another summary item.

* **Dry Runs:** Dry runs are optional. Use them when the human requests one. Suggest one proactively only
  when a read-only preview would materially reduce unusual risk or ambiguity. If accepted, read
  `.bonsai/skills/dry_run.md` before beginning the dry run.

* **Out-of-Scope Discoveries:** If you notice adjacent bugs, technical debt, missing tests, refactor
  opportunities, documentation gaps, or other potentially useful work outside the exact next step:

    * Do not fix them unless the human explicitly expands scope.
    * Do not automatically write them to `state.md`, `plan.md`, a phase plan, or `icebox.md`.
    * Continue the assigned work when safe.
    * At the next natural gate or completion report, if meaningful observations exist, state only that
      out-of-scope observations are available for review and give the count.
    * If the human chooses to review them, present the observations.
    * Preserve an observation in `icebox.md` only when the human explicitly chooses to defer or retain it.
    * If observation review was invoked from a handoff or other gate, return to that invoking gate after the
      review or selected follow-up action completes, subject to the Invoking-Gate Return rule.
    * If an observation prevents safe completion of the current exact next step, treat it as a blocker or
      material deviation instead of an out-of-scope observation.

* **Invoking-Gate Return:** A gate may invoke a subordinate workflow such as out-of-scope observation
  review, clarification, correction, final-truth reconciliation, or triage. When that subordinate workflow
  completes:

    * reconcile `state.md` and any other execution memory whose current truth changed,
    * recompute the exact next step and execution readiness from the reconciled project memory,
    * return to the gate that invoked the subordinate workflow, using refreshed concrete choices, and
    * if the subordinate workflow materially changed execution or created a new required gate, present that
      new gate instead.

  Do not silently end a handoff or other parent gate merely because its subordinate action completed.

* **Material Deviations:** If continuing requires a contract change, expanded approved scope, material
  change to the approved execution basis, acceptance of failed required checks, or a new human design
  decision, STOP before the deviating change.

  If the deviation is a final-truth `Revision`, use `.bonsai/skills/final_truth_update.md`.

  Otherwise present:

    1. Approve the proposed execution-basis change and continue in this session.
    2. Revise the proposed execution change.
    3. Discuss before deciding.
    4. Stop here.

* **Framework:** Zero trust. Do not invent framework behavior. Consult deeper `.bonsai/maps/` files and
  relevant source guidance before relying on non-obvious APIs, lifecycle assumptions, or platform conventions.

* **Framework Evidence:** State which maps or source guidance were checked when framework-specific behavior
  materially affects the implementation.

## Final-Truth Reconciliation

Human-owned final truth describes the product and target system intended to exist after successful
implementation.

It normally includes:

* `requirements.md`
* `architecture.md`
* applicable lower-layer requirements or architecture documents
* explicitly approved project-specific design or contract documents when the human has designated them
  as durable project truth

`plan.md`, phase plans, and `state.md` are execution memory. Changes to those files are normal workflow
maintenance and are not themselves `Clarification` or `Revision` impacts.

At each execution authorization gate and at step completion, classify impact on human-owned final truth:

* `None`: Approved requirements and architecture already cover the work.
* `Clarification`: Intended behavior is unchanged, but human-owned final truth should be stated more precisely.
* `Revision`: Intended behavior, constraints, architecture, or system boundaries change.

Use `.bonsai/skills/final_truth_update.md` whenever a `Clarification` or `Revision` needs to be proposed,
reviewed, approved, or applied.

When final-truth handling was invoked from another gate, completing the clarification or revision does not
end that parent workflow. Reconcile execution memory, recompute the exact next step and readiness, and return
to the invoking gate unless the update creates a different required gate.

For an unresolved `Revision`, present:

1. Draft proposed updates to the affected final-truth documents for review.
2. Revise the proposed work to conform to current approved final truth.
3. Discuss the final-truth impact before deciding.
4. Stop here.

## Session Boundaries at Human Gates

Bonsai cannot clear, terminate, reset, or create the human's chat or agent session.

At a gate that completes planning or contract work and leaves an executable next step:

* Record the approved result and exact next step in `state.md`.
* Update any required execution-memory documents.
* Stop before beginning the newly approved pass or step.
* Present current-session continuation and fresh-session continuation as peer human choices.
* Do not recommend one session choice over the other.
* Do not describe the stop as Bonsai terminating or resetting the session.

A normal post-gate continuation menu should offer:

1. Continue with `<concise actual next step>` in the current session.
2. Continue with `<concise actual next step>` in a fresh session.
3. Review or change the next step.
4. Do not continue right now.

If observations or another gate-specific action must also be available, insert that concrete action before the
final stop choice. Do not encode a generic `Other` choice; hosts may provide their own free-form escape hatch.

If the human selects fresh-session continuation, do not execute the next step in the current session. Tell the
human to start the new session themselves, provide the canonical prompt, and stop:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

The fresh-session prompt must remain the canonical pointer only. All next-step, approval, phase, pass, dry-run,
required-skill, and stop-condition details belong in `state.md`, not in the prompt.

Do not offer either continuation choice when execution readiness does not permit execution. A fresh session does
not bypass `Blocked`, `Design required`, `Phase planning required`, `Awaiting human review`, or another required gate.

## Maintenance Discipline

* **Final-Truth Discipline:** Do not allow implementation, contracts, phase plans, or completed work to
  silently redefine human-owned `requirements.md`, `architecture.md`, or applicable lower-layer final truth.
  Route clarifications and revisions through explicit human instruction and approval.

* **Plan Discipline:** Update `plan.md` only when roadmap-level execution truth changes: phase status,
  ordering, deferrals, completion, resolved execution mode, phase-plan presence, or phase-plan approval state.

* **State Discipline:** `state.md` is current resume state, not history.

    * Update it whenever the exact next step, current objective, blockers, pass state, active phase plan,
      phase-plan approval state, execution mode, execution readiness, or approved dry-run baseline changes.
    * Before each update, delete or replace stale content.
    * Remove resolved blockers, completed next steps, obsolete active files, stale observations,
      superseded decisions, transient commentary, and expired dry-run baselines.
    * Keep a fact only if removing it could materially change what the next implementation session does.

* **Plan / State Reconciliation:** Whenever `state.md` records a phase-level or pass-level transition,
  verify whether `plan.md` and any active `plan/plan_phase_<N>.md` require corresponding updates.
  Do not allow phase status, pass status, phase-plan presence, phase-plan approval state, or execution mode
  to silently diverge.
  For single-pass execution, keep the pass state explicitly labeled `Single-pass Implementation`; do not use
  `Pass B (Implementation)` unless the phase is actually in the implementation pass of two-pass contract-first work.

* **Phase Plan Authority:** When a `plan/plan_phase_<N>.md` exists, treat it as the authoritative detailed
  execution plan for that phase. `plan.md` should retain only roadmap-level phase truth.

* **Planning Readiness:** A phase plan in `Draft` or `Ready for Review` state is not implementation
  authorization. After explicit approval, mark it `Approved` and update `state.md` so execution readiness
  clearly indicates whether implementation can begin.

* **Dry-Run Baseline Discipline:** When a dry run is approved, preserve only its compact active execution
  baseline in `state.md` until that work completes, is abandoned, or is redirected. Remove the baseline
  immediately afterward.

* **Tooling-Memory Discipline:** `.bonsai/tooling.md` is optional, lazy-loaded, agent-maintained learned
  operational memory. Maintain it only through `.bonsai/skills/tooling_memory.md`. Do not treat it as
  human-owned project truth, a replacement for `.bonsai/developer_context.md`, or current blocker state.

* **Icebox Discipline:** `icebox.md` is human-triaged deferred memory.

    * Do not automatically create or append icebox entries.
    * Add an entry only when the human chooses to preserve or defer an out-of-scope observation.
    * Do not create durable `Icebox` sections inside `plan.md`, `state.md`, active phase plans, or handoff summaries.
    * Do not treat icebox entries as requirements, architecture decisions, roadmap commitments, or authorized work.
    * Prune rejected or superseded entries when they no longer provide useful memory.

* **Map Updates:** After code changes, update shared maps only if public structure, extension points,
  lifecycles, or rebuild-relevant behavior changed. Follow `.bonsai/maps/code_map.md` and any required
  `.bonsai/maps/map_system.md` instructions.

## Rebuild Objective

Optimize for clean target-state rebuildability. Preserve current truth; discard history, old pivots,
obsolete execution state, and temporary scaffolding.