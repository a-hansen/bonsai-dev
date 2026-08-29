# Bonsai v2 Self-Hosting Requirements

**Project:** `bonsai-dev`  
**Ownership:** Human-owned project truth  
**Bootstrap Runtime:** Bonsai 1.4  
**Target Runtime:** Bonsai 2.0

## Authority

This project builds Bonsai 2.0 using Bonsai 1.4 until the staged v2 implementation is validated and promoted.

During the bootstrap/refactor period, the authoritative Bonsai v2 specification is:

```text
bonsai/specification.md
```

The human-facing v2 workflow guide is:

```text
bonsai/README.md
```

After successful self-hosting promotion, the staged `bonsai/` tree is promoted into `.bonsai/`, the staging tree is removed, and the corresponding authoritative runtime paths become:

```text
.bonsai/specification.md
.bonsai/README.md
```

This path transition is part of the approved self-hosting lifecycle. It does not change the meaning of the specification.

The current Bonsai 1.4 implementation under `.bonsai/` is archaeological evidence and the temporary runtime driving the refactor. It is not authoritative when it conflicts with the v2 specification.

## Product Goal

Refactor Bonsai into the v2 operating model while preserving still-valid learned behavior from the existing implementation, and make the Bonsai repository self-hosting so future Bonsai revisions can be designed, implemented, tested, promoted, and reviewed using Bonsai itself.

## Core Requirements

### REQ-1 — Bonsai 1.4 must remain usable while v2 is built

The repository's current:

```text
.bonsai/
```

continues to be the running Bonsai 1.4 installation during the bootstrap period.

The `bonsai-dev` self-hosting project therefore uses Bonsai 1.4 execution-memory names while v1.4 is the active runtime:

```text
.bonsai/projects/bonsai-dev/
    requirements.md
    architecture.md
    plan.md
    state.md
    plan/plan_phase_<N>.md
```

Do not create parallel `agent_plan.md` / `agent_state.md` copies during the bootstrap period.

When v2 is promoted, the surviving self-hosting project memory is converted to the v2 execution-memory names:

```text
agent_plan.md
agent_state.md
plan/agent_plan_phase_<N>.md
```

The transition must preserve current execution meaning rather than create two competing truths.

### REQ-2 — `bonsai/` is a temporary staged v2 distribution

During the refactor:

```text
.bonsai/
    = current running Bonsai 1.4 + repository project memory

bonsai/
    = staged candidate Bonsai 2.0 distribution
```

`bonsai/` is temporary bootstrap staging, not the permanent source location.

It must contain only files intended to become part of the candidate Bonsai distribution.

Once v2 is validated, promoted, and proven through a fresh self-hosting session, `bonsai/` is removed and `.bonsai/` becomes the single canonical Bonsai distribution/source tree again.

### REQ-3 — The staged distribution must remain independently shippable

At every point where the staged v2 is considered testable, the `bonsai/` tree must be interpretable as the candidate distribution without filtering unrelated generated files.

Generated test output, temporary promotion candidates, logs, and run artifacts must never be written inside `bonsai/`.

### REQ-4 — Test definitions and generated test output are separate

Durable test material may live under:

```text
tests/
    fixtures/
    expected/
```

Generated test output belongs outside the staged distribution, conventionally under:

```text
build/bonsai-tests/
```

Generated promotion candidates may likewise use a disposable build location such as:

```text
build/bonsai-promotion/
```

`build/` output is disposable and should be ignored by source control.

Golden or expected artifacts may be checked into `tests/expected/` when comparison against a durable expected result provides useful contract coverage.

### REQ-5 — Learned behavior is extracted before standard artifacts are rewritten

Before materially rewriting an existing Bonsai prompt, skill, template, or mapping artifact:

1. inspect the existing artifact;
2. identify the behavior and edge cases it protects;
3. reconcile that behavior with the v2 specification;
4. classify it as `Keep`, `Adapt`, `Drop`, or `Missing`;
5. record the durable artifact contract;
6. review the contract sufficiently to make implementation safe.

The existing implementation is evidence, not a source to copy blindly.

### REQ-6 — Standard artifacts are rebuildable from durable design

Each standard artifact that survives or is introduced in v2 must have a durable behavioral contract sufficient to explain:

- why the artifact exists;
- when it is loaded;
- what inputs it assumes;
- what responsibilities it owns;
- what it must not do;
- what durable artifacts it may read or write;
- what other workflows it delegates to;
- what human gates it owns;
- what learned behavior is being preserved;
- what changed for v2;
- how the artifact can be validated.

Artifact contracts may be grouped for maintainability, but every implemented standard artifact must have an identifiable contract.

### REQ-7 — The v2 standard is implemented from contracts, not chat memory

Once an artifact contract is approved, the corresponding staged standard artifact under `bonsai/` is generated or updated to satisfy that contract and the v2 specification.

Conversational history is not implementation authority.

### REQ-8 — Preserve valuable v1 behavior unless v2 deliberately supersedes it

Repeatedly refined behavior in the existing implementation must not disappear merely because v2 changes file layout or workflow routing.

High-value areas include:

- implementation startup and execution gating;
- phase planning and contract-first execution;
- final-truth reconciliation;
- handoff and session-boundary behavior;
- out-of-scope observation handling;
- dry-run behavior;
- learned operational context;
- menu behavior embedded across workflows;
- project-memory synthesis;
- code-map calibration, navigation, indexing, maintenance, and evidence discipline.

Where the v2 model changes the surrounding mechanism, preserve the useful behavior by adapting it to the new boundary.

### REQ-9 — Do not preserve obsolete v1 structure for compatibility after promotion

Migration from Bonsai 1.x is out of scope unless separately adopted.

Temporary bootstrap use of v1.4 project-memory names is allowed only because v1.4 is the runtime performing this refactor.

Once v2 is successfully promoted, the repository must not retain duplicate v1/v2 execution-memory formats merely for compatibility.

### REQ-10 — Code mapping remains a first-class Bonsai capability

The existing mapping implementation must be mined carefully.

Useful mapping internals should be preserved when still valid, while entry, storage, context layering, source identity, and workflow integration are adapted to the v2 model defined by the specification.

The mapping refactor must not replace mature map structures solely for architectural neatness.

### REQ-11 — Promotion is part of the self-hosting project

The completed staged v2 must replace the Bonsai runtime that built it.

Promotion is an explicit project workflow, not a manual copy step.

Before replacing the current `.bonsai`, promotion must create a timestamped local rollback archive, conventionally:

```text
.bonsai-backups/
    bonsai-YYYYMMDD-HHMMSS.zip
```

The backup location is local/disposable and should normally be ignored by source control.

Promotion must preserve repository-specific durable memory, including the `bonsai-dev` project, while replacing the old standard with the validated staged v2 standard.

### REQ-12 — Promotion must be transactional enough to avoid a half-installed Bonsai

Promotion must not delete the current working Bonsai and then hope the staged copy succeeds.

The workflow must:

1. validate the staged `bonsai/` tree;
2. build a complete candidate `.bonsai` in a disposable location;
3. merge/preserve repository-owned memory into that candidate;
4. validate the complete candidate;
5. create the timestamped rollback archive;
6. swap/promote the candidate into `.bonsai`;
7. verify the promoted result.

If the platform cannot provide a truly atomic directory swap, the workflow must still minimize destructive steps and retain a clear rollback path.

### REQ-13 — Promotion must preserve local memory while replacing the standard

The promotion process must distinguish the Bonsai standard from repository-owned memory.

At minimum, the self-hosting project:

```text
.bonsai/projects/bonsai-dev/
```

must survive.

Applicable repository-local developer and agent context must also survive when present.

Legacy v1 standard files must not survive merely because they occupy the same `.bonsai` tree.

The exact preservation set must be contractually defined and validated before promotion is implemented.

### REQ-14 — Fresh-session execution is the self-hosting acceptance test

After promotion, `bonsai/` remains temporarily available until a fresh coding-agent session successfully starts using:

```text
Read .bonsai/start.md and follow its instructions.
```

The promoted v2 must:

- resolve the self-hosting repository correctly;
- select or resume `bonsai-dev`;
- understand the migrated v2 execution memory;
- report the correct current state and next step;
- continue under v2 semantics.

Only after that proof succeeds should the temporary `bonsai/` staging tree be removed.

### REQ-15 — Successful promotion collapses back to one Bonsai tree

The stable post-promotion repository model is:

```text
.bonsai/
    = shipped Bonsai standard
    + repository-local Bonsai memory
```

There is no permanent sibling `bonsai/` copy.

A contributor cloning the finished repository should be able to modify Bonsai itself and run Bonsai against those same shipped standard files without synchronizing two source trees.

### REQ-16 — Validate the actual v2 operating model

The completed refactor must be validated against the specification's required topologies:

- simple embedded repository;
- Bonsai Home repository;
- multi-repository project using `investment-app`, `barcache`, and `tickerview`;
- multi-project repository;
- external source without Bonsai project memory;
- greenfield repository.

Validation must cover workflow behavior, not just file existence.

## Constraints

- Keep startup context small.
- Keep simple repositories simple.
- Prefer lazy loading over automatic context accumulation.
- Prefer deterministic host discovery for deterministic facts.
- Do not add a configuration framework without demonstrated need.
- Keep work-specific names and employer-specific examples out of the public standard.
- Shell helpers remain optional conveniences.
- Human-owned final truth remains distinct from agent-owned execution memory.
- Source code and map data remain authoritative over summaries that describe them.
- Keep `bonsai/` free of generated test artifacts.
- Do not make manual copying part of the normal self-hosting release path.

## Phase 1 Boundaries

Phase 1 does not:

- implement v2 standard artifacts;
- implement `.bonsai/start.md`;
- promote or overwrite the running Bonsai;
- migrate active execution memory to v2 filenames;
- finalize helper-script packaging;
- redesign mature map data structures without archaeological evidence;
- create code maps merely to exercise the mapping workflow.

## Definition of Done

This project is complete when:

1. the staged v2 standard conforms to the v2 specification;
2. standard artifacts are backed by reviewed durable artifact contracts;
3. still-valid learned behavior from the existing implementation has been preserved or deliberately retired;
4. obsolete v1 seams have been removed rather than hidden behind permanent compatibility structure;
5. required v2 validation cases pass at the workflow level;
6. the current Bonsai has been archived and the validated v2 has been promoted into `.bonsai`;
7. a fresh session successfully resumes `bonsai-dev` using the promoted v2 runtime;
8. the temporary `bonsai/` staging tree has been removed;
9. `.bonsai/` is again the single shippable and self-hosting Bonsai tree.
