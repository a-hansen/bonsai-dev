# Bonsai Repository Mapping Prompt

## Purpose

We have been discussing a repository that will use Bonsai code maps.

Transition into the role of a strict Repository Cartographer and Technical Writer. Your task is to
synthesize this conversation into a clean, durable repository-calibration document for future
AI mapping sessions.

The output will become:

```text
.bonsai/maps/map_repo.md
```

This file is human-owned guidance for mapping agents. It should capture what a knowledgeable
developer knows about the repository before an AI begins scanning source.

---

## Output Protocol

Generate exactly one Markdown code block containing the full contents of:

```text
map_repo.md
```

Do not generate commentary before or after the code block.

Use the provided `map_repo_template.md` structure exactly. Fill it densely where the conversation
supports it. Remove placeholder examples that do not apply.

---

## Synthesis Rules

### 1. No hallucinations

Base the output strictly on:

* our conversation
* any repository facts the user provided
* any attached reference materials the user explicitly supplied for this synthesis

Do not invent:

* source roots
* module names
* build tooling
* runtime surfaces
* extension seams
* owner priorities
* representative examples
* mapping scope boundaries

If something is unknown, leave it as an open question or omit it where appropriate.

---

### 2. Preserve human judgment

`map_repo.md` exists partly to preserve repository-owner judgment that source inspection alone may
not reveal.

Capture statements such as:

* which areas matter most
* which areas should not be over-weighted
* which examples best reflect real usage
* which apparent architectural centers are actually low-value for day-to-day work
* which small areas are disproportionately important
* which code paths are historical, generated, misleading, or stale
* which patterns future mapping agents should pay special attention to
* which areas the current mapping effort is actually intended to cover

Do not dilute these judgments into generic prose.

---

### 3. Separate repository facts from mapping biases

Keep distinct:

* **Repository shape:** source roots, modules, runtime surfaces, packaging units
* **Owner weighting:** what deserves mapping priority
* **Intended mapping scope:** what should receive mapping artifacts during this effort
* **Calibration-only areas:** what may be inspected as supporting evidence without becoming its own mapping target
* **Out-of-scope areas:** what should not be mapped unless the human expands scope
* **Calibration sources:** what code reflects practical usage
* **Architectural biases:** how mapping agents should interpret the repo
* **Oddities / exceptions:** what may mislead outsiders

---

### 4. Define the intended mapping scope

When synthesizing `map_repo.md`, identify the intended scope of the current mapping effort.

Separate:

1. **In Scope for This Mapping Effort**

    * Areas that should receive actual Bonsai mapping artifacts

2. **Calibration-Only Areas**

    * Areas that may be inspected to validate patterns, confirm real usage, or provide representative
      examples
    * These should not receive their own subsystem maps or API maps unless scope is explicitly expanded

3. **Out of Scope Unless Explicitly Requested**

    * Areas the mapping effort should not turn into mapping artifacts during the current effort

Treat this as a scope boundary, not merely a priority hint.

If the conversation provides owner priorities but not a clear mapping boundary, make a reasonable
proposal based on the discussion rather than silently treating the entire repository as in scope.

If the intended mapping scope remains ambiguous, record that ambiguity under
**Open Repository-Specific Questions** rather than broadening scope by assumption.

---

### 5. Prefer concise durable guidance

Write for future AI mapping sessions, not for marketing or onboarding documentation.

Use:

* compact bullets
* exact paths when known
* precise domain terms
* short reasons for prioritization
* explicit confidence labels where appropriate

Avoid:

* filler prose
* sweeping generalizations
* long tutorials
* repeated restatement of the same idea

---

### 6. Identify mapping-relevant unknowns

Use **Open Repository-Specific Questions** for gaps that would materially affect future mapping.

Good questions include:

* uncertain source-root boundaries
* unclear extension surfaces
* uncertainty about which examples are most representative
* ambiguity over which modules deserve priority
* ambiguity over the intended mapping scope
* known repo areas whose role is not yet understood

Do not use open questions for trivial omissions.

---

## Inputs

The user will provide:

1. A discussion of the repository and how it should be mapped
2. The blank template:

```text
.bonsai/maps/templates/map_repo_template.md
```

Use those inputs to produce:

```text
map_repo.md
```