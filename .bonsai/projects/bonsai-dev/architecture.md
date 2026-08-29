# Bonsai v2 Self-Hosting Architecture

**Project:** `bonsai-dev`  
**Ownership:** Human-owned project truth  
**Bootstrap Runtime:** Bonsai 1.4  
**Target Runtime:** Bonsai 2.0

## Architectural Goal

Use the currently working Bonsai 1.4 installation to build a staged Bonsai 2.0 without destroying the tool performing the work, then promote the validated v2 over the old installation and collapse back to a single self-hosting `.bonsai` tree.

## Bootstrap Repository Model

During the refactor:

```text
repo/
├── .bonsai/
│   ├── ...                         # running Bonsai 1.4 standard
│   └── projects/
│       └── bonsai-dev/
│           ├── requirements.md
│           ├── architecture.md
│           ├── plan.md             # active v1.4 execution memory
│           ├── state.md            # active v1.4 resume state
│           └── artifact_contracts/
│
├── bonsai/                         # temporary staged Bonsai 2.0 distribution
│   ├── specification.md
│   ├── README.md
│   ├── start.md                    # added during implementation
│   ├── prompts/                    # added during implementation
│   ├── skills/                     # added during implementation
│   └── templates/                  # added during implementation
│
├── tests/                          # durable validation definitions
│   ├── fixtures/
│   └── expected/
│
└── build/                          # disposable/generated output
    ├── bonsai-tests/
    └── bonsai-promotion/
```

`tests/` and `build/` are target repository conventions. They need not exist until validation work requires them.

## Stable Repository Model After Promotion

After v2 promotion and the fresh-session self-hosting proof:

```text
repo/
├── .bonsai/
│   ├── start.md
│   ├── specification.md
│   ├── README.md
│   ├── prompts/
│   ├── skills/
│   ├── templates/
│   └── projects/
│       └── bonsai-dev/
│           ├── requirements.md
│           ├── architecture.md
│           ├── agent_plan.md
│           ├── agent_state.md
│           └── artifact_contracts/
│
├── tests/
└── build/
```

The sibling `bonsai/` staging tree is gone.

This stable model preserves the original Bonsai distribution property:

```text
clone repository
    ↓
the repository's .bonsai is the Bonsai distribution
```

and also enables:

```text
clone repository
cd repository
Read .bonsai/start.md and follow its instructions.
    ↓
use Bonsai to modify Bonsai itself
```

## Staging Principle

The temporary `bonsai/` tree exists only because Bonsai 1.4 cannot safely replace itself while actively driving the refactor.

During bootstrap:

```text
.bonsai/
    = builder

bonsai/
    = product being built
```

After successful promotion:

```text
.bonsai/
    = builder + product + shipped distribution

bonsai/
    = removed
```

Therefore `bonsai/` must never evolve into a second permanent source tree.

## Distribution Purity

The staged:

```text
bonsai/
```

must contain only candidate distribution artifacts.

Do not put generated output under it.

Durable test definitions belong beside the distribution:

```text
tests/
```

Disposable output belongs under:

```text
build/
```

A useful default:

```text
tests/
├── fixtures/
└── expected/

build/
├── bonsai-tests/
└── bonsai-promotion/
```

This creates a strong invariant:

> The complete `bonsai/` tree can be validated and promoted without filtering test debris.

## Golden Artifact Model

Some workflows naturally produce artifacts and should be tested as artifact producers.

Examples include:

- `create_project_memory.md` producing a project-memory zip/tree;
- `create_map_repo.md` producing `map_repo.md`;
- code-map creation producing named map trees;
- startup/project-management scenarios producing or updating execution memory;
- promotion producing a complete candidate `.bonsai`.

When a durable expected output is valuable:

```text
tests/expected/<scenario>/
```

may contain checked-in golden artifacts.

An actual run writes to:

```text
build/bonsai-tests/<scenario>/
```

and validation compares actual behavior/output with the expected contract.

Golden files are test authority only for the behavior intentionally covered by that test. They do not supersede the Bonsai specification or artifact contracts.

## Authority Chain During Bootstrap

```text
bonsai/specification.md
        │
        │ Bonsai v2 operating-model final truth
        ▼
.bonsai/projects/bonsai-dev/
    requirements.md
    architecture.md
        │
        │ design for this refactor
        ▼
artifact_contracts/
        │
        │ standard-artifact behavioral design
        ▼
bonsai/
    staged v2 implementation
        │
        ▼
tests/ + isolated build outputs
        │
        ▼
promotion candidate
        │
        ▼
promoted .bonsai/
```

After promotion, the same authority chain begins at:

```text
.bonsai/specification.md
```

instead of the removed staging path.

## Bootstrap Execution Memory

While Bonsai 1.4 is the active runtime, the self-hosting project intentionally uses:

```text
plan.md
state.md
plan/plan_phase_<N>.md
```

These are the active execution truth because the running v1.4 implementation knows how to load and maintain them.

Do not maintain duplicate v2 execution-memory files beside them.

The v2 target contract remains:

```text
agent_plan.md
agent_state.md
plan/agent_plan_phase_<N>.md
```

The transition to those names occurs as part of the self-hosting promotion.

This is a temporary bootstrap constraint, not v2 compatibility policy.

## Artifact Contract Layer

Artifact contracts remain human-owned project design under:

```text
.bonsai/projects/bonsai-dev/artifact_contracts/
```

Grouping is organizational only. Each implemented standard artifact must have an identifiable contract.

Default fields:

| Field | Meaning |
| --- | --- |
| Artifact | Exact standard artifact path or explicitly unresolved target seam |
| Role | Why it exists |
| Loaded when | Bootstrap, workflow, or facet trigger |
| Inputs | Context/state assumed available |
| Responsibilities | Behavior it owns |
| Must not | Boundaries and prohibited behavior |
| Reads | Durable artifacts it may consume |
| Writes | Durable artifacts it may maintain |
| Delegates to | Other prompts, skills, or workflows |
| Human gates | Approval boundaries it owns |
| Preserve from existing version | Learned behavior to retain |
| v2 changes | Deliberate changes from the old model |
| Validation cases | How implementation is tested |

Contracts describe behavior, not historical prose.

## Archaeological Flow

```text
existing v1 artifact
    ↓
behavior / edge-case extraction
    ↓
Keep / Adapt / Drop / Missing
    ↓
artifact contract
    ↓
human review
    ↓
staged v2 implementation
```

The old file path has no authority merely because it exists.

## Core Workflow Decomposition

Known target seams include:

```text
.bonsai/start.md                  # runtime path after promotion
prompts/implementation.md
skills/menu.md
skills/phase_execution.md
skills/handoff.md
skills/final_truth_update.md
skills/agent_context.md
skills/dry_run.md
skills/code_maps.md
```

During staging, the corresponding source-distribution paths are rooted under:

```text
bonsai/
```

For example:

```text
bonsai/start.md
bonsai/prompts/implementation.md
```

The exact set of additional project-management or Bonsai-Home workflow artifacts must come from Phase 1 archaeology rather than speculative decomposition.

## Mapping Architecture

Mapping becomes an integrated Bonsai capability while retaining useful mature internals.

During staging, its source artifacts live under `bonsai/`.

At runtime, reusable map data follows the specification's Bonsai Home or embedded map-store model.

Map data is not test output and is not automatically part of the standard distribution merely because the mapping implementation can create it.

## Promotion Architecture

Promotion is a controlled self-replacement operation.

### Inputs

- validated staged `bonsai/`;
- current running `.bonsai/`;
- repository-owned durable memory that must survive;
- validated rules defining the preservation set.

### Local rollback archive

Before destructive replacement, create:

```text
.bonsai-backups/
    bonsai-YYYYMMDD-HHMMSS.zip
```

The archive captures the pre-promotion `.bonsai` sufficiently for immediate local rollback.

The backup directory is local/disposable and normally gitignored.

### Candidate construction

Do not mutate the live `.bonsai` while assembling the replacement.

Construct a candidate in a disposable location, for example:

```text
build/bonsai-promotion/candidate/.bonsai/
```

Conceptually:

```text
staged v2 standard
        +
preserved repository memory
        +
v2-converted bonsai-dev execution memory
        =
complete candidate .bonsai
```

### Preservation boundary

At minimum preserve:

```text
.bonsai/projects/bonsai-dev/
```

while converting its active execution-memory names from the v1.4 bootstrap format to the v2 format.

Repository-local developer/agent context must be preserved when applicable.

Legacy v1 standard files are replaced, not merged blindly.

The exact standard-vs-memory preservation rules must be explicitly contracted and tested before implementation.

### Swap

After candidate validation and backup creation, replace the live `.bonsai` with the complete candidate using the safest host-supported directory replacement strategy.

If the replacement fails, the timestamped archive and staged `bonsai/` remain available.

## Fresh-Session Self-Hosting Proof

After promotion, do not immediately delete the staging tree.

Start a new coding-agent session and run:

```text
Read .bonsai/start.md and follow its instructions.
```

Success requires that v2:

- resolves environment identity correctly;
- resumes `bonsai-dev`;
- reads the v2 execution-memory names;
- reports the correct current phase/readiness/next step;
- can continue a bounded Bonsai-development action.

Only after that succeeds is the self-hosting transition complete.

Then:

```text
remove repo/bonsai/
```

and `.bonsai/` becomes the only canonical Bonsai tree.

## Phase Architecture

### Phase 1 — Archaeology and Artifact Contracts

Inventory the current standard, extract learned behavior, create/review contracts, and identify missing/obsolete seams.

No substantive v2 implementation.

### Phase 2 — Bootstrap and Core Execution Model

Implement the staged v2 startup and implementation spine under `bonsai/`.

Do not overwrite the active `.bonsai`.

### Phase 3 — Context and Project Workflows

Implement context layering, project lifecycle, project-memory synthesis, phase execution, final-truth handling, handoff, templates, and related behaviors.

### Phase 4 — Integrated Code Maps

Integrate the mature mapping system with the v2 environment/source/project model.

### Phase 5 — Validation, Promotion, and Self-Hosting Proof

- build isolated test fixtures and artifact-producing validation;
- validate the staged v2;
- validate a complete promotion candidate;
- archive the running v1.4 `.bonsai`;
- promote v2 into `.bonsai`;
- convert the self-hosting project execution memory to v2 names;
- prove fresh-session self-hosting;
- remove the temporary `bonsai/` staging tree.

## Guardrails

- Do not rewrite the running v1.4 standard in place during the staged refactor.
- Do not maintain duplicate v1/v2 execution-memory truths.
- Do not put generated test output under `bonsai/`.
- Do not make manual copying the release/promotion mechanism.
- Do not delete the current runtime before a complete candidate and rollback archive exist.
- Do not delete staging until the fresh-session v2 proof succeeds.
- Do not let artifact contracts silently revise the specification.
- Do not delete mature behavior until archaeology determines it is obsolete or conflicting.
- Do not introduce registries/configuration layers without demonstrated need.
