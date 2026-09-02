# Artifact Contracts — Validation and Self-Hosting Promotion

**Project:** `bonsai-dev`  
**Status:** Phase 1 promotion/validation archaeology complete; contract batch approved

## Purpose

Define the durable behavior required to validate artifact-producing Bonsai workflows, keep the staged v2
distribution independently shippable, construct and verify a complete replacement runtime, preserve repository
memory, provide a tested rollback point, promote without a half-installed `.bonsai`, prove the result in a genuinely
fresh session, and collapse the repository back to one Bonsai tree.

This contract does not choose a helper-script package or claim that one directory-swap command is portable across
all hosts. It defines the observable invariants any Phase 5 implementation must satisfy.

No v1.4 promotion implementation exists to preserve. Most promotion behavior is therefore **Missing** relative to
the archaeological source and required directly by approved requirements, architecture, and the v2 specification.

---

## Archaeological Evidence and Classification

### Distribution and test boundaries

| Evidence | Source evidence | Approved rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `PROMO-VAL-01` | No v1.4 validation harness; current `bonsai/` contains only candidate `../../../../../../README.md` and `../../../../../specification.md`. | REQ-2, REQ-3; Architecture **Staging Principle** and **Distribution Purity** | Missing | Phase 5 validation must treat the entire staged tree as candidate distribution input without exclusion filters. | A purity check fails for any generated log, test result, candidate, backup, or repository memory under `bonsai/`. |
| `PROMO-VAL-02` | No v1.4 boundary enforcement. | REQ-4; Architecture **Golden Artifact Model** | Missing | Durable fixtures/expected results belong under `../../../../../../tests`; generated runs belong under ignored `../../../../../../build`. | Every scenario writes to an isolated `build/bonsai-tests/<scenario>/`; reruns are deterministic and do not mutate durable inputs. |
| `PROMO-VAL-03` | No v1.4 artifact-contract validator. | REQ-6, REQ-7; specification **File Maintenance Discipline** | Missing | Candidate validation must check distribution references and required artifact identities against approved contracts. | Missing files, stale paths, duplicate compatibility identities, and references outside the candidate standard fail validation. |
| `PROMO-VAL-04` | Existing Web UI and mapping workflows produce Markdown/artifact trees but have no repeatable output tests. | REQ-4, REQ-16; Architecture **Golden Artifact Model** | Missing | Use semantic assertions where behavior matters and golden output only where exact stable structure is contractual. | Formatting-only drift does not fail semantic scenarios; exact archive/tree contracts fail on structural drift. |
| `PROMO-VAL-05` | No v1.4 topology suite. | REQ-16; specification **Bonsai 2.0 Validation Cases** | Missing | Validation must cover Embedded, Bonsai Home, multi-project, multi-repository, external-source, and greenfield operation. Multi-repository proof uses real Barcache and Tickerview external sources plus controlled consuming-project fixtures; Investment App is future out-of-band validation, not a Phase 5 input. | All six topologies have named, isolated, repeatable scenarios; actual Barcache and Tickerview maps are generated, rediscovered, and reused from an isolated/test Bonsai Home without modifying either source repository or its legacy Bonsai state. |
| `PROMO-VAL-06` | `../../../../../../.gitignore` ignores `../../../../../../build` but not `../../../../../../.bonsai-backups`. | REQ-4, REQ-11; Architecture **Local rollback archive** | Missing | Before live promotion, disposable generated output and local backups must be excluded from source control without placing ignores inside staged distribution. | Preflight verifies `../../../../../../build` and `../../../../../../.bonsai-backups` are ignored; archives/results are not staged for commit. |
| `PROMO-VAL-07` | No destructive-test isolation exists. | REQ-12; Architecture **Candidate construction** | Missing | Candidate, failure, rollback, and conversion tests operate only on copied fixture trees under `../../../../../../build`. | Validation refuses a fixture root resolving to live `.bonsai`, live `bonsai/`, repository root, or another broad path. |

### Candidate construction and preservation

| Evidence | Source evidence | Approved rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `PROMO-CAND-01` | v1.4 has no candidate builder. | REQ-12; Architecture **Candidate construction** | Missing | Build the complete `.bonsai` candidate in disposable storage before touching live runtime. | Candidate assembly leaves live `.bonsai` byte-for-byte unchanged. |
| `PROMO-CAND-02` | Current live `.bonsai` mixes standard files with repository context/projects. | REQ-13; Architecture **Preservation boundary** | Adapt | Classify live paths by ownership; take v2 standard only from validated `bonsai/`, never by merging the old tree. | Candidate contains no legacy standard file merely because it existed under live `.bonsai`. |
| `PROMO-CAND-03` | `../../..` contains human truth/contracts plus v1.4 execution memory. | REQ-1, REQ-13; Architecture **Bootstrap Execution Memory** | Adapt | Preserve human/project truth and semantically convert only current useful execution memory to v2 identities. | Candidate retains requirements, architecture, approved contracts, applicable layered truth/icebox/context, and current execution meaning. |
| `PROMO-CAND-04` | `plan.md`, `state.md`, and `plan/plan_phase_<N>.md` are the active v1.4 names. | REQ-1, REQ-9, REQ-13; specification **Agent Execution Memory** | Adapt | Convert to `agent_plan.md`, `agent_state.md`, and `plan/agent_plan_phase_<N>.md`; this is semantic current-truth conversion, not blind rename. | Cross-references, active plan paths, pass/readiness, objective, and exact next step use v2 semantics; no competing v1 names remain. |
| `PROMO-CAND-05` | v1.4 execution files contain bootstrap notes and old runtime instructions that become stale after promotion. | specification **Clean Rebuild Objective** | Drop | Remove obsolete bootstrap/current-runtime instructions during conversion while preserving current roadmap and resume truth. | Converted memory contains no instruction to use v1.4, stage v2 as future work, or start with `implementation_prompt.md`. |
| `PROMO-CAND-06` | `../../../../../developer_context.md` is human-owned repository context and ignored by Git. | REQ-13; specification **Repository-local Bonsai memory** and **Developer Context** | Keep | Preserve repository developer context verbatim when present; do not synthesize or normalize it during promotion. | Candidate retains the file content/ownership and does not place it in the shared standard. |
| `PROMO-CAND-07` | v1 `.bonsai/tooling.md` may exist; approved v2 contracts retire that identity in favor of scoped `agent_context.md`. | REQ-13; specification **Agent Context**; approved core/project contracts | Adapt | Convert qualifying repository tooling memory to repository `agent_context.md`; merge only by current meaning and never keep both identities. | Fixture with tooling memory yields one non-secret v2 repository agent-context file and no `tooling.md`. |
| `PROMO-CAND-08` | `.bonsai/maps/` currently contains only v1.4 mapping-standard/control artifacts; no generated repository code map exists. | REQ-10, REQ-13; approved mapping contract | Drop + conditional Adapt | Replace v1 map control files with v2 standard; preserve only separately identifiable runtime source-map data when present and validated, converting placement/identity as required. | Current candidate carries no v1 `map_prompt.md`, `map_system.md`, `repo_session.md`, or map templates under runtime map data. |
| `PROMO-CAND-09` | `../../../../task-tracker` is the repository's checked-in canonical Getting Started project, but its current execution memory uses v1.4 identities. | REQ-9, REQ-13, REQ-17; Architecture **Canonical Embedded Getting Started Project** | Adapt + Keep; disposition gate | Preserve the project in place as the single authoritative shipped Embedded example. Human-approved source preparation keeps its requirements/architecture, adapts its guide, and replaces—not renames—the legacy plan/state with a fresh v2 Getting Started checkpoint. | Candidate construction blocks until source preparation and isolated copied-project validation pass; the candidate preserves `../../../../task-tracker` with `../../../../../../README.md`, `requirements.md`, `architecture.md`, `agent_plan.md`, and `agent_state.md`, and no v1 execution identities. |
| `PROMO-CAND-10` | Future repository-owned paths may exist beyond today's inventory. | REQ-12, REQ-13 | Missing | Preflight uses an explicit classification manifest/report for every live top-level/local-memory path and stops on unknowns. | An extra project/context/map path cannot be silently dropped or blindly copied. |

### Backup, swap, and rollback

| Evidence | Source evidence | Approved rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `PROMO-BACKUP-01` | No v1.4 backup workflow. | REQ-11; Architecture **Local rollback archive** | Missing | Create a timestamped local archive of pre-promotion `.bonsai` only after candidate validation and immediately before live mutation. | Archive name is collision-safe and captures a restorable `.bonsai` root. |
| `PROMO-BACKUP-02` | No archive verification. | REQ-12 | Missing | Validate archive readability, safe paths, inventory, and content equivalence before promotion continues. | Corrupt, incomplete, path-unsafe, or colliding archive fails preflight and leaves live runtime untouched. |
| `PROMO-BACKUP-03` | No rollback rehearsal. | REQ-12; Architecture **Swap** | Missing | Isolated validation must prove restoration from the produced archive, not merely archive creation. | A copied fixture is restored to the pre-promotion inventory/content and starts with its pre-promotion state. |
| `PROMO-BACKUP-04` | No v1.4 rule for archive lifetime. | REQ-11, REQ-14 | Missing | Keep the archive outside both Bonsai trees through promotion/proof; do not automatically delete the recovery point during finalization. | Successful cleanup removes staging only, not the rollback archive. |
| `PROMO-SWAP-01` | No v1.4 live promotion operation. | REQ-12; Architecture **Swap** | Missing | Live mutation begins only with validated staged tree, validated complete candidate, verified archive, approved exact next step, and clean preflight classifications. | Every missing precondition stops before moving/replacing live `.bonsai`. |
| `PROMO-SWAP-02` | No portable atomic-directory guarantee. | REQ-12 | Missing, packaging unresolved | The implementation must choose the safest host-supported same-filesystem replacement and minimize incomplete exposure; exact command/script remains Phase 5 host work. | Failure injection at each mutation boundary proves live candidate or recoverable old runtime, never an accepted partial merge. |
| `PROMO-SWAP-03` | No v1.4 rollback behavior. | REQ-12 | Missing | Preserve a recoverable old live directory until candidate placement verifies; restore it automatically when safe or stop with exact archive/quarantine recovery instructions. | Simulated candidate-placement and post-placement verification failures retain both rollback assets and an unambiguous recovery path. |
| `PROMO-SWAP-04` | Manual copying is the only implied fallback in old guidance. | Constraint: no manual copying; Architecture **Guardrails** | Drop | Promotion is one controlled workflow/state machine, not a human sequence of ad hoc copies. | The normal release path builds, validates, archives, swaps, and verifies without manual file selection. |
| `PROMO-SWAP-05` | No v1.4 post-swap state. | REQ-14; Architecture **Fresh-Session Self-Hosting Proof** | Missing | Candidate `agent_state.md` must already record `Promoted, Unproven`, `Ready to execute`, and the fresh-session proof as its objective/next step; rollback archive retains the pre-promotion state. | First v2 startup sees proof as the exact next step, not stale promotion construction work or an invented readiness value. |
| `PROMO-SWAP-06` | No v1.4 secret/scope safeguard. | Developer Context; destructive-action rules | Missing | Promotion reports exact roots and never archives/writes outside resolved repository targets; it does not print context contents. | Ambiguous/broad roots, symlink/path escape, or unresolved target identity block destructive action. |

### Fresh-session proof and final collapse

| Evidence | Source evidence | Approved rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `PROMO-PROOF-01` | v1.4 fresh prompt uses `implementation_prompt.md`. | REQ-14; specification **Startup Bootstrap** | Adapt + Drop | Acceptance must start a genuinely fresh session with only `Read .bonsai/start.md and follow its instructions.`; old entry is not fallback. | Proof records that v2 `start.md` and v2 implementation router were used. |
| `PROMO-PROOF-02` | No v1.4 v2-memory startup. | REQ-14 | Missing | Acceptance must resolve the newly promoted repository `.bonsai` as the Embedded Bonsai Home, then resolve repository/project identity and converted memory. External-home preference is tested separately and cannot satisfy self-hosting proof. | Startup evidence identifies promoted `.bonsai` as Bonsai Home and reports `bonsai-dev`, correct phase/pass/readiness, and the exact post-promotion next step. |
| `PROMO-PROOF-03` | Current chat has archaeological context unavailable to a new session. | REQ-7, REQ-14; specification **Session Boundaries** | Missing | Proof cannot rely on prior chat, injected handoff packet, or v1 prompt. | A fresh session succeeds using durable promoted files and canonical pointer only. |
| `PROMO-PROOF-04` | No operational self-hosting acceptance. | REQ-14 | Missing | After startup gate, the human authorizes one bounded Bonsai-development action that routes/executes under v2 semantics. | Proof is not satisfied by file existence or startup prose alone. |
| `PROMO-PROOF-05` | No v1.4 failure disposition. | REQ-12, REQ-14 | Missing | Failed proof leaves `bonsai/` and archive intact and routes to rollback or bounded repair; it cannot declare promotion complete. | Failure state identifies current live runtime, recovery assets, and one exact recovery decision. |
| `PROMO-PROOF-06` | No staging-finalization workflow. | REQ-14, REQ-15 | Missing | Successful proof updates execution memory and stops at a separate explicit staging-removal action. | `bonsai/` still exists immediately after proof and is removed only after proof success and human continuation. |
| `PROMO-PROOF-07` | Bootstrap tree currently has two standards by design. | REQ-15; Architecture **Stable Repository Model** | Missing | Final validation requires `../../../../..` to be the single shipped/self-hosting standard and source tree. | No sibling `bonsai/`, no duplicate v1 execution names, and no runtime dependence on build output remain. |

### Clean rebuild and completion

| Evidence | Source evidence | Approved rule | Class | Rationale / owner | Validation obligation |
| --- | --- | --- | --- | --- | --- |
| `PROMO-FINAL-01` | Bootstrap plans/state contain temporary staging truth. | REQ-15; specification **Clean Rebuild Objective** | Adapt | Post-proof memory keeps current v2 execution truth and prunes completed bootstrap mechanics. | Fresh clone needs only `../../../../../start.md` plus durable project/source memory, not promotion history. |
| `PROMO-FINAL-02` | Human-owned requirements/architecture/contracts document the self-hosting lifecycle. | REQ-6, REQ-15 | Keep | Preserve durable design and archaeological citations; do not globally rewrite human truth merely because paths changed. | Final-truth updates occur only if current wording becomes false, through explicit clarification/revision handling. |
| `PROMO-FINAL-03` | Exact helper packaging is absent. | specification **Optional Helper Scripts** and **Design Boundaries Still Being Validated** | Missing, explicitly unresolved | Phase 5 may implement the smallest project-appropriate driver, but conceptual correctness cannot depend on its name or shell. | Contract scenarios can exercise behavior independently of one helper command identity. |
| `PROMO-FINAL-04` | Migration from arbitrary v1 projects is not implemented. | REQ-9; specification **Migration** | Drop | Only the explicitly approved self-hosting conversion is in scope; no general v1 compatibility/migration layer survives. | Candidate contains no generic v1 loader, aliases, or dual execution-memory format. |

---

## Contract: Staged Distribution and Validation Boundary

### Role

Keep `repo/bonsai/` equal to the complete candidate Bonsai v2 standard and validate artifact-producing workflows
without contaminating it or the live runtime.

### Trigger

Phase 5 validation preparation, every candidate-standard validation, and promotion preflight.

### Inputs / Reads

- approved specification and artifact contracts;
- staged `repo/bonsai/` as a whole tree;
- durable fixtures under `tests/fixtures/`;
- durable expected artifacts under `tests/expected/` when exact comparison is justified;
- copied source/project/runtime fixtures for the six required topologies;
- read-only real Barcache source at `/mnt/c/mine/dev/ca/barcache` (`C:\mine\dev\ca\barcache`);
- read-only real Tickerview source at `/mnt/c/mine/dev/ca/tickerview` (`C:\mine\dev\ca\tickerview`).

### Responsibilities

- validate that every staged file is intended distribution content;
- validate required artifact presence, canonical identities, internal references, and ownership boundaries;
- execute scenarios in isolated per-run output directories;
- support semantic assertions, tree/inventory assertions, and golden comparisons according to contract stability;
- make cleanup/re-run deterministic;
- validate Embedded, Bonsai Home, multi-project, multi-repository, external-source, and greenfield behavior;
- generate distinct Barcache and Tickerview maps from actual source into an isolated/test Bonsai Home, then
  rediscover and reuse them through normal v2 routing and controlled consuming-project fixtures;
- prove map lifecycle operations affect only generated map-owned artifacts and preserve all external-repository
  content, including unrelated or legacy Bonsai state;
- keep destructive promotion/rollback tests entirely inside disposable fixture roots;
- verify `../../../../../../build` and `../../../../../../.bonsai-backups` are ignored before generating those outputs in live-repository work.

### Must not

- write generated output, fixtures, local context, project memory, candidates, backups, or logs under `bonsai/`;
- mutate live `.bonsai` during ordinary validation;
- treat golden files as authority over requirements/specification/contracts;
- require exact-text goldens when semantic behavior is the contract;
- migrate, modify, delete, or activate repository-local Bonsai state found in Barcache or Tickerview;
- create, synthesize, stub, simulate, name, or represent a controlled fixture as Investment App for Phase 5;
- resolve destructive test paths from broad roots, unvalidated variables, or ambiguous symlinks;
- accept a candidate merely because files exist.

### Writes

Only isolated generated output such as:

```text
build/bonsai-tests/<scenario>/
build/bonsai-promotion/<run>/
```

Durable fixture/golden changes are normal source changes and require the applicable implementation scope; test runs
do not rewrite them.

### Delegates to

Candidate construction and isolated promotion/rollback validators defined below.

### Human gates

- approval of durable expected artifacts when their exact content defines reviewed behavior;
- acceptance of any required check that cannot pass is a material deviation;
- no live-promotion authority is implied by validation success.

### Validation cases

- generated file injected under `bonsai/` fails purity;
- missing/dangling/stale standard reference fails integrity;
- each required topology runs from isolated fixtures;
- Barcache and Tickerview produce distinct reusable map identities in the isolated/test map store, normal v2 routing
  rediscovers/reuses them through a controlled consuming-project fixture, and pre/post inventories prove both source
  repositories remain unchanged;
- repeated scenario run produces equivalent results;
- destructive fixture accidentally aimed at live/broad path is refused.

---

## Contract: Promotion Candidate Construction

### Role

Construct and validate a complete candidate `repo/.bonsai` in disposable storage without mutating the live v1.4
runtime.

### Trigger

Only after staged v2 validation passes and project state authorizes Phase 5 candidate construction.

### Inputs / Reads

- validated complete staged standard at `repo/bonsai/`;
- explicit staged-standard artifact inventory;
- read-only inventory of live `repo/.bonsai/` classified as old standard, repository memory, convertible memory,
  runtime map data, explicitly excluded material, or unknown;
- approved preservation and conversion rules in this contract;
- prepared canonical `../../../../task-tracker` with validated v2-only execution memory;
- current `bonsai-dev` execution state at candidate-build time.

### Responsibilities

1. create an empty disposable candidate root;
2. copy the staged standard without filtering into `candidate/.bonsai/`;
3. inject only classified repository-owned memory;
4. semantically convert current useful `bonsai-dev` execution memory to v2 identities;
5. convert qualifying repository tooling memory to `agent_context.md` when present;
6. preserve human-owned developer context verbatim;
7. preserve validated runtime source-map data only when it is distinguishable from v1 mapping-standard files;
8. preserve the prepared canonical Task Tracker project as classified repository-shipped project memory;
9. reject unknown live paths until their disposition is approved;
10. validate candidate layout, references, ownership, memory completeness, source-control boundaries, and startup
   semantics;
11. emit a concise candidate inventory/classification report outside staged distribution.

### Must not

- merge old `.bonsai` wholesale;
- mutate live `.bonsai`;
- place repository memory in the shared standard portion;
- preserve obsolete v1 control files, aliases, or dual execution-memory names;
- bulk rename stale execution history;
- rewrite human-owned truth to modernize archaeological citations;
- relocate, duplicate, silently discard, or preserve unprepared legacy execution state for `task-tracker`;
- proceed with any unclassified live path.

### Writes

```text
build/bonsai-promotion/<run>/candidate/.bonsai/
build/bonsai-promotion/<run>/candidate-inventory.*
```

The exact report serialization is implementation detail; its classifications and validation result are required.

### Delegates to

- staged-distribution validator;
- execution-memory semantic conversion;
- candidate startup/layout validator;
- agent-context conversion rules already approved in core/project contracts.

### Human gates

- unclassified live memory;
- in-place `task-tracker` guide/execution-memory adaptation and legacy-state retirement before source mutation;
- any proposed loss or semantic change to human-owned memory;
- any conversion ambiguity that changes current execution meaning.

### Validation cases

- current self-hosting tree;
- developer context present/absent;
- tooling context present and converted;
- unknown project blocks construction;
- optional runtime map data is preserved while v1 map-control artifacts are not;
- the canonical Task Tracker project is preserved after approved in-place preparation, copied for isolated
  validation, and contains no legacy or duplicate execution-memory identity;
- current state/plan/active phase plan convert with correct cross-references;
- candidate contains v2 names only and starts in isolated Embedded mode;
- live-tree inventory/content remains unchanged.

---

## Preservation and Conversion Set

### Preserve into the candidate

| Live material | Candidate treatment |
| --- | --- |
| `../../../requirements.md` and layered requirements | Preserve human-owned truth unchanged |
| `../../../architecture.md` and layered architecture | Preserve human-owned truth unchanged |
| `../../../artifact_contracts` | Preserve approved project design and archaeological evidence |
| `../../../../task-tracker/requirements.md` and `architecture.md` | Preserve canonical example human-owned truth unchanged |
| Prepared `../../../../task-tracker/README.md`, `agent_plan.md`, and `agent_state.md` | Preserve the approved v2 Getting Started guide and fresh v2 execution checkpoint; reject legacy `plan.md` / `state.md` |
| `.bonsai/projects/bonsai-dev/icebox.md`, if present | Preserve human-triaged human-owned memory unchanged |
| `.bonsai/projects/bonsai-dev/agent_context.md`, if present | Preserve current project-scoped agent context |
| `.bonsai/projects/bonsai-dev/plan.md` | Convert current useful roadmap meaning to `agent_plan.md` |
| `.bonsai/projects/bonsai-dev/state.md` | Convert current resume meaning to `agent_state.md` and set the post-promotion proof gate |
| Active/useful `../archive/v2/plan/plan_phase_<N>.md` | Convert to `plan/agent_plan_phase_<N>.md`; prune obsolete completed detail |
| `../../../../../developer_context.md`, if present | Preserve verbatim as repository human-owned context |
| `.bonsai/agent_context.md`, if present | Preserve current repository agent context |
| `.bonsai/tooling.md`, if present | Convert/merge current qualifying meaning into repository `agent_context.md`; remove old identity |
| Separately identifiable runtime source-map data, if present | Preserve/convert under v2 named-source map-store rules after identity validation |

### Replace from the staged standard

All v1.4 distribution files—including root prompts/guides, `skills/`, `templates/`, and mapping control/template
files—are replaced by the validated staged v2 standard. They are not preservation inputs.

### Require preparation or disposition before promotion

| Live material | Required disposition |
| --- | --- |
| `../../../../task-tracker` | Complete the approved in-place v2 preparation and isolated copied-project validation; preserve the canonical path and reject legacy `plan.md` / `state.md` or any duplicate authoritative source |
| Any other project or unknown top-level local path | Explicitly classify as preserve/convert, relocate, or retire before candidate validation can pass |
| Ambiguous `.bonsai/maps/` content | Establish whether it is old standard or runtime map data; do not guess |

This is an exact classification policy rather than a fragile filename-only copy list: known categories have one
treatment, and unknown categories block promotion.

### Execution-memory conversion rules

- preserve current phase status, ordering, execution mode, approval state, objective, blockers, exact next step,
  and success condition;
- change paths/names and metadata to v2 `agent_` identities;
- update execution-memory cross-references, including phase-plan parent/active paths;
- set candidate promotion status to `Promoted, Unproven`, execution readiness to `Ready to execute`, and the
  fresh-session self-hosting proof as the current objective/exact next step;
- keep only active/useful phase details; completed bootstrap history is compressed into roadmap-level outcome;
- remove v1.4 bootstrap notes, stale staging-as-future language, old canonical prompts, and expired dry-run state;
- preserve archaeological v1 path citations in human-owned contracts/architecture when they remain accurate evidence;
- never create both old and new execution-memory filenames.

---

## Contract: Backup and Rollback

### Role

Create and verify an immediate local recovery point before any live runtime mutation and preserve recovery until
the promoted v2 is proven.

### Trigger

After complete candidate validation and immediately before an explicitly authorized live promotion.

### Inputs / Reads

- exact resolved live `repo/.bonsai/`;
- candidate/preflight report;
- local backup root `repo/.bonsai-backups/`.

### Responsibilities

- create a collision-safe timestamped archive conventionally named
  `.bonsai-backups/bonsai-YYYYMMDD-HHMMSS.zip`;
- archive a directly restorable `.bonsai` root;
- reject unsafe archive entry paths;
- verify archive readability, inventory, and content equivalence;
- restore the archive into an isolated fixture and validate the recovered v1.4 startup/state before live swap;
- retain the archive through promotion, fresh proof, and staging cleanup;
- expose the exact archive path without printing context contents.

### Must not

- continue after backup or verification failure;
- overwrite an existing archive;
- place the archive under `.bonsai`, `bonsai`, or `build`;
- treat the archive as source-controlled release history;
- delete the archive automatically at project completion.

### Writes

```text
repo/.bonsai-backups/bonsai-<timestamp>.zip
build/bonsai-promotion/<run>/restore-verification/
```

### Delegates to

Archive creation plus isolated restore verification; exact host tooling is not fixed by this contract.

### Human gates

- live promotion remains a separate destructive action after backup success;
- backup path/restore ambiguity blocks promotion.

### Validation cases

- normal archive/restore;
- filename collision;
- corrupt/incomplete archive;
- unsafe entry path;
- backup permission/failure;
- restored v1.4 state equals the pre-promotion source.

---

## Contract: Live Promotion State Machine

### Role

Replace the running v1.4 `.bonsai` with the fully validated candidate while preventing an accepted half-install and
retaining a clear rollback path.

### Trigger

Only when current project state names live promotion as the approved exact next step and every precondition passes.

### Inputs / Reads

- exact validated candidate root and its inventory/content identity;
- exact live repository `.bonsai` root;
- verified rollback archive path and restore result;
- complete preservation/disposition/preflight report;
- current execution state and the human's exact live-promotion authorization;
- host/filesystem capabilities needed to choose the replacement strategy.

### States and invariants

| State | Required invariant |
| --- | --- |
| Prepared | Staged tree validated; live untouched |
| Candidate Validated | Complete candidate validated outside live tree; live untouched |
| Backup Verified | Restorable archive verified; live untouched |
| Swap Authorized | Human explicitly authorized exact live target/candidate/archive operation |
| Promoted, Unproven | Live `.bonsai` equals candidate; staging and archive retained; candidate state requires fresh proof |
| Proof Failed / Recovery Required | Staging and archive retained; current live identity and exact rollback/repair choice explicit |
| Proven, Cleanup Pending | Fresh-session proof passed; staging still retained until separate cleanup action |
| Complete | Staging removed; `.bonsai` is sole standard/source; archive retained locally |

No state may accept a partially copied hybrid tree as a valid runtime.

### Preconditions

- staged distribution and complete candidate validations pass;
- preservation/disposition report has no unknowns;
- converted execution memory is internally consistent;
- rollback archive and isolated restore validation pass;
- candidate and live roots are exact, non-broad, and safe for the selected host strategy;
- current execution state and human authorization name this promotion.

### Responsibilities

- use the safest host-supported replacement strategy, preferring same-filesystem directory operations where they
  actually provide stronger guarantees;
- retain the old live directory in recoverable quarantine until new placement verifies when the host strategy
  permits;
- verify promoted inventory/content against the validated candidate;
- verify local bootstrap and post-promotion state are readable;
- restore the old directory automatically when safe after a failed placement, or stop with exact verified archive/
  quarantine recovery directions;
- keep staging and archive intact;
- report the resulting live state without claiming self-hosting completion.

### Must not

- delete live `.bonsai` before candidate, backup, and authorization exist;
- perform in-place merge/copy over live standard;
- continue through failed checks or partial operations;
- remove staging during the swap;
- use manual file selection as the normal release path;
- claim atomicity unsupported by the host;
- broaden targets through unresolved variables, globs, symlinks, or repository-root recursion.

### Writes

The exact live `.bonsai` replacement plus host-local quarantine/transaction records outside staged distribution.
Packaging and temporary names are Phase 5 implementation details.

### Delegates to

Candidate verifier, archive/rollback verifier, host-specific replacement implementation, and promoted-tree verifier.

### Human gates

- explicit authorization immediately before live replacement;
- any changed precondition invalidates prior authorization;
- failed promotion requires a concrete rollback/repair decision when automatic restoration is not safe.

### Validation cases

- success path;
- failure before live mutation;
- failure moving old live aside;
- failure placing candidate;
- failure verifying new live tree;
- automatic restoration where safe;
- exact archive recovery when restoration is not automatic;
- no accepted hybrid/partial tree at any boundary.

---

## Contract: Fresh-Session Self-Hosting Proof and Finalization

### Role

Prove that promoted Bonsai v2 can independently resume and continue the project that created it, then remove the
temporary sibling standard only after that proof.

### Trigger

Live candidate verification succeeds and state is `Promoted, Unproven`.

### Inputs / Reads

- promoted repository `../../../../../start.md` and v2 standard;
- converted `../../../agent_plan.md`, `agent_state.md`, and active phase plan;
- applicable repository/project context;
- canonical fresh-session prompt only.

### Responsibilities

1. require the human to start a genuinely new coding-agent session;
2. use exactly:

   ```text
   Read .bonsai/start.md and follow its instructions.
   ```

3. run in an acceptance environment with no valid external `BONSAI_HOME`, resolve the newly promoted repository
   `.bonsai` as the Embedded Bonsai Home, and resolve repository home and `bonsai-dev` correctly;
4. load v2 agent execution memory and report correct phase/pass/readiness/next step;
5. prove no v1 prompt/control fallback was used;
6. after its normal gate, execute or route one human-authorized bounded Bonsai-development action under v2;
7. record proof success in v2 execution memory;
8. stop at a separate staging-removal action;
9. after explicit continuation, remove `repo/bonsai/` and verify `../../../../..` is the only standard/source tree;
10. reconcile remaining execution memory and any final-truth clarification/revision that is actually required.

### Must not

- reuse the promotion chat as the acceptance session;
- inject a handoff packet beyond the canonical pointer;
- satisfy self-hosting acceptance through an external Bonsai Home instead of the promoted repository `.bonsai`;
- load v1.4 implementation files as silent fallback;
- declare success from file presence or startup output alone;
- delete staging or archive before proof;
- remove staging in the same destructive action as live promotion;
- globally rewrite historical final-truth citations without an approved impact.

### Writes

- current v2 `agent_state.md`/roadmap updates needed to record proof and cleanup state;
- removal of temporary `repo/bonsai/` only after proof and explicit continuation;
- no deletion of the local rollback archive.

### Delegates to

Normal v2 bootstrap, implementation router, handoff, and final-truth reconciliation when applicable.

### Human gates

- human starts the fresh session;
- normal v2 startup gate;
- authorization of one bounded follow-up action;
- failed proof recovery decision;
- separate staging-removal continuation;
- any final-truth clarification/revision exposed by completed promotion.

### Validation cases

- acceptance resolves promoted Embedded `.bonsai` with no valid external `BONSAI_HOME`;
- a separate topology fixture validates external `BONSAI_HOME` preference without being counted as self-hosting proof;
- correct `bonsai-dev` resume from v2 names;
- no prior-chat dependency;
- no v1 fallback;
- bounded v2 action succeeds;
- failed proof retains staging/archive and yields recovery state;
- successful proof retains staging until cleanup gate;
- cleanup yields one `.bonsai` standard/source tree.

---

## Post-Promotion Repository Invariant

After proof and cleanup:

```text
repo/.bonsai/
```

is simultaneously the shipped Bonsai standard, the source contributors modify, the Embedded runtime for
self-hosting, and the location of repository/project memory. There is no sibling `repo/bonsai/` source twin, no
v1 standard/control artifact, no duplicate v1/v2 execution-memory format, and no dependency on disposable build
output.

The local rollback archive may remain under ignored `../../../../../../.bonsai-backups`. Disposable test/promotion output may remain
under ignored `../../../../../../build` until normal cleanup, but neither is runtime authority.

---

## Cross-Contract Validation Matrix

| Scenario | Required proof |
| --- | --- |
| Staged distribution purity | Whole-tree allow/contract check; no generated/local memory |
| Artifact reference integrity | Every standard reference resolves to one canonical identity; known v1 stale names absent |
| Project-memory synthesis | Semantic ownership/content plus archive/tree structure |
| Map calibration and creation | Optional calibration, source authority, named-source storage, canonical templates |
| Embedded standalone | Local `../../../../../start.md` resolves embedded standard/project simply |
| Bonsai Home | Valid home preferred while repository-local project/context remains local |
| Multi-project repository | Deterministic listing/selection; concurrent session selection remains session-local |
| Multi-repository project | Real Barcache and Tickerview sources produce distinct reusable maps in an isolated/test Bonsai Home; a controlled consuming-project fixture rediscovers/selects both without representing Investment App; both source repositories and their legacy Bonsai state remain unchanged |
| External source | Mapping succeeds without source project memory |
| Greenfield | No repeated map pressure |
| Candidate construction | Standard replacement plus exact memory preservation/conversion; live untouched |
| Task-tracker disposition | Canonical in-place project preserved with unchanged human truth, adapted guide, fresh v2 execution memory, and validation from generated copies only |
| Backup/restore | Archive verified and independently restorable before mutation |
| Swap failures | Failure injection leaves verified old or new tree and clear recovery assets |
| Promoted startup | v2 local bootstrap and converted state work in isolation |
| Fresh-session proof | Canonical pointer only, correct resume, one bounded v2 action |
| Final collapse | staging absent; `.bonsai` sole source/standard; archive non-authoritative |

---

## Explicitly Unresolved Implementation Decisions

These are owned, bounded Phase 5 implementation decisions rather than missing product behavior:

1. **Host-specific replacement mechanism:** Choose and failure-test the safest strategy available on the actual
   host/filesystem. The transactional invariants above are fixed; the command sequence is not.
2. **Helper/driver packaging:** Use the smallest project-appropriate executable seam, if any. Do not create a
   permanent framework or make the AI workflow conceptually depend on one script name.
3. **Minimal transaction report format:** Preserve classifications/check results needed for safe execution and
   review, but do not establish a public schema without demonstrated reuse.
4. **Current `task-tracker` source preparation:** The approved disposition preserves the canonical project in place.
   Before promotion implementation can be live-ready, its guide and execution memory must be prepared and validated
   exactly as `PROMO-CAND-09` requires; automatic legacy-state conversion and duplicate fixture authority remain
   prohibited.

No unresolved item authorizes live mutation, compatibility artifacts, failed checks, or manual-copy promotion.
