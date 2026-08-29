# Bonsai v2 Artifact Contracts

**Project:** `bonsai-dev`  
**Ownership:** Human-owned project design  
**Purpose:** Durable behavioral contracts for the Bonsai standard artifacts and self-hosting transition

## Bootstrap Context

These contracts are being extracted while Bonsai 1.4 is the active runtime.

The running v1.4 standard under `.bonsai/` is archaeological evidence and temporary execution machinery.

The candidate v2 standard is staged under:

```text
bonsai/
```

The staged tree is temporary. After successful promotion and fresh-session proof, it is removed and `.bonsai/` again becomes the single shipped/self-hosting Bonsai tree.

## Why This Layer Exists

The existing Bonsai implementation contains accumulated workflow knowledge that is more detailed than the new v2 specification.

The contracts prevent that knowledge from being lost while also preventing old implementation structure from becoming accidental authority.

```text
existing implementation
    ↓
learned behavior
    ↓
Keep / Adapt / Drop / Missing
    ↓
artifact contract
    ↓
v2 staged implementation
    ↓
validation
    ↓
promotion
```

## Contract Schema

Each implemented standard artifact should eventually have a contract covering:

| Field | Purpose |
| --- | --- |
| Artifact | Exact standard artifact path/name |
| Role | Why the artifact exists |
| Loaded when | Bootstrap / workflow / facet trigger |
| Inputs | Context/state assumed available |
| Responsibilities | Behavior the artifact must provide |
| Must not | Important boundaries and prohibited behavior |
| Reads | Durable artifacts it may consume |
| Writes | Durable artifacts it may maintain |
| Delegates to | Prompts/skills/workflows it invokes |
| Human gates | Approval boundaries it owns |
| Preserve from existing version | Learned behavior that should survive |
| v2 changes | Behavior intentionally changed for v2 |
| Validation cases | How the implementation will be tested |

If v2 requires behavior but Phase 1 has not established the correct artifact seam, record it as an unresolved responsibility rather than inventing a permanent file merely to complete the table.

## Classification Meanings

- **Keep:** behavior remains correct with little conceptual change.
- **Adapt:** behavior is valuable, but v2 changes its surrounding model, path, ownership, trigger, or integration.
- **Drop:** behavior belongs to a deliberately removed v1 assumption.
- **Missing:** v2 requires behavior not represented adequately in the old standard.

## Contract Groups

```text
core_workflows.md
    startup, implementation routing, menus, phase execution,
    final truth, dry runs, handoff, operational agent memory

project_workflows.md
    project-memory synthesis, project lifecycle, Bonsai Home,
    templates and context/project workflow seams

code_maps.md
    mapping calibration, mapping workflow, map data structures,
    evidence discipline, navigation, maintenance, source identity

promotion_validation.md
    test artifact boundaries, staged-distribution purity,
    rollback archive, candidate construction, promotion,
    execution-memory conversion, fresh-session self-hosting proof
```

These groups are for review convenience, not runtime modules.

## Initial Archaeological Inventory

### Existing standard / workflow artifacts

| Existing artifact | Current v2 direction | Initial classification |
| --- | --- | --- |
| `.bonsai/implementation_prompt.md` | staged `bonsai/prompts/implementation.md` plus extracted skills/bootstrap responsibilities | Adapt |
| `.bonsai/design_session.md` | staged `bonsai/prompts/create_project_memory.md` | Adapt |
| `.bonsai/skills/phase_execution.md` | staged `bonsai/skills/phase_execution.md` | Keep + Adapt |
| `.bonsai/skills/handoff.md` | staged `bonsai/skills/handoff.md` | Keep + Adapt |
| `.bonsai/skills/final_truth_update.md` | staged `bonsai/skills/final_truth_update.md` | Keep + Adapt |
| `.bonsai/skills/dry_run.md` | staged `bonsai/skills/dry_run.md` | Mostly Keep |
| `.bonsai/skills/tooling_memory.md` | staged `bonsai/skills/agent_context.md` | Adapt |
| `.bonsai/templates/plan_phase_template.md` | v2 phase-plan template | Adapt |
| `.bonsai/templates/icebox_template.md` | v2 icebox template | Mostly Keep |
| `.bonsai/developer_context.example.md` | distribution/example decision still to be extracted | Unresolved |
| `.bonsai/developer_context.md` | repository-specific context, not standard artifact | Do not treat as standard source |

### Existing mapping artifacts

| Existing artifact | Current v2 direction | Initial classification |
| --- | --- | --- |
| `.bonsai/maps/repo_session.md` | staged `bonsai/prompts/create_map_repo.md` | Adapt |
| `.bonsai/maps/map_prompt.md` | integrated map lifecycle workflow | Adapt |
| `.bonsai/maps/map_system.md` | retain useful map-system rules under integrated mapping | Major Adapt |
| `.bonsai/maps/README.md` | reconcile with integrated user guidance | Adapt |
| `.bonsai/maps/templates/code_map_template.md` | map entry format | Preserve candidate |
| `.bonsai/maps/templates/namespace_router_template.tsv` | namespace lookup format | Preserve candidate |
| `.bonsai/maps/templates/subsystem_map_template.md` | subsystem map format | Preserve candidate |
| `.bonsai/maps/templates/api_pub_template.md` | optional public API map format | Preserve candidate |
| `.bonsai/maps/templates/api_ext_template.md` | optional extension API map format | Preserve candidate |
| `.bonsai/maps/templates/manifest_template.tsv` | optional lookup artifact | Preserve candidate |
| `.bonsai/maps/templates/symbol_index.tsv` | optional symbol lookup artifact | Preserve candidate |
| `.bonsai/maps/templates/map_state_template.md` | active mapping resume state | Preserve + Adapt candidate |

### Existing validation fixture

The v1.4:

```text
.bonsai/projects/task-tracker/
```

is archaeological validation material, not a Bonsai standard artifact.

Its eventual role should be decided during validation planning rather than converted automatically.

## Known Missing v2 Behavior

The specification requires behavior that has no clean independent artifact in the old tree, including:

- repository-local `.bonsai/start.md`;
- reusable menu behavior;
- Bonsai Home creation and resolution;
- session-local project selection and project management;
- developer/repository/project scoped `agent_context.md`;
- integrated Manage Code Maps routing;
- map/source identity alignment;
- project-level relevant-map selection;
- self-hosting promotion and rollback behavior needed by this repository.

Phase 1 must assign these responsibilities deliberately.

## Contract Status

The files in this directory are **seed contracts**, not completed archaeology.

They capture v2 decisions already established plus first-pass learned behavior from the old implementation.

Phase 1 must deepen them before associated staged standard artifacts are materially rewritten.
