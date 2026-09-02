# Bonsai Home

## Purpose

Create or safely populate the reusable Bonsai Home already identified by the environment, starting from a valid
embedded Bonsai standard. Preserve repository-local memory and return control through normal startup identity
resolution.

This is a bounded migration workflow, not an environment-configuration framework or a general installation and
synchronization mechanism.

## When to Load

Load this skill only when the human:

- explicitly requests Create Bonsai Home at startup; or
- selects Create Bonsai Home from **See more options** while the current session is using Embedded Bonsai.

The explicit request or menu selection authorizes creation or safe population of the configured target. It does
not authorize changes to shell startup files, machine configuration, credentials, developer context, agent
context, repository project memory, or an ambiguous existing target.

Retain the invoking gate and current session's repository home and active project so they can be resolved again
after the workflow.

## Required Inputs

Use only:

- the resolved repository home;
- the current embedded standard at `<repository-home>/.bonsai/`;
- `BONSAI_HOME` read from the actual process environment;
- the configured target's existence and content; and
- the invoking gate.

Do not accept a path supplied only in conversation as a substitute for `BONSAI_HOME`. Do not search broadly,
infer a target from a user-profile or home-directory convention, or retrieve a remembered path from developer or
agent context.

## Source and Environment Validation

Complete all validation before writing anything.

1. Confirm the current session is using the repository-local embedded standard. If a distinct valid Bonsai Home
   is already active, report that Create Bonsai Home is not applicable and return to the invoking gate.
2. Confirm the embedded source contains readable `../specification.md` and `prompts/implementation.md`. If it does
   not, stop: an invalid embedded source must not seed a reusable home.
3. Read `BONSAI_HOME` from the environment. If it is undefined or blank, stop with no writes and tell the human
   to configure it in the environment before retrying. Do not offer a session-only path.
4. Resolve the configured path using host path semantics without searching for alternatives. If it identifies
   the embedded `.bonsai` itself, report that it does not establish a distinct reusable home and return to the
   invoking gate without writing.
5. Confirm the target can be addressed as a directory: it may be absent, empty, or safely compatible as defined
   below. A non-directory target, inaccessible target, unsafe path, or unresolved path error is a blocker.

Never print or persist unrelated environment values while validating `BONSAI_HOME`.

## Shared Standard Boundary

Populate only distribution-owned standard artifacts from the embedded source:

```text
specification.md
README.md
prompts/
skills/
templates/
```

Include another source artifact only when the current specification explicitly identifies it as part of the
shared standard rather than repository-owned memory. Do not assume every entry under the embedded `.bonsai/`
belongs in Bonsai Home.

In particular, do not copy or move:

```text
start.md
developer_context.md
agent_context.md
projects/
maps/
```

`start.md` remains the repository-local bootstrap. Developer and agent context remain at their existing scopes.
Project memory always remains under `<repository-home>/.bonsai/projects/`. Embedded maps remain repository-local;
map creation or migration belongs to the code-map workflow, not this skill.

Do not delete, prune, or rewrite the embedded source after copying. It may remain as the repository's fallback
standard while the reusable home is validated.

## Target Preflight

Build the complete source-to-target copy set before mutation and inspect every destination.

A target is safely compatible only when:

- the target directory is absent or is an existing directory;
- every destination is absent or has content identical to its source;
- required directory/file types agree; and
- an existing managed directory (`prompts/`, `skills/`, or `templates/`) contains no additional entry whose
  ownership or compatibility is unclear.

Existing content outside the managed copy set may remain untouched. Never treat an existing
`developer_context.md`, `agent_context.md`, or `maps/` as an instruction to replace, merge, or import context.

If any destination differs, a file blocks a required directory, a directory blocks a required file, or managed
content cannot be reconciled unambiguously, stop before all writes. Report the conflicting target paths and ask
the human to resolve or explicitly direct the conflict. Do not overwrite, merge, rename, back up, or delete the
content automatically.

## Authorized Population

After the complete preflight succeeds:

1. Create the configured target directory when absent.
2. Create required managed directories.
3. Copy missing shared-standard files while preserving their relative paths and content.
4. Leave byte-identical destinations and all content outside the managed copy set unchanged.
5. Create reusable context or map directories only when the current standard actually requires their existence;
   do not create placeholder context files or migrate repository-local content.

Use ordinary host filesystem operations. An optional helper may perform these same checks and writes for
convenience, but the workflow must remain executable without one.

If population fails, stop and report exactly which configured target operation failed. Do not claim the target is
current or valid, and do not compensate by changing environment configuration or repository memory.

## Result Validation

Before treating the configured home as session identity:

1. confirm the target contains readable `../specification.md` and `prompts/implementation.md`;
2. confirm every artifact in the copy set is present with the source content;
3. confirm repository-local `start.md`, developer context, agent context, maps, and project memory were not moved,
   copied, or modified by this workflow; and
4. confirm `BONSAI_HOME` still resolves to the validated target.

Failure of any check leaves the current session on the embedded standard and returns a concrete blocker. Do not
store the target path in context as a fallback.

## Return Through Startup

After successful validation:

1. mark only the current Create Bonsai Home action as handled so it is not replayed;
2. preserve any remaining natural-language startup request and the current-session active-project request;
3. reread `<repository-home>/.bonsai/start.md` and resolve Bonsai Home, repository home, and active project again;
4. require normal resolution to select the configured home as the preferred valid standard;
5. load the implementation kernel from that newly resolved home; and
6. recompute and restore the invoking gate with refreshed identity and choices.

If normal startup does not select the new home, stop and report the identity-resolution mismatch. Do not bypass
`start.md` with a direct one-session standard path. Replace the invoking gate only when refreshed startup state
requires a different mandatory gate.

At the refreshed gate, report the configured target, whether it was created or safely populated, that repository
memory remained local, and any environment setup still needed for future processes to receive `BONSAI_HOME`.
Explain that setup without editing shell startup files or machine configuration.

## Stop Conditions

Stop without target mutation when:

- `BONSAI_HOME` is undefined or blank;
- the current source is not a valid embedded standard;
- a distinct valid Bonsai Home is already active;
- the configured path is the embedded standard itself;
- the target path is unsafe, inaccessible, or not a directory;
- target preflight finds conflicting or ambiguous content; or
- safe completion would require modifying environment configuration, repository-local memory, context, or
  approved standard truth.

After a population or validation failure, report the partial target state honestly and return to the invoking
gate when safe. Never report creation as successful until result validation and startup re-resolution both pass.
