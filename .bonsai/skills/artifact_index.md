# Artifact Index Skill

## Purpose

Keep Bonsai's prompt, skill, and template category guides aligned with the discoverable standard artifact surface
without turning those guides into duplicate authority.

This skill owns category-guide reconciliation and validation. It does not authorize the underlying framework
artifact change, redefine artifact behavior, or manage runtime code maps.

## When to Load

Load this skill when:

- an authorized standard prompt, skill, or template addition, removal, rename, or material responsibility change
  has made category-guide reconciliation the current facet or a required completion condition;
- the human explicitly requests category-guide maintenance or validation; or
- a known category-guide accuracy problem must be resolved within an authorized workflow.

Do not load it for ordinary internal edits that leave an artifact's routing responsibility unchanged, routine
startup, speculative inventory work, or runtime map lifecycle changes.

## Required Inputs

Use only the context needed for the affected categories:

- the resolved Bonsai Home from the invoking session;
- the authorized artifact change and its approved basis;
- the affected standard directories and existing category guides;
- relevant `specification.md` rules when authority, scope, or discoverability must be checked; and
- the invoking workflow or gate.

Resolve all standard identities beneath the active Bonsai Home. Do not substitute the repository-local `.bonsai`
tree when the session resolved a different home, combine inventories from multiple homes, or persist Bonsai Home
as project state.

## Owned Guides

This skill maintains only:

```text
<bonsai-home>/skills/skills.md
<bonsai-home>/prompts/prompts.md
<bonsai-home>/templates/templates.md
```

Each guide is a concise routing surface for its own category. The guide file itself is not an entry in its own
inventory. `skills/artifact_index.md` is a discoverable skill and belongs in `skills/skills.md`.

## Qualifying Changes

Reconcile a guide when a standard artifact in its category is:

- added;
- removed;
- renamed; or
- materially changed in responsibility so that its routing description is no longer accurate.

An internal clarification, implementation detail, example, validation refinement, or other change that preserves
the artifact's discoverability and responsibility does not require guide churn. When qualification is ambiguous,
compare the previous and current routing responsibility and surface the ambiguity instead of editing for
completeness theater.

Category-guide maintenance is part of the qualifying lifecycle change. An approved multi-step change may defer
reconciliation until the affected artifact set is stable, but the lifecycle change must not be reported complete
until the affected guides have been reconciled and validated.

## Reconciliation Workflow

1. Retain the invoking workflow or gate and its authorization boundary.
2. Resolve the active Bonsai Home and the affected categories without writing session identity.
3. Confirm the underlying change is authorized and qualifies under this skill. If it does not qualify, leave the
   guides unchanged and return that result to the invoking workflow.
4. Inspect the actual affected standard directory and identify the relevant current standard artifacts. Exclude
   the category guide itself, generated output, runtime data, project memory, maps, and files whose framework role
   is not established by the active standard.
5. Compare the inventory with the affected guide. Add new entries, remove retired entries, reconcile renamed
   entries, and revise descriptions only when responsibility materially changed.
6. Keep each entry responsibility-oriented and sufficient to decide whether to load that artifact next. Do not
   copy detailed procedures, template contents, or specification rules into the guide.
7. Preserve the guide's existing clear structure. When creating a required missing guide, use a compact heading,
   a short authority statement, and one unambiguous artifact-to-responsibility listing; do not invent a broader
   catalog schema.
8. Validate the affected guides before returning.

If approved final truth does not establish whether an artifact belongs in the discoverable standard surface or
what responsibility it exposes, stop for the applicable final-truth clarification or revision workflow rather
than guessing.

## Validation

For every affected guide, verify that:

- every listed identity resolves to a readable artifact beneath the same Bonsai Home;
- every relevant current artifact in the category is represented exactly once, excluding the guide itself;
- removed and renamed identities no longer remain as stale entries;
- descriptions remain concise, responsibility-oriented routing information;
- the guide does not claim authority over `specification.md` or reproduce detailed artifact behavior; and
- no `maps/maps.md` guide or runtime map index has been introduced.

Use deterministic filesystem checks for identities and coverage. Use focused semantic review for responsibility
descriptions. A broken reference, omitted relevant artifact, duplicate entry, mixed-home identity, or authority
conflict blocks completion of the qualifying lifecycle change.

## Return and Handoff

Report to the invoking workflow:

- the qualifying change or explicit maintenance request;
- guides changed, or `None` when no reconciliation was required;
- validation actually performed and its result;
- unresolved ambiguity or blockers; and
- final-truth impact: `None`, `Clarification`, or `Revision`.

Guide reconciliation that faithfully applies approved truth has final-truth impact `None`. A needed clarification
or revision delegates to `skills/final_truth_update.md` and returns through the invoking workflow's gate.

This skill does not independently update project execution memory or choose the next implementation step. After
successful reconciliation, return control to the invoking workflow so it can reconcile its own state and present
the applicable gate.

## Boundaries

- Do not edit unrelated standard artifacts merely because their directory was inspected.
- Do not add guide entries for hypothetical, retired, generated, project-specific, or runtime artifacts.
- Do not make a category guide self-referential.
- Do not treat editing a guide's own wording as a new lifecycle trigger for that same guide.
- Do not create a global catalog or `maps/maps.md` for symmetry.
- Do not use guide maintenance to broaden the authorized framework change.
