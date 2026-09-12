# Bonsai Testbed Requirements

## Purpose

Bonsai Testbed is a deliberately trivial software project used to exercise Bonsai workflows and lifecycle behavior
with minimal source inspection, implementation effort, and token usage.

The software itself has no production purpose. The roadmap is the primary test harness.

## Goals

- Keep implementation work tiny, deterministic, and fast.
- Exercise real Bonsai planning, execution, review, handoff, and fresh-session lifecycle boundaries.
- Make lifecycle failures easy to distinguish from software-development complexity.
- Allow new Bonsai workflow scenarios to be added over time without turning the product into a realistic application.

## Product Behavior

The project uses a tiny Python module and standard-library tests.

The initial behaviors are intentionally simple:

1. A `message()` function can return a deterministic string.
2. A later trivial change can add another deterministic function.
3. A contract-first phase uses a text file whose complete contract content is:

   `BONSAI TESTBED CONTRACT v1`

4. Pass B of that contract-first phase makes `message()` return the approved contract string.
5. A final trivial phase adds one more deterministic behavior.

## Constraints

- Use Python standard library only.
- Keep source and tests as small as practical.
- Do not introduce packages, frameworks, services, databases, networking, configuration systems, or unnecessary abstractions.
- Prefer a few obvious functions and direct tests over architectural realism.
- Do not make the application more sophisticated merely to make implementation work appear substantive.
- Human review surfaces should be intentionally cheap to understand.
- New Bonsai scenarios may extend the roadmap later, but application complexity should remain minimal.

## Validation

Behavior should be validated with the smallest practical standard-library test suite.

The expected normal test command is:

```text
python -m unittest -q
```

## Out of Scope

- Production usefulness.
- Performance work.
- Packaging or deployment.
- External dependencies.
- Realistic domain modeling.
- Architecture intended for reuse outside the testbed.
