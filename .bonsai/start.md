# Bonsai Startup

This file is the repository-local Bonsai bootstrap. Keep startup read-only and small.

## Session Inputs

Retain the human's complete startup request as natural language. An explicit active-project request is session
identity; any remaining request is passed through unchanged after identity resolution. Do not require or invent a
startup command syntax.

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
     ask the human to correct the project or choose an available one.
   - Otherwise, use `main` when `projects/main/` exists.
   - Otherwise, if exactly one project directory exists, use it.
   - Otherwise, if several project directories exist, list them and ask the human to choose one.
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
