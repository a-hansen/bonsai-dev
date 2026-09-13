# Bonsai Startup

This file is the repository-local Bonsai bootstrap. Keep startup read-only and small.

It is not a Bonsai Home entry point. Normal startup must begin from the target repository's local `.bonsai/start.md` anchor.

## Session Inputs

Retain the human's complete startup request as natural language. An explicit active-project or active-map request is
session identity; any remaining request is passed through unchanged after identity resolution. Do not require or
invent a startup command syntax.

Only one active workspace may be explicit. If the request names both an active project and an active map, stop and
ask the human to choose one; do not guess which identity takes precedence.

A request for a repository-level workflow that does not require an active workspace, such as **Manage Code Maps**
or **Create Bonsai Home**, leaves active workspace identity unresolved unless the human also explicitly supplied
one. Preserve the request for the implementation kernel rather than forcing ordinary project selection first.

## Bootstrap Location Guard

Before deriving repository home, verify that the startup request is using this file as the target repository's local
`.bonsai/start.md` bootstrap. `BONSAI_HOME` supplies the Bonsai standard after repository identity is established; it
must not be used as a substitute repository anchor.

If the human explicitly directed startup through `$BONSAI_HOME/start.md`, or through an equivalent resolved path to
the reusable Bonsai Home copy of `start.md`, stop before deriving repository home. Do not ask for confirmation and do
not treat the parent of `BONSAI_HOME` as a repository. Explain that Bonsai startup must begin from the target
repository and provide the canonical instruction:

```text
Read .bonsai/start.md and follow its instructions.
```

An embedded Bonsai installation remains valid because its `start.md` is the repository-local `.bonsai/start.md`
anchor. The guard rejects using a reusable Bonsai Home as the repository anchor; it does not reject a repository-local
embedded standard merely because that same `.bonsai` directory also serves as Bonsai Home.

## Resolve Identity

Resolve deterministic facts with host tools when available.

1. **Repository home:** Treat the parent of the `.bonsai` directory containing this file as repository home. Do
   not infer repository home from the process working directory when the two differ.
2. **Bonsai Home:** A directory is a valid Bonsai standard for bootstrap when specification.md and 
   prompts/implementation.md exist and are accessible. Check only their existence/accessibility; do 
   not read specification.md during bootstrap.
   - If `BONSAI_HOME` is defined and identifies a valid standard, use it.
   - Otherwise, if the repository-local `.bonsai` directory is a valid embedded standard, use it.
   - Otherwise stop and ask the human to configure or identify Bonsai Home. Report a defined but invalid
     `BONSAI_HOME`; do not search broadly for another installation, substitute a one-session path for the missing
     environment configuration, or persist a guessed location.
3. **Workspace candidates:** Enumerate only immediate child directories of
   `<repository-home>/.bonsai/projects/` and `<repository-home>/.bonsai/maps/`, each in stable lexical order. Keep
   the two concrete types separate. Do not infer a workspace from unrelated files or generated map output.
4. **Active workspace:** Resolve at most one concrete workspace using these rules:
   - If the human explicitly named an active project, select
     `<repository-home>/.bonsai/projects/<project>` only when that immediate project directory exists. Otherwise
     stop and ask the human to correct the name or choose from the available projects.
   - If the human explicitly named an active map, select `<repository-home>/.bonsai/maps/<map>` only when that
     immediate map directory exists. Otherwise stop and ask the human to correct the name or choose from the
     available maps.
   - If no workspace is explicit and the retained request directly invokes a repository-level workflow that does
     not require one, leave active workspace unresolved and continue to handoff.
   - Otherwise preserve ordinary project-oriented startup: select `projects/main` when it exists; if not, select
     the sole project candidate; if several projects exist, stop and present them as numbered choices in stable
     lexical order, accepting the corresponding number as the selection; if no projects exist, leave active
     workspace unresolved for the implementation kernel's repository-entry routing.
   - Never infer a map from an unqualified startup merely because one or more map directories exist.

When an explicit workspace does not exist and alternatives are presented, list only candidates of that same
concrete type in stable lexical order. Do not silently substitute `main`, a sole candidate, or a workspace of the
other type for an invalid explicit identity.

## Load the Workspace Entry

When a workspace was selected, require and read only `<active-workspace-home>/workspace.md` before implementation
handoff.

The entry is valid for bootstrap only when it has one unambiguous `Type` and one unambiguous `Route` declaration
matching both the selected directory kind and one of these two approved pairs:

| Type | Route |
| --- | --- |
| `project` | `Project workspace behavior` |
| `map` | `Map workspace behavior` |

Stop clearly when the entry is missing or inaccessible, a required declaration is absent or conflicting, the type
does not match the selected directory kind, the route does not match the type, or the type is unsupported. Do not
guess around an invalid entry or fall back to another workspace.

Keep repository home, Bonsai Home, active workspace type/name/home, the loaded workspace entry, project and map
candidates, and the retained startup request as current-session context only. Do not write an active-workspace
pointer or store session identity in developer context, agent context, project memory, or map memory.

Do not read `agent_plan.md`, `agent_state.md`, requirements, architecture, map calibration, generated maps, detailed
plans, developer context, agent context, or specialized skills during bootstrap.

## Hand Off

After repository home and Bonsai Home are resolved, and after any selected workspace entry is loaded and validated:

1. read `<bonsai-home>/prompts/implementation.md`;
2. provide it the resolved Bonsai Home, repository home, optional active workspace type/name/home, loaded workspace
   entry when applicable, project and map candidates, and retained natural-language startup request;
3. follow it as the implementation kernel.

When no workspace is active, supply the unresolved identity and candidates so the implementation kernel can own
repository-entry routing. Do not manufacture workspace execution readiness in bootstrap.

Do not execute requested project, map, Bonsai Home, code-map, or implementation workflows here. Preserve the request
for the implementation kernel, which must report any unavailable delegated workflow without claiming success.
