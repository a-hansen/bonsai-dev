# Bonsai Start

This file is the repository-local Bonsai entry point.

The repository home is the parent of the `.bonsai` directory containing this file.

Resolve Bonsai Home:

- If `BONSAI_HOME` is defined, require `$BONSAI_HOME/prompts/bootstrap.md`.
- Otherwise, require `.bonsai/prompts/bootstrap.md` in this repository.
- If the required bootstrap file is missing or inaccessible, stop and report the configuration problem. Do not search for another Bonsai installation or guess a replacement.

Use ordinary environment and filesystem capabilities for these checks. Do not generate scripts or compound shell commands merely to locate or validate Bonsai Home.

Read the resolved `prompts/bootstrap.md` and follow it, providing:
- repository home;
- resolved Bonsai Home;
- the human's complete startup request unchanged.