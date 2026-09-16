# Bonsai Startup

Repository-local, read-only Bonsai bootstrap. It is not a Bonsai Home entry point. Normal startup begins at the target repository's local `.bonsai/start.md`.

## Session Inputs

- Retain the human's complete startup request as natural language. An explicit active project or map is session identity; after resolving identity, pass the remaining request through unchanged. Do not require or invent startup command syntax.
- At most one workspace may be explicit. If both project and map are named, stop and ask the human to choose; do not choose precedence.
- A repository-level workflow needing no active workspace, such as **Manage Code Maps** or **Create Bonsai Home**, leaves workspace identity unresolved unless explicitly supplied. Preserve the request for the implementation kernel; do not force ordinary project selection first.

## Bootstrap Location Guard

Before deriving repository home, verify this is the target repository's local `.bonsai/start.md`. `BONSAI_HOME` supplies the Bonsai standard only after repository identity is established; never use it as repository anchor.

If startup was explicitly directed through `$BONSAI_HOME/start.md` or an equivalent resolved reusable Bonsai Home `start.md`:

- stop before deriving repository home;
- do not ask for confirmation or treat the parent of `BONSAI_HOME` as a repository;
- explain that startup must begin from the target repository and provide:

```text
Read .bonsai/start.md and follow its instructions.
```

A repository-local embedded installation remains valid even when its `.bonsai` also serves as Bonsai Home. The guard rejects a reusable Bonsai Home as repository anchor, not a repository-local embedded standard.

## Resolve Identity

Use host tools for deterministic facts when available.

1. **Repository home:** Parent of the `.bonsai` containing this file. Never substitute process working directory when they differ.
2. **Bonsai Home:** Bootstrap-valid iff `specification.md` and `prompts/implementation.md` exist and are accessible. Check existence/accessibility only; do not read `specification.md`.
   - Valid `BONSAI_HOME` defined: use it.
   - Otherwise, valid repository-local `.bonsai`: use it as embedded standard.
   - Otherwise stop and ask the human to configure or identify Bonsai Home. Report a defined but invalid `BONSAI_HOME`; do not broadly search for another installation, substitute a one-session path for missing environment configuration, or persist a guessed location.
3. **Workspace candidates:** Enumerate only immediate child directories of `<repository-home>/.bonsai/projects/` and `<repository-home>/.bonsai/maps/`, each in stable lexical order. Keep types separate. Never infer workspaces from unrelated files or generated map output.
4. **Active workspace:** Resolve at most one:
   - Explicit project: select `<repository-home>/.bonsai/projects/<project>` only if that immediate directory exists; otherwise stop and ask for a corrected name or choice from available projects.
   - Explicit map: select `<repository-home>/.bonsai/maps/<map>` only if that immediate directory exists; otherwise stop and ask for a corrected name or choice from available maps.
   - No explicit workspace + repository-level workflow needing none: leave unresolved; continue to handoff.
   - Otherwise use project-oriented startup: `projects/main` if present; else sole project candidate; else, if several, stop and present numbered choices in stable lexical order and accept the corresponding number; else leave unresolved for implementation-kernel repository-entry routing.
   - Never infer a map from unqualified startup merely because map candidates exist.

If an explicit workspace is invalid, present only same-type candidates in stable lexical order. Never substitute `main`, a sole candidate, or the other workspace type.

## Load the Workspace Entry

If a workspace is selected, require and read only `<active-workspace-home>/workspace.md` before handoff.

A bootstrap-valid entry has one unambiguous `Type` and one unambiguous `Route`, matching the selected directory kind and an approved pair:

| Type | Route |
| --- | --- |
| `project` | `Project workspace behavior` |
| `map` | `Map workspace behavior` |

Stop clearly if the entry is missing/inaccessible; either declaration is absent/conflicting; `Type` mismatches directory kind; `Route` mismatches `Type`; or `Type` is unsupported. Do not guess around an invalid entry or fall back to another workspace.

Keep repository home, Bonsai Home, active workspace type/name/home, loaded workspace entry, project/map candidates, and retained startup request as current-session context only. Do not write an active-workspace pointer or store session identity in developer context, agent context, project memory, or map memory.

During bootstrap, do not read `agent_plan.md`, `agent_state.md`, requirements, architecture, map calibration, generated maps, detailed plans, developer context, agent context, or specialized skills.

## Hand Off

After repository home and Bonsai Home are resolved, and any selected workspace entry is loaded and validated:

1. Read `<bonsai-home>/prompts/implementation.md`.
2. Provide resolved Bonsai Home, repository home, optional active workspace type/name/home, loaded workspace entry when applicable, project/map candidates, and retained natural-language startup request.
3. Follow it as the implementation kernel.

With no active workspace, pass unresolved identity and candidates so the implementation kernel owns repository-entry routing. Do not manufacture workspace execution readiness in bootstrap.

Do not execute requested project, map, Bonsai Home, code-map, or implementation workflows here. Preserve the request for the implementation kernel; it must report unavailable delegated workflows without claiming success.
