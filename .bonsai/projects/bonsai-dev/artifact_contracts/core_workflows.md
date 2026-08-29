# Artifact Contracts — Core Workflows

**Project:** `bonsai-dev`  
**Status:** Seeded; Phase 1 archaeology required before implementation

> **Staging note:** Target runtime paths in these contracts are shown as they will exist after promotion under `.bonsai` / Bonsai Home. During this self-hosting refactor, new standard artifacts are first implemented under the temporary `bonsai/` staging tree. The active project continues to use Bonsai 1.4 `plan.md` / `state.md` / `plan/plan_phase_<N>.md` until Phase 5 promotion converts that execution memory to the v2 `agent_` names.


## Artifact: `.bonsai/start.md`

**Classification:** Missing

### Role

Provide the tiny repository-local runtime bootstrap for every Bonsai-enabled repository.

### Loaded when

Always first, through the canonical coding-agent instruction:

```text
Read .bonsai/start.md and follow its instructions.
```

### Inputs

- repository-local `.bonsai` anchor;
- optional `BONSAI_HOME`;
- available project directories;
- optional natural-language startup request from the human.

### Responsibilities

- establish repository home;
- resolve Bonsai Home according to the specification;
- resolve the active project for the current session;
- preserve resolved identity as current-session context;
- preserve any explicit startup request;
- load `<bonsai-home>/prompts/implementation.md`;
- hand control to the implementation kernel.

### Must not

- eagerly load requirements, architecture, maps, developer context, agent context, or specialized skills;
- persist the active project as repository-wide state;
- broadly search the filesystem to guess Bonsai Home;
- invent a formal startup command language;
- silently use a one-session path as a replacement for missing `BONSAI_HOME`.

### Reads

Only the minimum deterministic environment/repository information required to resolve identity.

### Writes

None during normal startup.

### Delegates to

```text
<bonsai-home>/prompts/implementation.md
```

### Human gates

Only when identity cannot be resolved safely, such as ambiguous project selection or unavailable Bonsai Home.

### Preserve from existing version

The v1 implementation prompt strongly protects a short stable startup instruction and keeps volatile phase/pass/next-step state out of the human's fresh-session prompt.

That principle survives.

### v2 changes

Bootstrap identity resolution moves out of the monolithic implementation prompt and into this small repository-local artifact.

The canonical startup prompt no longer embeds the active project unless the human wants to be explicit.

### Validation cases

- embedded repository with `projects/main`;
- valid `BONSAI_HOME` plus embedded fallback;
- explicit named project;
- exactly one non-main project;
- several non-main projects;
- no project;
- invalid/missing Bonsai Home without embedded standard;
- concurrent sessions choose different projects without persistent interference.

---

## Artifact: `bonsai/prompts/implementation.md`

**Classification:** Adapt from `.bonsai/implementation_prompt.md`

### Role

Stable implementation kernel and router after environment identity has already been resolved.

### Loaded when

Immediately after `.bonsai/start.md` establishes Bonsai Home, repository home, active project, and any explicit startup request.

### Inputs

- Bonsai Home;
- repository home;
- active project;
- optional startup request;
- minimum project bootstrap state needed to determine execution condition.

### Responsibilities

- load only enough state to determine execution readiness and exact next step;
- distinguish human-owned final truth from agent-owned execution memory;
- lazily load skills and facet context only when triggered;
- identify inconsistencies as blockers rather than silently choosing an interpretation;
- classify anticipated final-truth impact;
- present a concise startup summary;
- stop at the startup gate before substantive work;
- route secondary workflows without allowing them to erase their invoking gate;
- enforce exact-next-step focus, scope discipline, and material-deviation stops;
- ensure completion is reconciled through handoff rules before claiming the step complete.

### Must not

- perform bootstrap identity discovery that belongs in `.bonsai/start.md`;
- recursively load project memory merely because files exist;
- automatically load all developer context, agent context, maps, or skills;
- invent software-engineering conventions, abstractions, interfaces, test philosophy, or dependency rules;
- treat execution memory, maps, developer context, agent context, or icebox contents as project final truth;
- require a clean Git working tree;
- report unrelated pre-existing changes unless they affect safe execution;
- silently broaden scope.

### Reads

Minimum project state first, then additional durable truth, active phase plans, context, maps, or skills only when the exact next step requires them.

Exact v2 startup read order must be finalized during Phase 1 archaeology so lazy loading remains deterministic without recreating v1 eager-loading assumptions.

### Writes

Normal implementation routing does not itself own arbitrary writes.

It authorizes agent-owned maintenance through the applicable workflow contracts.

### Delegates to

Known v2 skills include:

```text
skills/menu.md
skills/phase_execution.md
skills/dry_run.md
skills/handoff.md
skills/final_truth_update.md
skills/agent_context.md
skills/code_maps.md
```

Additional project/Bonsai-Home workflow seams remain to be assigned after archaeology.

### Human gates

- startup gate;
- material execution-deviation gate when no more specific workflow owns it.

### Preserve from existing version

Preserve these learned rules from the v1 implementation prompt:

- startup is a read-only orientation pass before substantive execution;
- required inconsistencies become blockers;
- human-owned requirements/architecture are not silently edited;
- exact-next-step focus;
- current working tree is treated as the human's intended baseline;
- unrelated pre-existing Git modifications are not normalized, reverted, or noisily reported;
- out-of-scope discoveries do not expand scope or automatically enter the icebox;
- subordinate workflows return to the invoking gate after reconciliation;
- revision-level final-truth changes stop before implementation;
- framework/platform behavior requires evidence rather than invention;
- completion reports distinguish work performed from unrelated workspace state;
- Bonsai cannot terminate/reset/create the host session.

### v2 changes

- bootstrap identity resolution moves to `.bonsai/start.md`;
- project files use `agent_plan.md`, `agent_state.md`, and `agent_` ownership naming;
- global/repository/project context layering replaces repository-only developer/tooling assumptions;
- code maps become integrated workflows rather than a parallel `.bonsai/maps` control system;
- menu presentation moves into a reusable skill;
- Dry Run, Manage Projects, Manage Code Maps, and Create Bonsai Home normally live under contextual **See more options**;
- startup loads context lazily by workflow/facet trigger.

### Validation cases

- startup with Phase 1 planning required;
- startup awaiting phase-plan review;
- startup ready to execute;
- startup blocked by inconsistent memory;
- exact-next-step completion invokes handoff reconciliation;
- out-of-scope observation remains unpersisted until human triage;
- subordinate workflow returns to refreshed parent gate;
- dirty working tree does not block unrelated approved work;
- final-truth revision stops before substantive implementation.

---

## Artifact: `bonsai/skills/menu.md`

**Classification:** Missing as an independent artifact; behavior is distributed through old implementation and skills

### Role

Define consistent interaction semantics for Bonsai human gates without forcing every workflow to repeat presentation rules.

### Loaded when

A Bonsai workflow must present a human decision or a contextual secondary-action menu.

### Inputs

- invoking workflow;
- concrete current choices;
- whether secondary actions are applicable;
- whether the host already supplies a free-form choice.

### Responsibilities

- keep the primary menu focused on the immediate workflow decision;
- use concrete action wording;
- expose less-frequent actions through contextual **See more options**;
- allow a secondary action to be promoted when directly relevant;
- preserve host-provided free-form choices rather than manufacturing generic `Other`;
- support subordinate workflows and return to the invoking gate with refreshed choices;
- avoid making parent gates disappear after subordinate actions.

### Must not

- become a fixed junk drawer;
- add every Bonsai feature to every menu;
- manufacture a generic `Other` when the host already provides one;
- substitute presentation mechanics for workflow authorization;
- recommend current-session versus fresh-session continuation as inherently superior.

### Reads / Writes

No durable project memory merely for menu rendering.

The invoking workflow owns any memory changes.

### Delegates to

Only the subordinate workflow selected by the human.

### Human gates

This skill provides presentation behavior; the invoking workflow owns the meaning of the gate.

### Preserve from existing version

Extract and preserve distributed rules covering:

- supported structured choices when available;
- concrete numbered choices otherwise;
- distinction between **approve** reviewed artifacts and **proceed** with actions;
- no generic `Other` item when the host provides free-form input;
- subordinate workflow return semantics;
- fresh/current session choices as peers.

### v2 changes

Menu behavior becomes a reusable contract and **See more options** becomes the normal location for secondary workflows such as project management, code-map management, Create Bonsai Home, and Dry Run when contextually applicable.

### Validation cases

- startup primary gate remains small;
- Dry Run appears under secondary choices without becoming routine;
- subordinate map management returns to startup gate;
- observation review returns to handoff;
- host free-form input is not duplicated;
- contextually relevant secondary action can be promoted.

---

## Artifact: `bonsai/skills/phase_execution.md`

**Classification:** Keep + Adapt

### Role

Govern phase planning, execution-mode selection, phase-plan lifecycle, and contract-first two-pass gates.

### Loaded when

- Phase 1 plan must be created or corrected;
- later phase planning is genuinely warranted;
- phase execution mode is unresolved;
- Pass A or a contract review gate is active;
- phase-plan status or contract basis is inconsistent.

### Inputs

- `agent_plan.md`;
- `agent_state.md`;
- relevant requirements/architecture;
- active phase plan when present;
- exact next step.

### Responsibilities

- make Phase 1 planning mandatory before substantive implementation of a newly synthesized project;
- avoid detailed later phase plans unless they add real execution value;
- assess single-pass vs two-pass contract-first mode based on whether a durable contract independently deserves review;
- make the mode recommendation visible to the human when unresolved;
- draft phase plans from the phase template when warranted;
- maintain phase-plan approval state;
- stop at plan review gates;
- govern Pass A scope and contract review;
- ensure approved contracts are implemented faithfully;
- keep roadmap state and detailed phase state consistent.

### Must not

- create a phase plan merely because multiple files are involved;
- label ordinary implementation `Pass B`;
- require a separate prose contract when native source/schema/tests/examples are the useful review surface;
- manufacture interfaces, adapters, builders, abstractions, or dependency seams solely for the contract gate;
- begin implementation from an unapproved required phase plan;
- weaken an approved behavioral contract without review.

### Reads

- project final truth relevant to the phase;
- `agent_plan.md`;
- `agent_state.md`;
- active phase plan;
- phase-plan template only when drafting a plan.

### Writes

- `agent_plan.md`;
- `agent_state.md`;
- active `plan/agent_plan_phase_<N>.md`.

### Delegates to

- final-truth update when plan/contract work exposes clarification or revision;
- handoff at natural phase/contract boundaries;
- menu presentation at human gates.

### Human gates

- initial Phase 1 plan review;
- later phase-plan review when warranted;
- contract review after Pass A.

### Preserve from existing version

Preserve mature v1 rules including:

- Phase 1 is special and always receives a reviewable detailed plan;
- later phases only receive detailed plans when useful;
- two-pass is justified by a durable reviewable contract, not phase size;
- code-contract Pass A may use minimal source-level skeletons plus behavior-focused tests/examples;
- Pass A code and contract-test source must compile before review;
- behavior tests may remain disabled/failing until Pass B when that is part of the plan;
- approved behavior matters more than immutable test plumbing;
- fixtures/helpers/construction may change in Pass B without new contract review when behavioral expectations remain materially identical;
- require renewed contract review when approved scenarios, observable outcomes, or failure expectations are weakened or changed;
- contract gates do not imply interfaces or other indirection;
- phase plans remain execution memory, not product/architecture truth;
- current phase/pass/approval state must remain reconciled across plan and state.

### v2 changes

- v2 agent-owned filenames;
- menu/gate presentation delegates to `menu.md`;
- final-truth and context layering follow v2 scopes;
- fresh-session prompt is the v2 `.bonsai/start.md` pointer rather than the old implementation-prompt path.

### Validation cases

- new project requires Phase 1 plan;
- trivial later phase proceeds without unnecessary phase plan;
- public API phase selects two-pass;
- internally large but non-contract phase remains single-pass;
- Pass A source compiles while behavior remains unimplemented;
- test plumbing changes without semantic contract change do not cause false review gate;
- semantic contract weakening does require review.

---

## Artifact: `bonsai/skills/final_truth_update.md`

**Classification:** Keep + Adapt

### Role

Handle proposed or completed changes to human-owned project final truth without allowing execution memory or implementation behavior to silently redefine approved design.

### Loaded when

A proposed or completed step may require `Clarification` or `Revision` of requirements, architecture, or other explicitly designated human-owned final truth.

### Inputs

- invoking gate/workflow;
- proposed or completed work;
- affected human-owned final-truth documents;
- current execution memory.

### Responsibilities

- classify impact as `None`, `Clarification`, or `Revision`;
- identify affected final-truth documents;
- distinguish wording precision from actual design change;
- draft proposed updates for human review;
- require explicit approval for revision-level changes;
- apply approved updates when authorized;
- reconcile downstream execution memory after the update;
- return to the invoking gate unless a new required gate supersedes it.

### Must not

- silently edit human-owned final truth;
- bury revision-level changes in plans/state;
- treat phase plans or agent context as product/architecture authority;
- let completion of the subordinate workflow discard its parent gate.

### Reads

Affected requirements/architecture and execution memory.

### Writes

Human-owned final truth only with explicit authorization; agent-owned execution memory as needed for reconciliation.

### Delegates to

- menu behavior for review choices;
- invoking workflow after completion.

### Human gates

Required for revision; clarification approval behavior should preserve the existing explicit-human-authorization boundary for durable meaning.

### Preserve from existing version

- `None` / `Clarification` / `Revision`;
- explicit affected-document identification;
- revision stops before implementation;
- execution-memory consequences are reconciled;
- invoking-gate return rule;
- implementation behavior is not final truth until authoritative documents are updated.

### v2 changes

Use v2 ownership/naming and layered project truth. Do not treat the Bonsai framework specification itself as ordinary project final truth; changes to Bonsai's own `bonsai/specification.md` remain explicit human-owned framework changes.

### Validation cases

- wording precision with unchanged intent;
- actual architecture revision;
- clarification invoked from handoff returns to handoff;
- approved revision invalidates active phase plan and readiness is recomputed.

---

## Artifact: `bonsai/skills/dry_run.md`

**Classification:** Mostly Keep

### Role

Provide an optional read-only preview of an exact next step when requested or when unusual risk/ambiguity makes a preview materially useful.

### Loaded when

- human requests Dry Run; or
- human accepts a context-specific Dry Run suggestion.

### Inputs

- exact next step;
- approved basis;
- current execution memory;
- relevant project truth;
- relevant source/maps/context needed to preview safely.

### Responsibilities

- remain read-only;
- describe intended touch points, result, checks, likely scope concerns, and anticipated final-truth impact;
- identify uncertainties honestly;
- create a compact baseline only when the workflow calls for one;
- return to an approval/proceed decision without accidentally executing the work.

### Must not

- become a routine mandatory gate;
- appear as a primary option everywhere;
- modify project/source files as part of the preview;
- imply preview certainty when source inspection cannot establish it.

### Reads

Only what the preview needs.

### Writes

No implementation changes. Any approved compact dry-run baseline in execution memory must follow the v2 state rules and expire when no longer useful.

### Delegates to

Menu / invoking gate.

### Human gates

Approval to proceed after preview remains separate from the preview itself.

### Preserve from existing version

Preserve the optional, read-only nature; exact-next-step focus; compactness discipline; approval separation; and stop-on-material-uncertainty behavior.

### v2 changes

Dry Run normally moves under **See more options** and the state file is `agent_state.md`.

### Validation cases

- normal startup does not push Dry Run;
- explicit request produces no writes;
- unusual-risk suggestion still requires human acceptance;
- stale baseline is removed after the underlying step changes.

---

## Artifact: `bonsai/skills/handoff.md`

**Classification:** Keep + Adapt

### Role

Reconcile completed work, preserve the exact resume state, report completion, handle deferred observations, and present session-continuation choices at natural boundaries.

### Loaded when

- exact next step has completed;
- session is ending;
- a handoff is requested;
- phase/contract work reaches a natural boundary.

### Inputs

- completed step;
- project final truth;
- `agent_plan.md`;
- `agent_state.md`;
- active phase plan;
- relevant validation results;
- any unreviewed out-of-scope observations;
- invoking workflow/gate.

### Responsibilities

- reconcile agent-owned execution memory before reporting completion;
- remove stale resume state rather than appending history;
- update roadmap/phase status when current truth changed;
- classify final-truth impact of completed work;
- report actual changed files and checks performed without unrelated workspace noise;
- surface only the existence/count of meaningful unreviewed out-of-scope observations until the human chooses review;
- persist observations to `icebox.md` only after human authorization;
- present the exact next step and execution readiness as standalone resume fields;
- offer current-session and fresh-session continuation as peer choices when execution is ready;
- use the canonical v2 fresh-session prompt;
- return from subordinate review/update actions to the refreshed handoff unless a new gate supersedes it.

### Must not

- claim a step complete before reconciliation;
- turn `agent_state.md` into history;
- auto-create icebox entries;
- treat fresh session as preferred;
- claim Bonsai can terminate/reset/create a session;
- bury next step/readiness inside prose;
- enumerate unrelated dirty-tree changes.

### Reads

Current project truth, roadmap/state, active phase plan, validation evidence, and observation set.

### Writes

- `agent_plan.md`;
- `agent_state.md`;
- active phase plan when its current truth changed;
- `icebox.md` only after human chooses preservation;
- qualifying agent context should be written through the agent-context workflow, not as handoff dumping.

### Delegates to

- final-truth update;
- observation review;
- agent-context maintenance when required;
- menu presentation.

### Human gates

- observation preservation;
- final-truth updates;
- session continuation choice.

### Preserve from existing version

Preserve mature behavior around:

- exact-step completion reconciliation;
- changed-file reporting;
- out-of-scope observation count-before-detail behavior;
- human-triaged icebox;
- invoking-gate return;
- fresh/current continuation parity;
- canonical prompt self-check;
- no host-session control claims.

### v2 changes

Use v2 filenames and the canonical fresh-session prompt:

```text
Read .bonsai/start.md and follow its instructions.
```

Include explicit active project only when needed.

### Validation cases

- ordinary completed step;
- completed step with stale blocker removed;
- observation review then return to handoff;
- clarification during handoff then return;
- fresh-session choice produces pointer only, without volatile state in the prompt;
- completed phase updates both roadmap and state.

---

## Artifact: `bonsai/skills/agent_context.md`

**Classification:** Adapt from `.bonsai/skills/tooling_memory.md`

### Role

Govern durable agent-owned operational memory at developer, repository, and project scopes.

### Loaded when

A relevant operational fact may need to be applied, discovered, corrected, or preserved, including tooling/environment work, source-location knowledge, map-selection rules, and other stable working rules.

### Inputs

Effective context scopes:

```text
$BONSAI_HOME/agent_context.md
repo/.bonsai/agent_context.md
repo/.bonsai/projects/<project>/agent_context.md
```

plus current evidence and the exact next step.

### Responsibilities

- lazy-load only relevant agent context;
- layer broader to more specific context;
- apply more specific statements when scopes conflict;
- preserve a learned fact only when durable, actionable, sufficiently supported, reusable, and operational;
- store the current useful rule rather than troubleshooting history;
- choose the narrowest reusable scope;
- create a context file only when a qualifying fact exists;
- consolidate, correct, or prune stale entries;
- keep secrets out.

### Must not

Use agent context to:

- store active project selection;
- store transient blockers instead of `agent_state.md`;
- override approved requirements/architecture;
- silently modify developer-owned context;
- authorize software installation, machine configuration changes, dependency changes, scope expansion, credential changes, or acceptance of failed required checks;
- preserve speculative causes or failed-command history.

### Reads

Relevant scope layers only when the current facet needs them.

### Writes

The narrowest applicable `agent_context.md` scope.

### Delegates to

Normal execution workflow for actions that require authorization beyond memory maintenance.

### Human gates

No gate is required for routine agent-owned maintenance of qualifying operational facts.

Actions implied by those facts may still require normal authorization.

### Preserve from existing version

Preserve the mature tooling-memory qualification test:

- durable;
- reusable;
- actionable;
- evidence-based;
- operational.

Also preserve:

- lazy loading;
- current-rule-over-history;
- distinction from developer context;
- blocker remains in execution state while durable lesson may also enter operational memory;
- no secrets;
- proactive correction/pruning when direct evidence invalidates an old entry;
- agent-owned maintenance does not authorize environmental changes.

### v2 changes

Generalize beyond tooling to operational context and introduce developer/repository/project scopes.

Examples now include stable source locations and useful code-map selection rules.

### Validation cases

- repository-specific build rule stored at repository scope;
- project-only useful maps stored at project scope;
- cross-repository source location stored at developer scope when genuinely reusable;
- active blocker remains in `agent_state.md`;
- stale context is corrected;
- developer context conflicts are surfaced rather than silently edited.
