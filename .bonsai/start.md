# Bonsai Startup

This file is the repository-local Bonsai bootstrap. Keep startup read-only and small.

It is not a Bonsai Home entry point. Normal startup must begin from the target repository's local `.bonsai/start.md` anchor.

## Session Inputs

Retain the human's complete startup request as natural language. An explicit active-project request is session
identity; any remaining request is passed through unchanged after identity resolution. Do not require or invent a
startup command syntax.

When no active project is explicit, do not silently select `main` or a sole project. Preserve repository-level
entry state so the implementation kernel can present project choices alongside repository-level workflows such as
**Manage Code Maps**.

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
3. **Project candidates and active project:** Enumerate only immediate child directories of
   `<repository-home>/.bonsai/projects/` in stable lexical order.
   - If the human explicitly named a project, use it only when that project directory exists. Otherwise stop and
     ask the human to correct the project or choose an available one. When multiple existing projects are offered
     as alternatives, present them in stable lexical order as numbered choices and accept the corresponding number
     as the selection.
   - If no project was explicitly named, leave active project unresolved. Do not auto-select `main`, a sole
     project, or any other candidate. Preserve the enumerated project candidates for the repository entry gate.
   - No project directory is required for repository-level workflows that do not require project memory.

Keep repository home, Bonsai Home, the optional active project, available project candidates, and the retained
startup request as current-session context only. Do not write a current-project pointer or store session identity
in developer context, agent context, or project memory.

## Hand Off

After repository home and Bonsai Home are resolved:

1. read `<bonsai-home>/prompts/implementation.md`;
2. provide it the resolved Bonsai Home, repository home, optional active project, available project candidates,
   and retained natural-language startup request;
3. follow it as the implementation kernel.

Do not load requirements, architecture, maps, developer context, agent context, or specialized skills in this
bootstrap. Do not execute requested project, Bonsai Home, code-map, or implementation workflows here; preserve
the request for the implementation kernel, which must report any unavailable delegated workflow without claiming
success.
