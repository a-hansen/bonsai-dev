# Developing Bonsai with Bonsai

`bonsai-dev` is Bonsai's persistent self-development project.

It exists so Bonsai can be used to design, implement, validate, and evolve Bonsai itself.

The project is not tied to a single release or enhancement. Individual changes are bounded bodies of work within the continuing `bonsai-dev` project.

## Designing a Bonsai Change

Bonsai changes normally begin in a fresh Web UI AI conversation.

Start by providing the current:

```text
specification.md
```

from the Bonsai Home you intend to modify, then describe the change you want to make.

`specification.md` is the authoritative description of Bonsai's current behavior and operating model. It should provide enough context for the design AI to determine what additional framework artifacts are relevant.

Do not preload the entire Bonsai standard.

Instead, add context progressively.

When the design AI needs to discover more detailed framework behavior, provide the applicable category guide:

```text
skills/skills.md
prompts/prompts.md
templates/templates.md
```

The AI can then request the specific skills, prompts, or templates it needs.

For example, a change to menu behavior might proceed like this:

```text
specification.md
    ↓
skills/skills.md
    ↓
skills/menu.md
```

If the change also affects startup or implementation routing, the AI may additionally request:

```text
prompts/prompts.md
prompts/implementation.md
start.md
```

Supply only the artifacts that become relevant to the design.

## Use One Bonsai Home

Framework artifacts used together during design should normally come from the same Bonsai Home as the supplied `specification.md`.

Depending on the environment, the Bonsai Home may be:

```text
$BONSAI_HOME/
```

or an Embedded Bonsai standard under:

```text
repo/.bonsai/
```

The physical location does not change the workflow.

When intentionally comparing Bonsai versions, artifacts from another Bonsai Home may also be supplied, but the distinction should be explicit.

## Additional Design Context

Skills, prompts, and templates are not the only context a design may need.

Relevant source, code maps, existing project memory, examples, or other artifacts may also be supplied when they materially help the design.

There is no requirement to provide all available maps or source context at the start of a design session. Add them when the design actually needs them.

## Updating `bonsai-dev` Project Memory

When the design is mature enough to implement, provide the Web UI AI with:

```text
prompts/create_project_memory.md
```

and ask it to update the existing named project:

```text
bonsai-dev
```

The design workflow should use the current `bonsai-dev` project memory as its baseline and update only the artifacts materially affected by the approved design.

A typical update may include:

```text
.bonsai/projects/bonsai-dev/
    requirements.md
    architecture.md
    agent_plan.md
    agent_state.md
```

Not every change requires all four files, but the live project memory should remain internally consistent and describe the current project and current body of work.

The Web UI workflow produces a ZIP rooted at:

```text
.bonsai/projects/bonsai-dev/
```

Review the generated human-owned project truth before adopting it, then extract the ZIP at the repository root.

The design workflow does not create the detailed Phase 1 implementation plan.

## Starting Implementation

After adopting the updated project memory, start a coding-agent session with:

```text
Read .bonsai/start.md and follow its instructions. Active project: bonsai-dev.
```

Bonsai should reconstruct the current project state from durable memory.

For a newly designed body of work, the normal first implementation gate is:

```text
Execution Readiness: Phase planning required
```

The coding agent then drafts:

```text
plan/agent_plan_phase_1.md
```

for human review.

After the plan is approved, Bonsai implements the authorized work, performs the required validation, reconciles final-truth impact, and updates execution memory at the next natural boundary.

## Persistent Project, Bounded Work

`bonsai-dev` remains available after an enhancement is complete.

Do not create a new Bonsai project merely because a new Bonsai enhancement begins.

Instead:

```text
persistent bonsai-dev project
        ↓
design a bounded change
        ↓
update current project memory
        ↓
plan / implement / validate
        ↓
complete the body of work
        ↓
begin the next change when needed
```

Completed-work history may be preserved separately from living project truth. Current project artifacts should describe Bonsai and its active work now, not force future contributors to reconstruct current state from historical implementation material.

## Context Discipline

The same context principle used by Bonsai implementation applies when designing Bonsai itself:

> Start with the smallest authoritative context and load additional context only when it becomes useful.

For framework design, that normally means:

```text
specification.md
        ↓
category guide when needed
        ↓
specific framework artifact
        ↓
source, maps, or other context when needed
```

This keeps design sessions focused while still allowing the AI to inspect the exact current behavior relevant to the change.
