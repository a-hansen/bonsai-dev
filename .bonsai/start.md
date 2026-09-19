# Bonsai Startup

Repository-local, read-only Bonsai bootstrap. It is not a Bonsai Home entry point. Normal startup begins at the target repository's local `.bonsai/start.md`.

## Session Inputs

- Retain the human's complete startup request as natural language. An explicit active project or map is session identity; after resolving identity, pass the remaining request through unchanged. Do not require or invent startup command syntax.
- At most one workspace may be explicit. If both project and map are named, stop and ask the human to choose; do not choose precedence.
- A repository-level workflow needing no active workspace, such as **Manage Code Maps**, leaves workspace identity unresolved unless explicitly supplied. Preserve the request for the implementation kernel; do not force ordinary project selection first.

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

Resolve Bonsai Home, repository identity, and workspace candidates using ordinary read-only host filesystem/environment capabilities when available. Do not use a generated shell script or compound shell command merely to perform existence, readability, or directory-enumeration checks.

1. **Repository home:** Parent of the `.bonsai` containing this file. Never substitute process working directory when they differ.
2. **Bonsai Home:** Bootstrap-valid iff `prompts/implementation.md` exists and is accessible.
    - Valid `BONSAI_HOME` defined: use it.
    - Otherwise, valid repository-local `.bonsai`: use it as embedded standard.
    - Otherwise stop and ask the human to configure or identify Bonsai Home. Report a defined but invalid `BONSAI_HOME`; do not broadly search for another installation, substitute a one-session path for missing environment configuration, or persist a guessed location.
3. **Workspace candidates:** Enumerate only established immediate child workspaces of `<repository-home>/.bonsai/projects/` and `<repository-home>/.bonsai/maps/`, each in stable lexical order. A child is established only when both `agent_plan.md` and `agent_state.md` exist and are accessible. Keep types separate. The containing `projects/` or `maps/` path determines workspace type. Never infer a workspace from unrelated files or generated map output.
4. **Active workspace:** Resolve at most one:
   - Explicit project: select `<repository-home>/.bonsai/projects/<project>` only if that immediate directory is an established project workspace; otherwise stop and report whether it is absent or present but incomplete, then ask for a corrected name or choice from available established projects.
   - Explicit map: select `<repository-home>/.bonsai/maps/<map>` only if that immediate directory is an established map workspace; otherwise stop and report whether it is absent or present but incomplete, then ask for a corrected name or choice from available established maps.
   - No explicit workspace + repository-level workflow needing none: leave unresolved; continue to handoff.
   - Otherwise use project-oriented startup: `projects/main` if present; else sole project candidate; else, if several, stop and present numbered choices in stable lexical order and accept the corresponding number; else leave unresolved for implementation-kernel repository-entry routing.
   - Never infer a map from unqualified startup merely because map candidates exist.

If an explicit workspace is invalid, present only same-type candidates in stable lexical order. Never substitute `main`, a sole candidate, or the other workspace type.

## Validate the Active Workspace

If a workspace is selected, its structural path is authoritative for type:

```text
<repository-home>/.bonsai/projects/<project>/ → project
<repository-home>/.bonsai/maps/<map>/         → map
```

Require both `<active-workspace-home>/agent_plan.md` and `<active-workspace-home>/agent_state.md` to exist and be accessible. Their presence establishes the directory as a resumable workspace; bootstrap checks existence/accessibility only and does not read them.

Stop clearly if the selected directory is absent or either required execution-memory artifact is missing/inaccessible. Do not guess around an incomplete workspace, infer type from workspace contents, or fall back to another workspace.

Keep repository home, Bonsai Home, active workspace type/name/home, project/map candidates, and retained startup request as current-session context only. Do not write an active-workspace pointer or store session identity in developer context, agent context, project memory, or map memory.

During bootstrap, do not read `agent_plan.md`, `agent_state.md`, requirements, architecture, map calibration, generated maps, detailed plans, developer context, agent context, or specialized skills.

## Hand Off

After repository home and Bonsai Home are resolved, and any selected workspace is structurally identified and validated:

1. Read `<bonsai-home>/prompts/implementation.md`.
2. Provide resolved Bonsai Home, repository home, optional active workspace type/name/home, project/map candidates, and retained natural-language startup request.
3. Follow it as the implementation kernel.

With no active workspace, pass unresolved identity and candidates so the implementation kernel owns repository-entry routing. Do not manufacture workspace execution readiness in bootstrap.

Do not execute requested project, map, code-map, repository-level, or implementation workflows here. Preserve the request for the implementation kernel; it must report unavailable delegated workflows without claiming success.
