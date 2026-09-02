# Artifact Contracts — Core Workflows

**Project:** `bonsai-dev`  
**Status:** Approved; Phase 1 core archaeology complete

> **Identity and placement:** Artifact headings and owning-contract references are relative to the Bonsai standard
> root. During this bootstrap refactor, candidate artifacts are staged at `repo/bonsai/<artifact-identity>`.
> Shared runtime artifacts resolve from `<bonsai-home>/<artifact-identity>`; in Embedded Bonsai the standard root is
> `repo/.bonsai/`. `start.md` remains the repository-local bootstrap at `repo/.bonsai/start.md`. The active project
> continues to use Bonsai 1.4 execution-memory names until Phase 5 promotion.

## Batch Scope and Result

This batch reconciles the six running Bonsai 1.4 core artifacts against the authoritative v2 specification. It
closes behavior, not wording: repeated rules are consolidated under their v2 owner, obsolete v1 control-plane
placement is dropped, and specification-only behavior is recorded as `Missing` even when the target contract is
already known.

The result preserves the mature execution and gate behavior without preserving the monolithic v1 loader. Bootstrap
owns identity, the implementation prompt owns minimum-state routing, triggered skills own detailed workflows, and
`menu.md` owns reusable interaction mechanics. No core ownership seam remains unresolved.

## Source Closure

| v1.4 source | Material areas closed | Evidence records | Closure |
| --- | --- | --- | --- |
| `.bonsai/implementation_prompt.md` | stable startup pointer; startup reads and gate; file authority; exact-step authorization; working-tree baseline; deviations; observations; final truth; session boundaries; state/plan/map maintenance | `CORE-START-02`, `CORE-IMPL-01`–`CORE-IMPL-10`, `CORE-MENU-01`–`CORE-MENU-04`, `CORE-TRUTH-01`, `CORE-HANDOFF-01`, `CORE-HANDOFF-05` | Closed |
| `../../../../../skills/phase_execution.md` | mode selection; plan lifecycle; boundary discipline; Pass A/B semantics; review gates; continuation; stop conditions | `CORE-PHASE-01`–`CORE-PHASE-08` | Closed |
| `../../../../../skills/final_truth_update.md` | ownership boundary; impact classification; approval; reconciliation; invoking-gate return | `CORE-TRUTH-01`–`CORE-TRUTH-04` | Closed |
| `../../../../../skills/dry_run.md` | optional trigger; read-only preview; approved basis; baseline lifecycle; revision stop | `CORE-DRY-01`–`CORE-DRY-04` | Closed |
| `../../../../../skills/handoff.md` | completion reconciliation; state pruning; reporting; observations; gate return; session continuation | `CORE-HANDOFF-01`–`CORE-HANDOFF-06` | Closed |
| `.bonsai/skills/tooling_memory.md` | lazy operational context; qualification; authority limits; current-rule maintenance; v2 scope expansion | `CORE-CONTEXT-01`–`CORE-CONTEXT-06` | Closed |

Markdown layout, illustrative placeholder text, repeated examples, and v1.4 bootstrap filenames are not separately
preserved when the same material behavior is covered below. They are presentation or obsolete placement, not an
additional behavioral contract.

## Archaeological Evidence and Classification

Each record supplies the evidence trace required by `artifact_contracts/README.md`. Headings identify the exact
source section; specification headings identify the authoritative v2 rule.

### Startup and implementation routing

| Evidence ID | Source evidence | Specification rule | Classification and rationale | Owning contract | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `CORE-START-01` | None; v1.4 begins directly in `.bonsai/implementation_prompt.md`. | **Startup Bootstrap**; **Bootstrap responsibilities**; **Bonsai-home resolution**; **Active project is session state**. | **Missing** — v2 requires a small local bootstrap that deterministically resolves repository home, Bonsai Home, and session-local project identity before loading knowledge. | `start.md` | Exercise embedded and external-home resolution, explicit/default/unique/ambiguous/absent project selection, invalid homes, and concurrent project choices. |
| `CORE-START-02` | `.bonsai/implementation_prompt.md` — **Prompt-Cache Friendly Startup** and **Session Boundaries at Human Gates** keep the pointer short and volatile state in project memory. | **AI sessions are the primary interaction model**; **Startup Bootstrap**; **Session Boundaries**. | **Adapt** — preserve the pointer-only discipline but replace the v1 implementation-prompt path and normally embedded project key with repository-local `../../../../../start.md`; add the project only when deterministic resumption requires it. | `start.md`; `skills/handoff.md` | A normal fresh-session prompt contains only the start pointer; an ambiguous named-project topology adds only `Active project: <project>.`; no phase/pass/next-step text leaks into it. |
| `CORE-START-03` | None; v1.4 has no Bonsai Home resolver or embedded/external preference. | **Bonsai Home**; **Embedded Bonsai**; **Bonsai-home resolution**. | **Missing** — prefer a valid `BONSAI_HOME`, fall back to a valid embedded standard, otherwise ask; broad filesystem guessing and session-only path persistence are prohibited. | `start.md` | Verify external-home preference, embedded fallback, invalid environment value, no valid standard, and no filesystem-wide search or `agent_context.md` write. |
| `CORE-START-04` | The v1 fresh-session prompt accepts only the project parameter carried in the prompt. | **Startup Bootstrap** permits natural-language startup requests and rejects a formal command language. | **Missing** — v2 bootstrap must preserve and route an appended request such as Create Bonsai Home or Manage Code Maps without parsing a proprietary command grammar. | `start.md`; `prompts/implementation.md` | Explicit natural-language requests reach the correct workflow after identity resolution; unrecognized prose remains available for normal interpretation. |
| `CORE-IMPL-01` | `.bonsai/implementation_prompt.md` — **Startup Sequence**, **Startup response**, and **Startup Gate** require a read-only orientation, inconsistency reporting, concise summary, and stop. | **Implementation Workflow**; **Execution Readiness**; **Startup gate**. | **Adapt** — preserve orientation and authorization, but operate after identity resolution and use v2 execution-memory names. | `prompts/implementation.md` | Ready, blocked, design-required, planning-required, and awaiting-review states produce accurate summaries and no substantive writes before approval. |
| `CORE-IMPL-02` | `.bonsai/implementation_prompt.md` — **File Roles**, **Execution Rules**, and **Final-Truth Reconciliation** distinguish authority and prohibit execution memory from substituting for project truth. | **Specification Authority**; **Artifact Ownership**; **Project Final Truth**; **Agent Execution Memory**. | **Keep** — the authority boundary survives unchanged; only names and context scopes change elsewhere. | `prompts/implementation.md`; `skills/final_truth_update.md` | Plans, state, maps, developer context, agent context, and icebox content never authorize a requirements/architecture change. |
| `CORE-IMPL-03` | `.bonsai/implementation_prompt.md` — **Startup Sequence** always loads the code map when present, developer context when present, then all four project core files in a fixed repository-local order. | **Bootstrap should resolve identity, not load knowledge**; **Lazy Loading**; **Implementation Workflow**. | **Drop** — v2 rejects unconditional map/developer-context loading and the v1 repository-only loader. The v2 kernel always reads `agent_state.md`, reads `agent_plan.md` to validate roadmap state, reads a named active phase plan when needed to establish the gate, and then loads final truth, context, maps, and skills only when the exact step or inconsistency requires them. | `prompts/implementation.md` | Startup with an unrelated map/context does not load it; state/plan inconsistency blocks; a named review gate loads its phase plan; required facet context loads only when triggered. |
| `CORE-IMPL-04` | `.bonsai/implementation_prompt.md` — **Execution Rules**, **Material Deviations**, and **Framework** enforce exact-next-step scope, stop before unapproved deviation, and require evidence for non-obvious framework behavior. | **Implementation Workflow**; **Human control should not require constant babysitting**; **Final-truth gate**. | **Keep** — these are execution invariants independent of v1 file placement. | `prompts/implementation.md` | Approved work proceeds autonomously within scope; a contract, scope, architecture, or failed-check deviation stops at the applicable gate; framework assumptions cite maps/source guidance. |
| `CORE-IMPL-05` | `.bonsai/implementation_prompt.md` — **Working-Tree Baseline** treats current contents as intended, ignores unrelated modifications, and forbids cleanup/reversion outside scope. | **Implementation Workflow** leaves coding mechanics to repository context while requiring authorized exact-step execution. | **Keep** — this protects user work and prevents Git cleanliness from becoming an invented gate. | `prompts/implementation.md` | An unrelated dirty file neither blocks nor appears in the completion report; an overlapping change is surfaced only when safe completion is affected. |
| `CORE-IMPL-06` | `.bonsai/implementation_prompt.md` — **Out-of-Scope Discoveries** prevents automatic fixes or persistence and requires blockers to be distinguished from observations. | **Out-of-Scope Observations and `icebox.md`**. | **Keep** — preserve notice/continue/count/triage behavior; detailed handoff handling belongs to the handoff skill. | `prompts/implementation.md`; `skills/handoff.md` | Adjacent work remains unchanged and unpersisted; a safety-critical discovery blocks; only a human-selected observation enters `icebox.md`. |
| `CORE-IMPL-07` | `.bonsai/implementation_prompt.md` — **Invoking-Gate Return** and repeated subordinate-workflow rules require reconciliation and return to the parent gate. | **Subordinate workflows**. | **Adapt** — keep the invariant, centralize presentation in `menu.md`, and leave state changes with the invoking workflow. | `prompts/implementation.md`; `skills/menu.md` | Dry run, correction, observation review, and clarification each return to refreshed parent choices unless a new required gate supersedes them. |
| `CORE-IMPL-08` | `.bonsai/implementation_prompt.md` — **Maintenance Discipline** actively maintains plan/state/phase plan, prunes stale state, reconciles pass status, and conditionally maintains maps. | **Agent Execution Memory**; **File Maintenance Discipline**. | **Adapt** — retain current-truth maintenance under `agent_` names; map and agent-context maintenance delegate to their triggered skills. | `prompts/implementation.md`; `skills/handoff.md`; `skills/phase_execution.md` | State loses completed steps and resolved blockers; roadmap/phase transitions agree; map/context writes occur only under their own triggers. |
| `CORE-IMPL-09` | `.bonsai/implementation_prompt.md` — **Communication & Style** distinguishes supported choices, approval of artifacts, and proceeding with actions. | **Human Gates and Menus**; **Host-provided free-form choices**. | **Adapt** — retain the semantics but move reusable presentation rules out of the always-loaded kernel. | `skills/menu.md` | Artifact gates say approve/revise/discuss; action gates say proceed/correct/stop; a host free-form escape is not duplicated. |
| `CORE-IMPL-10` | `.bonsai/implementation_prompt.md` — **Rebuild Objective** requires current truth and removal of obsolete execution scaffolding. | **Clean Rebuild Objective**; **File Maintenance Discipline**. | **Keep** — core workflows preserve rebuildable current state rather than historical process residue. | `prompts/implementation.md`; all maintaining skills | Reconstructed project memory contains current authority, state, and approved contracts without stale gates, duplicate execution formats, or chat-only decisions. |

### Menus and phase execution

| Evidence ID | Source evidence | Specification rule | Classification and rationale | Owning contract | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `CORE-MENU-01` | `.bonsai/implementation_prompt.md` — **Communication & Style**; phase, final-truth, dry-run, and handoff skills each embed numbered gate choices. | **Human Gates and Menus**; **Primary menus**. | **Adapt** — consolidate concrete wording and structured-choice behavior into a reusable presentation skill while each workflow retains decision authority. | `skills/menu.md` | Equivalent gates use consistent concrete choices without transferring authorization logic to the menu skill. |
| `CORE-MENU-02` | No v1 artifact owns contextual secondary-menu behavior; Dry Run is manually omitted from primary gates. | **See more options**. | **Missing** — v2 requires contextual secondary actions and promotion of a secondary action only when directly relevant. | `skills/menu.md` | Startup stays focused; Manage Projects, Manage Code Maps, Create Bonsai Home, Dry Run, diagnostics, or maintenance appear only when applicable. |
| `CORE-MENU-03` | `.bonsai/implementation_prompt.md` — **Invoking-Gate Return**; final-truth and handoff skills repeat parent-gate return. | **Subordinate workflows**. | **Keep** — parent-gate identity and refreshed choices are protected behavior. | `skills/menu.md`; invoking workflow | Completing or declining a subordinate action returns to the same recomputed gate unless execution state creates a different mandatory gate. |
| `CORE-MENU-04` | `.bonsai/implementation_prompt.md` avoids generic `Other`; `../../../../../skills/handoff.md` still embeds `Other` in observation preservation. | **Host-provided free-form choices**. | **Drop** — a standard-generated generic `Other` is obsolete when the host supplies free-form input. | `skills/menu.md`; `skills/handoff.md` | No Bonsai primary or subordinate menu duplicates the host's free-form option. |
| `CORE-PHASE-01` | `../../../../../skills/phase_execution.md` — **Execution-State Terminology** and **Phase Execution Mode Assessment** distinguish single-pass from durable-contract two-pass work. | **Contract gate**; **Contract-First Two-Pass Execution**. | **Keep** — contract value, not size or internal complexity, selects two-pass; single-pass is never mislabeled Pass B. | `skills/phase_execution.md` | A public durable seam selects two-pass; a large internal change remains single-pass; labels match actual mode. |
| `CORE-PHASE-02` | `../../../../../skills/phase_execution.md` — **Phase Plan Creation** makes the initial plan mandatory and later plans conditional. | **Phase plans**; **Phase-plan gate**. | **Keep** — this matches v2 exactly. | `skills/phase_execution.md` | New project stops for Phase 1 plan review; a simple later phase avoids a needless detail plan; a sequenced/gated later phase creates one. |
| `CORE-PHASE-03` | `../../../../../skills/phase_execution.md` — **Missing or Incomplete Phase Plans**, **Phase Plan Content Requirements**, and **Phase Plan Approval Gate** correct stale plans before implementation and stop for approval. | **Execution Readiness**; **Phase-plan gate**; **Agent Execution Memory**. | **Adapt** — preserve lifecycle and review behavior using `agent_` names and menu delegation. | `skills/phase_execution.md` | Missing/stale/inconsistent required plan yields `Phase planning required` or `Awaiting human review`; approval records a concrete executable next step before work begins. |
| `CORE-PHASE-04` | `../../../../../skills/phase_execution.md` — **Approved Boundary Assessment** and **Phase Plan Content Requirements** forbid invented seams and classify unclear approved boundaries. | **Simple projects should stay simple**; **Project Final Truth**; **Pass A: Contract**. | **Keep** — planning records only approved or necessary durable boundaries. | `skills/phase_execution.md` | A plan does not invent modules/interfaces/dependency rules; a genuine ambiguity routes to plan correction, clarification, revision, or observation. |
| `CORE-PHASE-05` | `../../../../../skills/phase_execution.md` — **Two-Pass Contract Gate** prefers native source/schema/tests/examples, requires code-contract compilation, and allows behavior to remain unimplemented. | **Pass A: Contract**; **Contract review**. | **Keep** — these mechanics are valuable procedural detail permitted by the specification. | `skills/phase_execution.md` | A code-contract Pass A compiles its source/test surface, reports intentionally failing/disabled behavior tests, and stops before implementation. |
| `CORE-PHASE-06` | `../../../../../skills/phase_execution.md` — **Implementation Discipline** permits test plumbing changes but requires review before weakening approved scenarios/outcomes/failures. | **Pass B: Implementation**. | **Keep** — preserve behavioral meaning without freezing incidental test source. | `skills/phase_execution.md` | Pass B may change fixtures/helpers while retaining expectations; all approved expectations are enabled and pass before completion; semantic weakening reopens review. |
| `CORE-PHASE-07` | `../../../../../skills/phase_execution.md` repeatedly rejects interfaces/builders/adapters created only for workflow formality. | **Simple projects should stay simple**; **Pass A: Contract**. | **Keep** — Bonsai gates do not prescribe implementation architecture. | `skills/phase_execution.md` | Contract-first work can use a concrete type or native schema with no process-induced abstraction. |
| `CORE-PHASE-08` | `../../../../../skills/phase_execution.md` — **Fresh Session Continuation** uses the v1 implementation prompt and explicit project key. | **Session Boundaries**. | **Adapt** — retain peer continuation choices and recorded state, but use `../../../../../start.md` and add project identity only when needed. | `skills/phase_execution.md`; `skills/menu.md` | Plan/contract approval stops before the new pass; current/fresh choices are peers; fresh startup cannot bypass readiness. |

### Final truth, dry runs, handoff, and agent context

| Evidence ID | Source evidence | Specification rule | Classification and rationale | Owning contract | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `CORE-TRUTH-01` | `.bonsai/implementation_prompt.md` — **Final-Truth Reconciliation**; `../../../../../skills/final_truth_update.md` — **Human-Owned Final-Truth Documents** and **Impact Classification**. | **Artifact Ownership**; **Project Final Truth**; **Final-truth gate**. | **Keep** — human-owned durable meaning stays distinct from agent-owned execution memory and uses `None` / `Clarification` / `Revision`. | `skills/final_truth_update.md` | Each gate and completion classifies impact; affected human-owned documents are explicit; execution-memory edits alone remain `None`. |
| `CORE-TRUTH-02` | `../../../../../skills/final_truth_update.md` — **Approval Behavior** and **Forbidden Changes** require authorization and stop on revision. | **Human-owned artifacts**; **Final-truth gate**. | **Keep** — clarification cannot hide changed intent and revision cannot proceed silently. | `skills/final_truth_update.md`; `skills/menu.md` | Wording-only clarification and behavior-changing revision reach distinct gates; no changed behavior executes before revision approval. |
| `CORE-TRUTH-03` | `../../../../../skills/final_truth_update.md` — **Return-to-Invoking-Gate Rule** and **Execution-Memory Consequences** recompute plan/state/readiness. | **Subordinate workflows**; **Agent Execution Memory**. | **Keep** — final-truth handling is subordinate unless it creates a new required gate. | `skills/final_truth_update.md` | Clarification from startup/handoff/contract returns to that refreshed gate; an invalidated plan produces the new planning gate instead. |
| `CORE-TRUTH-04` | `../../../../../skills/final_truth_update.md` treats framework skills as non-project truth; v1 has no explicit framework-specification distinction. | **Specification Authority**; **File Maintenance Discipline — Bonsai specification**. | **Adapt** — project final-truth workflow must recognize `../../../../../specification.md` as human-owned Bonsai framework truth when Bonsai itself is the project, without treating it as routine project requirements. | `skills/final_truth_update.md` | A behavior change to Bonsai routes to explicit specification review; framework prompt/skill edits cannot silently become authority. |
| `CORE-DRY-01` | `../../../../../skills/dry_run.md` — **Purpose**, **Rules**, and **Stop Conditions** make previews optional, compact, read-only, and subordinate to approved gates. | **Dry Runs**; **See more options**. | **Keep** — preserve the risk-reduction preview without making it routine. | `skills/dry_run.md`; `skills/menu.md` | Normal gates omit Dry Run; explicit request or accepted unusual-risk suggestion performs no writes and returns for approval. |
| `CORE-DRY-02` | `../../../../../skills/dry_run.md` — **Required Inputs**, **Procedure**, and **Output** require an approved basis, touch points, result, checks, concerns, and final-truth impact. | **Dry Runs**; **Final-truth gate**. | **Keep** — these fields make the preview decision-useful without becoming design authority. | `skills/dry_run.md` | Preview names its approved basis and uncertainties; absent basis returns to planning/review rather than inventing scope. |
| `CORE-DRY-03` | `../../../../../skills/dry_run.md` — **Approval Handling** stores a compact baseline and removes it after completion, abandonment, or redirection. | **`agent_state.md`**; **File Maintenance Discipline — Agent execution memory**. | **Adapt** — retain the lifecycle under `agent_state.md`; only a human-approved preview creates the baseline. | `skills/dry_run.md`; `skills/handoff.md` | Approved baseline is resume-critical and compact; it is removed when the step completes or changes; actual deviations are reported. |
| `CORE-DRY-04` | `../../../../../skills/dry_run.md` allows preview of a `Revision` but forbids implementation before final-truth approval. | **Final-truth gate**; **Dry Runs**. | **Keep** — read-only preview does not bypass durable-meaning approval. | `skills/dry_run.md`; `skills/final_truth_update.md` | Revision preview offers final-truth drafting rather than proceed; no implementation write occurs. |
| `CORE-HANDOFF-01` | `../../../../../skills/handoff.md` — **Handoff Procedure**; `.bonsai/implementation_prompt.md` — **Completion Reporting** require reconciliation before completion. | **Implementation Workflow**; **Agent Execution Memory**; **Session Boundaries**. | **Adapt** — preserve the completion boundary with v2 names and triggered workflow ownership. | `skills/handoff.md` | A step cannot be reported complete until checks, final-truth impact, state/plan consequences, exact next step, and readiness are reconciled. |
| `CORE-HANDOFF-02` | `../../../../../skills/handoff.md` — **Handoff Procedure** and **Completion Summary** prune stale state and report only actual work/checks. | **`agent_state.md`**; **File Maintenance Discipline — Agent execution memory**. | **Keep** — current resume truth replaces session history. | `skills/handoff.md` | Completed steps/resolved blockers/expired baselines disappear; changed-file and check reports exclude unrelated workspace changes. |
| `CORE-HANDOFF-03` | `../../../../../skills/handoff.md` — **Out-of-Scope Observation Handling** requires count-before-detail and human authorization before persistence. | **Out-of-Scope Observations and `icebox.md`**; **File Maintenance Discipline — Icebox**. | **Keep** — `icebox.md` remains human-owned triage, not an automatic backlog. | `skills/handoff.md`; `skills/menu.md` | Handoff reports only a count until review; rejection leaves no durable entry; preservation writes one item but does not authorize implementation. |
| `CORE-HANDOFF-04` | `../../../../../skills/handoff.md` — **Gate Return Rule** protects the handoff after observation/final-truth/correction workflows. | **Subordinate workflows**. | **Keep** — parent handoff survives subordinate work unless superseded by a new mandatory gate. | `skills/handoff.md`; `skills/menu.md` | Observation correction or clarification returns to a refreshed handoff; a new blocker/review gate replaces it explicitly. |
| `CORE-HANDOFF-05` | `../../../../../skills/handoff.md` — **Handoff Menu**, **Fresh Session Continuation**, and **Canonical Prompt Self-Check** prohibit host-session claims and keep volatile state out of the pointer. | **Session Boundaries**. | **Adapt** — retain peer choices and pointer-only self-check, changing the runtime entry to `../../../../../start.md`. | `skills/handoff.md`; `skills/menu.md` | Ready work offers current/fresh/change/stop; blocked/review work offers no bypass; fresh output contains only the canonical pointer plus project when necessary. |
| `CORE-HANDOFF-06` | `../../../../../skills/handoff.md` — **Stop Conditions** requires an explicit human choice before the next step begins. | **Session Boundaries**; **Human Gates and Menus**. | **Keep** — handoff is an authorization boundary, not merely a report. | `skills/handoff.md` | Completion stops at its applicable gate; only current-session continuation starts the recorded executable step. |
| `CORE-CONTEXT-01` | `.bonsai/skills/tooling_memory.md` — **When to Load** and **Lazy-Load Rule** avoid routine startup loading. | **Agent Context**; **Lazy Loading**. | **Adapt** — preserve facet-triggered loading while broadening beyond tooling. | `skills/agent_context.md` | Unrelated startup does not load agent context; tooling/source/map operational work loads only relevant scopes. |
| `CORE-CONTEXT-02` | `.bonsai/skills/tooling_memory.md` — **What Qualifies for Preservation**, **Do Not Preserve**, and **Completion** require durable, reusable, actionable, evidence-based, operational facts and reject transient blockers, history, and secrets. | **Durable discovery should become agent memory**; **Agent Context**; **File Maintenance Discipline — Agent context**. | **Adapt** — retain the mature qualification test; specification wording `sufficiently supported` is satisfied by evidence-based facts likely to matter again, while the active blocker remains in execution state. | `skills/agent_context.md` | A qualifying working rule is stored; transient/speculative/history/secret examples are rejected; an unresolved blocker remains in `agent_state.md`. |
| `CORE-CONTEXT-03` | `.bonsai/skills/tooling_memory.md` — **Maintenance Rules** and **Applying Existing Memory** create only on first fact, consolidate, prune, and prefer current evidence. | **Agent-owned artifacts**; **Agent Context**. | **Keep** — proactive current-truth maintenance remains agent-owned and gate-free. | `skills/agent_context.md` | No empty context file is created; duplicate/stale rules are consolidated or corrected at the narrowest reusable scope. |
| `CORE-CONTEXT-04` | `.bonsai/skills/tooling_memory.md` — **Relationship to Developer Context** and **Authority Boundary** prohibit overriding human context or authorizing environmental/project changes. | **Developer Context**; **Agent Context**; **Context Layering**. | **Keep** — operational memory informs execution but grants no new authority. | `skills/agent_context.md` | Context conflict is surfaced with more-specific scope semantics; no install/config/dependency/scope/credential action is inferred. |
| `CORE-CONTEXT-05` | `.bonsai/skills/tooling_memory.md` owns only repository-local `.bonsai/tooling.md`. | **Agent Context**; **Agent-context scopes**. | **Drop** — the tooling-only filename and single repository scope are obsolete in v2. Qualifying content moves conceptually to scoped `agent_context.md`; no compatibility copy is retained. | `skills/agent_context.md` | Developer-, repository-, and project-level rules layer broad-to-specific; active project is stored in none; no `tooling.md` compatibility artifact is required. |
| `CORE-CONTEXT-06` | `.bonsai/skills/tooling_memory.md` covers tooling/environment facts but not source locations or map-selection rules. | **Agent Context**; **Agent-context scopes**. | **Missing** — v2 operational context additionally owns stable source locations and useful map-selection knowledge at the narrowest reusable scope. | `skills/agent_context.md` | Cross-repository source location persists at developer scope when reusable; repository build rule stays local; project-only useful maps stay project-scoped. |


## Artifact: `start.md`

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
- resolve Bonsai Home by preferring a valid `BONSAI_HOME`, otherwise using a valid embedded standard, otherwise
  stopping for human configuration;
- resolve the active project for the current session: explicit project first, then `projects/main`, then the only
  enumerated project, then human selection when several exist, or project creation/design when none exists;
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
- create project memory or durable design merely because no project exists.

### Reads

Only the local anchor, `BONSAI_HOME` when defined, standard-validity markers, and project-directory names required
to resolve identity. Deterministic lookup and enumeration should use host tools when available.

### Writes

None during normal startup.

### Delegates to

```text
<bonsai-home>/prompts/implementation.md
```

### Human gates

Only when identity cannot be resolved safely, such as ambiguous project selection, an explicit unavailable project,
an unavailable Bonsai Home, or a repository with no project memory.

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

## Artifact: `prompts/implementation.md`

**Classification:** Adapt from `.bonsai/implementation_prompt.md`

### Role

Stable implementation kernel and router after environment identity has already been resolved.

### Loaded when

Immediately after `../../../../../start.md` establishes Bonsai Home, repository home, active project, and any explicit startup request.

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
- own the small in-session Project Management workflow for deterministic listing, session-local switching, and
  project-directory creation without inventing project design;
- route secondary workflows without allowing them to erase their invoking gate;
- enforce exact-next-step focus, scope discipline, and material-deviation stops;
- ensure completion is reconciled through handoff rules before claiming the step complete.

### Must not

- perform bootstrap identity discovery that belongs in `../../../../../start.md`;
- recursively load project memory merely because files exist;
- automatically load all developer context, agent context, maps, or skills;
- invent software-engineering conventions, abstractions, interfaces, test philosophy, or dependency rules;
- treat execution memory, maps, developer context, agent context, or icebox contents as project final truth;
- require a clean Git working tree;
- report unrelated pre-existing changes unless they affect safe execution;
- silently broaden scope.

### Reads

After bootstrap identity is available:

1. read project `agent_state.md` when present;
2. read `agent_plan.md` when present and compare roadmap-level phase, mode, plan, approval, and readiness truth with
   state;
3. read the active phase plan when state names one or when it is required to establish the current planning or
   review gate;
4. load relevant requirements, architecture, deeper final truth, developer context, agent context, maps, or skills
   only when the exact next step, requested workflow, impact classification, or detected inconsistency requires them.

Missing required execution memory and conflicts among loaded project memory become explicit readiness/gate results;
they are not repaired by recursive discovery or guessed from unrelated files.

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
skills/bonsai_home.md
```

Project Management remains an inline kernel responsibility; `skills/menu.md` owns its contextual presentation and
invoking-gate return behavior. It does not have a separate Project Management skill. Create Bonsai Home delegates
to the lazy-loaded `skills/bonsai_home.md` workflow defined by the project/context contract batch.

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

- bootstrap identity resolution moves to `../../../../../start.md`;
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
- in-session project listing, switching, and creation route through the kernel without a dedicated Project
  Management skill;
- Create Bonsai Home loads `skills/bonsai_home.md` only when explicitly requested or contextually selected;
- dirty working tree does not block unrelated approved work;
- final-truth revision stops before substantive implementation.

---

## Artifact: `skills/menu.md`

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
- include only applicable secondary actions such as Manage Projects, Manage Code Maps, Create Bonsai Home, Dry Run,
  diagnostics, or maintenance;
- allow a secondary action to be promoted when directly relevant;
- preserve host-provided free-form choices rather than manufacturing generic `Other`;
- support subordinate workflows and return to the invoking gate with refreshed choices;
- avoid making parent gates disappear after subordinate actions.

### Must not

- become a fixed junk drawer;
- add every Bonsai feature to every menu;
- manufacture a generic `Other` when the host already provides one;
- put a normally secondary action in the primary menu unless current context makes it directly relevant;
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

## Artifact: `skills/phase_execution.md`

**Classification:** Keep + Adapt

### Role

Govern phase planning, execution-mode selection, phase-plan lifecycle, and contract-first two-pass gates.

### Loaded when

- Phase 1 plan must be created or corrected;
- later phase planning is genuinely warranted;
- phase execution mode is unresolved;
- an exact implementation step is governed by an active phase plan or approved phase contract;
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
- fresh-session prompt is the v2 `../../../../../start.md` pointer rather than the old implementation-prompt path.

### Validation cases

- new project requires Phase 1 plan;
- trivial later phase proceeds without unnecessary phase plan;
- public API phase selects two-pass;
- internally large but non-contract phase remains single-pass;
- Pass A source compiles while behavior remains unimplemented;
- test plumbing changes without semantic contract change do not cause false review gate;
- semantic contract weakening does require review.

---

## Artifact: `skills/final_truth_update.md`

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

When Bonsai itself is being changed, read `../../../../../specification.md` as the human-owned framework truth governing standard
behavior; do not demote it to an implementation artifact or treat it as ordinary execution memory.

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

Use v2 ownership/naming and layered project truth. Do not treat the active Bonsai `../../../../../specification.md` as ordinary
project final truth; changes to that specification remain explicit human-owned framework changes regardless of its
current staging, Bonsai Home, or embedded placement.

### Validation cases

- wording precision with unchanged intent;
- actual architecture revision;
- clarification invoked from handoff returns to handoff;
- approved revision invalidates active phase plan and readiness is recomputed.

---

## Artifact: `skills/dry_run.md`

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
- create that baseline only after the human approves the preview;
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

## Artifact: `skills/handoff.md`

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

Project identity is needed when omitting it would not deterministically resume the same project, such as a
repository with several named projects and no `projects/main`. It is not needed for the conventional deterministic
`projects/main` case.

### Validation cases

- ordinary completed step;
- completed step with stale blocker removed;
- observation review then return to handoff;
- clarification during handoff then return;
- fresh-session choice produces pointer only, without volatile state in the prompt;
- completed phase updates both roadmap and state.

---

## Artifact: `skills/agent_context.md`

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
- layer developer-level, repository-level, then project-level context, with the more specific statement winning
  when scopes conflict;
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

## Human Review Focus

- Approve the bootstrap/kernel boundary: `start.md` resolves identity only; `prompts/implementation.md` determines
  execution state and routing.
- Approve dropping v1.4's unconditional startup loading of maps and developer context in favor of workflow/facet
  triggers.
- Approve `menu.md` as presentation ownership only; invoking workflows retain gate meaning and durable writes.
- Approve adapting tooling memory into layered `agent_context.md` without a permanent `tooling.md` compatibility
  artifact.
- Confirm that the 46 evidence records and eight complete artifact contracts are sufficient implementation authority
  for later phases after the remaining Phase 1 batches are reviewed.
