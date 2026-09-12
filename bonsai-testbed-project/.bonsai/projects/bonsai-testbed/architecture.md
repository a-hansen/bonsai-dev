# Bonsai Testbed Architecture

## Overview

Bonsai Testbed is intentionally flat.

Its target implementation is a tiny Python module plus a tiny standard-library test module and, during the
contract-first phase, one plain-text contract artifact.

Conceptually:

```text
repository root
├── testbed.py
├── test_testbed.py
└── contract.txt        # introduced by the contract-first phase
```

## Source

`testbed.py` contains only the trivial deterministic functions required by the approved roadmap.

Use direct module-level functions unless an approved future test scenario specifically requires another shape.

## Tests

`test_testbed.py` uses Python's standard `unittest` library.

Tests should directly verify the tiny observable behaviors required by the roadmap. Test helpers, fixtures, and
support infrastructure should be avoided unless a future Bonsai scenario explicitly needs them.

## Contract Surface

The initial contract-first lifecycle scenario uses `contract.txt` as the durable review surface.

Its approved content is exactly:

```text
BONSAI TESTBED CONTRACT v1
```

The contract exists to exercise Bonsai's two-pass contract lifecycle, not to model a realistic protocol or API.

## Dependencies

Python standard library only.

## Architectural Guardrail

Application complexity is intentionally undesirable. If a proposed implementation structure is more complicated
than necessary to exercise the Bonsai scenario, prefer the simpler structure.
