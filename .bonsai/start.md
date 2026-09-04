# Bonsai Startup

This file is the repository-local Bonsai bootstrap. Keep startup read-only and small.

It is not a Bonsai Home entry point. Normal startup must begin from the target repository's local `.bonsai/start.md` anchor.

## Session Inputs

Retain the human's complete startup request as natural language. An explicit active-project request is session
identity; any remaining request is passed through unchanged after identity resolution. Do not require or invent a
startup command syntax.

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
2. **Bonsai Home:** A directory is a valid Bonsai standard for bootstrap when it contains readable
   `specification.md` and `prompts/implementation.md` files.
   - If `BONSAI_HOME` is defined and identifies a valid standard, use it.
   - Otherwise, if the repository-local `.bonsai` directory is a valid embedded standard, use it.
   - Otherwise stop and ask the human to configure or identify Bonsai Home. Report a defined but invalid
     `BONSAI_HOME`; do not search broadly for another installation, substitute a one-session path for the missing
     environment configuration, or persist a guessed location.
3. **Active project:** Resolve only immediate child directories of `<repository-home>/.bonsai/projects/`.
   - If the human explicitly named a project, use it only when that project directory exists. Otherwise stop and
     ask the human to correct the project or choose an available one. When multiple existing projects are offered
     as alternatives, present them in stable lexical order as numbered choices and accept the corresponding number
     as the selection.
   - Otherwise, use `main` when `projects/main/` exists.
   - Otherwise, if exactly one project directory exists, use it.
   - Otherwise, if several project directories exist, enumerate them in stable lexical order, present them as
     numbered choices, and ask the human to choose by number. Accept the corresponding number as the project
     selection; do not require the human to retype the project name.
   - Otherwise stop and surface project creation or project design as the required next action. Do not create
     project memory or invent durable design during bootstrap.

Keep repository home, Bonsai Home, active project, and the retained startup request as current-session context
only. Do not write a current-project pointer or store session identity in developer context, agent context, or
project memory.

## Hand Off

After all identity values are resolved:

1. read `<bonsai-home>/prompts/implementation.md`;
2. provide it the resolved Bonsai Home, repository home, active project, and retained natural-language startup
   request;
3. follow it as the implementation kernel.

Do not load requirements, architecture, maps, developer context, agent context, or specialized skills in this
bootstrap. Do not execute requested project, Bonsai Home, code-map, or implementation workflows here; preserve
the request for the implementation kernel, which must report any unavailable delegated workflow without claiming
success.
