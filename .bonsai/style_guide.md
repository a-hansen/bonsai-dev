# Global AI Engineering & Style Directives

Follow the standard conventions of the project's primary language and framework unless explicitly overridden by these instructions or the surrounding local code.

## 1. Instruction Priority & AI Behavior

When generating code, analyzing architecture, or refactoring, obey this strict priority hierarchy:

1. **Local Code Style:** Match the style, patterns, and naming of the existing file.
2. **Environment Constraints:** Strictly adhere to the version, linting, and logging rules of the target environment and framework.
3. **These Directives:** Obey the pragmatic rules defined below.
4. **Generic Patterns:** Treat generic enterprise patterns (SOLID, DRY) as advisory.

**AI Core Directives:**

* Do NOT default to generic enterprise patterns.
* Do NOT introduce unnecessary abstractions (interfaces, layers, patterns) unless they solve an
  immediate, tangible problem.
* If the surrounding code is simple and imperative, keep it simple and imperative.
* Explain trade-offs briefly if multiple viable options exist.

---

## 2. The Pragmatic Core (Architecture & Design)

* **Practicality over Purity:** Do not refactor just to "apply a principle."
* **Debuggability over Abstraction:** Keep data and control flow linear, easy to inspect, and easy
  to trace.
* **Composition over Inheritance:** Use when needed, but do not force it.
* **Acceptable Duplication:** Small duplication is preferable if it keeps the code simple and avoids
  premature generalization.

---

## 3. Default Coding Choices

- Use modern language features only when they improve clarity or reduce noise.
- Prefer simple control flow over complex functional pipelines when debugging would suffer.
- Fail fast; do not silently swallow errors. Follow the standard error-handling idioms of the target language.
- Keep names concise; avoid noise words.
- Test behavior, not implementation details. Prefer simple tests over heavy mocking.

---

## 4. The Final Gate

Before finalizing any code generation or refactor, verify:

* [ ] Is this simple?
* [ ] Is this easy to debug?
* [ ] Does this perfectly match the surrounding local code style?
* [ ] Is this free of over-engineering?

If any answer is NO, simplify the solution before outputting.