# Artifact Contracts — Validation and Self-Hosting Promotion

**Project:** `bonsai-dev`  
**Status:** Seeded; exact implementation seams to be finalized before Phase 5

## Purpose

Define the durable boundaries required to test artifact-producing Bonsai workflows, keep the staged distribution clean, safely replace the Bonsai runtime that built v2, and prove the repository is truly self-hosting afterward.

---

## Contract: Staged Distribution Purity

### Role

Keep:

```text
repo/bonsai/
```

equal to the candidate Bonsai 2.0 distribution during the bootstrap refactor.

### Responsibilities

- contain only artifacts intended to ship as Bonsai;
- remain suitable as direct input to isolated validation and promotion;
- allow a complete-tree comparison without filtering generated test debris.

### Must not

- contain generated test outputs;
- contain test logs;
- contain promotion scratch directories;
- contain local rollback archives;
- contain repository-specific Bonsai project memory.

### Validation cases

- clean-tree assertion detects accidental generated files under `bonsai/`;
- staged tree can be copied directly as the standard portion of an isolated embedded Bonsai fixture.

---

## Contract: Test Artifact Boundaries

### Role

Provide repeatable validation for workflows that produce files, directories, zips, maps, or execution-memory changes.

### Durable inputs

Conventionally:

```text
tests/fixtures/
```

### Durable expected outputs

When golden artifacts are appropriate:

```text
tests/expected/
```

### Generated outputs

Conventionally:

```text
build/bonsai-tests/
```

### Responsibilities

- isolate each scenario's generated output;
- allow deterministic cleanup/re-run;
- compare only behavior/artifacts intentionally covered by the test;
- support artifact-producing workflows such as project-memory generation, mapping, startup/project routing, and promotion.

### Must not

- write actual test results into `bonsai/`;
- let golden outputs become a second specification;
- require golden-file comparison when semantic assertions are more appropriate;
- preserve disposable run output in source control.

### Validation cases

At minimum support eventual scenarios for:

- `create_project_memory.md` output;
- `create_map_repo.md` output;
- code-map output;
- embedded startup;
- Bonsai Home startup;
- project selection/switching;
- agent-context layering;
- promotion candidate construction;
- self-hosting project-memory conversion.

---

## Contract: Self-Hosting Backup

### Role

Create an immediate local rollback point immediately before live promotion.

### Output

Conventionally:

```text
.bonsai-backups/
    bonsai-YYYYMMDD-HHMMSS.zip
```

### Responsibilities

- archive the pre-promotion `.bonsai` sufficiently for direct rollback;
- use an unambiguous local datetime stamp;
- complete successfully before the live standard is replaced;
- keep backups outside both staged `bonsai/` and live `.bonsai/`.

### Must not

- be treated as source-controlled release history;
- replace Git history or formal release artifacts;
- continue promotion if the required backup fails.

### Validation cases

- archive can reconstruct the pre-promotion `.bonsai`;
- timestamp naming does not collide in normal use;
- backup failure prevents destructive promotion.

---

## Contract: Promotion Candidate Construction

### Role

Build a complete replacement `.bonsai` without mutating the live runtime.

### Working location

A disposable location such as:

```text
build/bonsai-promotion/candidate/.bonsai/
```

### Inputs

- validated staged `bonsai/`;
- current repository-local Bonsai memory that must survive;
- explicit v1.4 → v2 self-hosting execution-memory conversion rules.

### Responsibilities

- copy the candidate v2 standard into the candidate root;
- preserve applicable repository-owned memory;
- convert `bonsai-dev` execution memory:
  - `plan.md` → `agent_plan.md`;
  - `state.md` → `agent_state.md`;
  - active/future `plan/plan_phase_<N>.md` → v2 naming when applicable;
- remove bootstrap-only v1.4 execution-memory duplicates from the candidate;
- validate that no required local memory was lost;
- validate that no legacy v1 standard file leaked into the candidate merely because it shared the old `.bonsai` tree.

### Must not

- merge the entire old `.bonsai` blindly;
- overwrite the live runtime while candidate assembly is incomplete;
- create both v1 and v2 execution-memory names as competing truths.

### Preservation set

At minimum:

```text
.bonsai/projects/bonsai-dev/
```

must survive semantically.

Repository-local developer/agent context must survive when present and applicable.

The exact broader preservation set must be finalized from the v2 standard artifact inventory before implementation.

### Validation cases

- candidate contains staged standard plus project memory;
- candidate contains v2 execution-memory names only;
- candidate excludes obsolete v1 standard files;
- candidate preserves repository context that contract says must survive;
- candidate passes startup-layout validation before live swap.

---

## Contract: Live Promotion

### Role

Replace the Bonsai runtime that built v2 with the fully validated v2 candidate.

### Preconditions

- staged distribution passes required validation;
- complete candidate `.bonsai` passes validation;
- timestamped backup succeeds;
- current project state records promotion as the authorized exact next step.

### Responsibilities

- use the safest host-supported directory replacement procedure;
- minimize the interval in which live `.bonsai` is incomplete;
- verify the resulting live tree after replacement;
- leave rollback archive and staged `bonsai/` intact until fresh-session proof succeeds.

### Must not

- delete live `.bonsai` before a complete candidate exists;
- continue silently after partial-copy failures;
- remove `bonsai/` in the same destructive step as promotion;
- claim self-hosting success merely because file copy completed.

### Validation cases

- successful swap;
- simulated copy/swap failure with rollback assets retained;
- promoted tree equals validated candidate;
- current self-hosting project is still present.

---

## Contract: Fresh-Session Self-Hosting Proof

### Role

Prove that the promoted Bonsai 2.0 can resume and operate the project that created it.

### Test instruction

From a fresh coding-agent session in the repository:

```text
Read .bonsai/start.md and follow its instructions.
```

### Success criteria

The new v2 runtime:

- resolves Bonsai Home / embedded identity correctly;
- resolves repository home;
- resolves the `bonsai-dev` project correctly;
- reads `agent_plan.md` / `agent_state.md`;
- reports the correct phase, readiness, and exact next step;
- can execute or route one bounded authorized follow-up under v2 rules.

### Responsibilities after success

- mark the self-hosting transition complete;
- remove temporary `repo/bonsai/`;
- ensure `.bonsai/` is now the single canonical distribution/self-hosting source tree;
- update project architecture/state if any temporary bootstrap statements are no longer current.

### Must not

- use the old v1.4 implementation prompt as fallback without surfacing failure;
- rely on the old chat session's volatile context;
- delete staging before the fresh-session proof succeeds.

### Validation cases

The proof itself is an acceptance test and should also be represented by repeatable isolated startup tests where feasible.

---

## Contract: Post-Promotion Repository Invariant

After successful promotion:

```text
repo/.bonsai/
```

is simultaneously:

- the Bonsai distribution that users can copy/use;
- the Bonsai standard source contributors edit;
- the embedded Bonsai runtime for developing Bonsai itself;
- the location containing repository/project memory needed for self-hosting.

There is no permanent:

```text
repo/bonsai/
```

source twin.

Future Bonsai revisions should normally be performed directly under v2's own workflow. If a future revision again requires destructive replacement of the running standard, the same staging/promotion pattern may be used deliberately rather than creating a permanently duplicated source tree.
