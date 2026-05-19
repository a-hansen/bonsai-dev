# Bonsai Map Prompt

## Purpose

Build, refresh, or maintain Bonsai code maps for this repository.

Code maps are durable navigation memory for future AI implementation sessions. They should help an
agent:

- orient quickly
- identify the right owning subsystem
- find the right source to inspect
- avoid repeatedly rediscovering important architectural structure
- preserve non-obvious calling and extension mechanics when they are likely to matter again

Code maps do not replace source inspection.  
They help future agents read the right source first.

All map structure, artifact-editing rules, maintenance rules, compression rules, and completion
standards are defined in:

```text
.bonsai/maps/map_system.md
```

Read and follow that file before proposing or performing mapping work.

---

## Mapping Workspace Initialization

Before beginning a mapping session, ensure the required mapping state file exists.

### `map_state.md`

If `.bonsai/maps/map_state.md` does not exist:

1. Read:

```text
.bonsai/maps/templates/map_state_template.md
```

2. Create:

```text
.bonsai/maps/map_state.md
```

3. Fill it with:

- the initial mapping objective
- active pass or focus
- exact next mapping step
- success condition for the next step
- recommended AI level for the current session

If `map_state.md` already exists, read it at startup and update it as the session progresses.

---

## Startup Sequence

1. Read:

```text
.bonsai/maps/map_system.md
.bonsai/maps/map_repo.md
.bonsai/maps/map_state.md
```

2. Read, if it exists:

```text
.bonsai/maps/code_map.md
```

3. Determine:

- the current mapping objective
- the active mapping pass or focus
- the exact next mapping step proposed by the current state
- whether that next step still appears valid
- the recommended AI level for the next mapping step
- whether the session appears to be:
  - initial map creation
  - targeted subsystem mapping
  - map maintenance after code changes
  - map cleanup / compression
  - complete for the current mapping scope

4. Read only enough additional map artifacts or repository structure to validate the proposed next
   step before presenting the startup gate.

Do not begin substantive repository inspection, deep subsystem analysis, or map artifact editing
before the startup gate is approved by the human.

---

## Startup Gate

After completing the startup sequence, stop and present a concise mapping proposal to the human.

The startup gate must include:

- the current mapping mode
- the proposed next mapping step
- a brief reason that step appears to be next
- the recommended AI level
- an explicit request for the human to proceed or redirect the session

Use a concise format such as:

```text
Mapping mode: Targeted subsystem mapping

Proposed next step:
Complete the `history` subsystem map, then evaluate whether `api_pub.md` and/or `api_ext.md`
are justified for that subsystem.

Why this appears next:
`map_state.md` identifies `history` as the active focus, and the current subsystem work is not yet
complete enough to move on.

Recommended AI level:
Thinking

Say `proceed` to continue, or redirect the mapping focus.
```

The mapping agent must wait for explicit human direction before continuing.

The human may:

- approve the proposed next step
- redirect to a different subsystem
- request map maintenance for a recent code change
- request cleanup or compression
- revise the mapping scope
- stop the session

---

## When the Current Mapping Scope Appears Complete

If the startup review does not reveal a clear next mapping step within the current scope, say so
plainly and stop.

Do not invent a new mapping objective merely to continue working.

Use a concise format such as:

```text
The current mapping scope appears complete.

I do not see an unfinished subsystem, deferred API-map decision, maintenance task, or compression task
that is clearly implied by the current map state.

You can direct me to:

- add a new subsystem to the mapping scope
- deepen or refresh an existing subsystem
- perform maintenance after recent code changes
- review compression or consistency across existing maps
```

Then wait for the human to choose the next direction.

---

## After the Human Proceeds

Once the human approves or redirects the next step:

1. Follow the applicable mapping workflow and editing rules in:

```text
.bonsai/maps/map_system.md
```

2. Read only the source, examples, tests, existing maps, and optional lookup artifacts needed for the
   approved mapping step.

3. Produce or update only the Bonsai map files justified by the approved work.

4. Update:

```text
.bonsai/maps/map_state.md
```

to reflect:

- what was completed
- the current mapping status
- unresolved uncertainties, if any
- the exact next mapping step
- the recommended AI level for the next session

5. If the completed work changes top-level routing, subsystem status, lookup artifacts, or other
   dependent map artifacts, update those files according to `map_system.md`.

---

## System-Control Files

Do not modify these files unless the human explicitly requests it:

```text
.bonsai/maps/map_prompt.md
.bonsai/maps/map_system.md
.bonsai/maps/map_repo.md
```

Ordinary mapping sessions maintain generated map artifacts and `map_state.md`.

---

## Output Style

Use:

- concise wording
- dense, practical content
- deterministic headings
- stable section ordering
- exact paths
- explicit uncertainty where needed
- no filler prose

When creating or updating files, return the full file contents in fenced Markdown blocks unless the
human asks for patches instead.
