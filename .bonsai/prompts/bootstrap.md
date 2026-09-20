# Bonsai Startup

Read-only Bonsai bootstrap. Repository home and Bonsai Home are already resolved by `.bonsai/start.md`.

## Session Inputs

* Retain the human's complete startup request as natural language. An explicit active project or map is session identity; after resolving identity, pass the remaining request through unchanged. Do not require or invent startup command syntax.
* At most one workspace may be explicit. If both project and map are named, stop and ask the human to choose; do not choose precedence.
* A repository-level workflow needing no active workspace, such as **Manage Code Maps**, leaves workspace identity unresolved unless explicitly supplied. Preserve the request for the implementation kernel; do not force ordinary project selection first.

## Resolve Workspace

Resolve only as much workspace information as the current startup requires. A workspace is established only when its immediate directory exists and both `agent_plan.md` and `agent_state.md` are accessible. The containing `projects/` or `maps/` path determines workspace type. Never infer a workspace from unrelated files or generated map output.

1. **Explicit workspace:** If a project or map is explicitly named, resolve that workspace directly without enumerating other projects or maps.

    * Explicit project: validate `<repository-home>/.bonsai/projects/<project>` as an established project workspace. If valid, select it and continue. If absent or incomplete, enumerate only established immediate project children in stable lexical order, report the problem, and ask for a corrected name or choice.
    * Explicit map: validate `<repository-home>/.bonsai/maps/<map>` as an established map workspace. If valid, select it and continue. If absent or incomplete, enumerate only established immediate map children in stable lexical order, report the problem, and ask for a corrected name or choice.
    * Never substitute `main`, a sole candidate, or the other workspace type for invalid explicit identity.

2. **No explicit workspace:**

    * Repository-level workflow needing no active workspace: leave identity unresolved and continue to handoff without enumerating workspace candidates merely for startup.
    * Otherwise use project-oriented startup. First validate `projects/main` directly; if established, select it without enumerating other workspaces. Otherwise enumerate only established immediate project children in stable lexical order: select the sole candidate; if several exist, stop and present numbered choices and accept the corresponding number; if none exist, leave identity unresolved for implementation-kernel repository-entry routing.
    * Never enumerate or infer map workspaces for ordinary unqualified project startup merely because map directories exist.

Workspace candidates are therefore optional session context: retain only candidates actually enumerated for selection, correction, or repository-entry routing.

## Validate the Active Workspace

If a workspace is selected, its structural path is authoritative for type:

```text
<repository-home>/.bonsai/projects/<project>/ → project
<repository-home>/.bonsai/maps/<map>/         → map
```

Require both `<active-workspace-home>/agent_plan.md` and `<active-workspace-home>/agent_state.md` to exist and be accessible. Their presence establishes the directory as a resumable workspace; bootstrap checks existence/accessibility only and does not read them.

Stop clearly if the selected directory is absent or either required execution-memory artifact is missing/inaccessible. Do not guess around an incomplete workspace, infer type from workspace contents, or fall back to another workspace.

Keep repository home, Bonsai Home, active workspace type/name/home, any workspace candidates actually enumerated, and retained startup request as current-session context only. Do not write an active-workspace pointer or store session identity in developer context, agent context, project memory, or map memory.

During bootstrap, do not read `agent_plan.md`, `agent_state.md`, requirements, architecture, map calibration, generated maps, detailed plans, developer context, agent context, or specialized skills.

## Hand Off

After any selected workspace is structurally identified and validated:

1. Read `<bonsai-home>/prompts/implementation.md`.
2. Provide resolved Bonsai Home, repository home, optional active workspace type/name/home, any workspace candidates actually enumerated, and retained natural-language startup request.
3. Follow it as the implementation kernel.

With no active workspace, pass unresolved identity and any candidates already enumerated so the implementation kernel owns repository-entry routing. Do not manufacture workspace execution readiness in bootstrap.

Do not execute requested project, map, code-map, repository-level, or implementation workflows here. Preserve the request for the implementation kernel; it must report unavailable delegated workflows without claiming success.
