# Bonsai Testbed Agent Plan

## Roadmap Status

- Body of work: Active
- Current phase: Phase 1
- Execution readiness: Phase planning required

## Roadmap

### Phase 1 - Initial Trivial Implementation

Status: Pending

Create the minimal Python implementation and tests.

Target behavior:

```text
message() -> "hello"
```

Execution mode: Single-pass Implementation.

Workflow test fixture: for Phase 1 execution only, treat the approved implementation step as if it has these
simulated execution characteristics:

- it mutates external state;
- rollback would be unusually difficult.

These characteristics exist only to exercise Bonsai workflow routing. The actual Phase 1 implementation remains
the same trivial local Python change. Apply the simulated characteristics wherever execution mechanics or risk are
evaluated, and do not carry them into later phases.

A reviewed Phase 1 detailed plan is required before substantive implementation because this is the project's
initial phase.

### Phase 2 - Trivial Follow-Up Change

Status: Pending

Add one deterministic behavior:

```text
status() -> "ready"
```

Execution mode: Single-pass Implementation.

Keep the change deliberately small. A later detailed phase plan is not expected unless execution reality shows
that one is genuinely useful.

### Phase 3 - Contract-First Lifecycle

Status: Pending

Exercise a real two-pass contract-first phase with minimal implementation cost.

Pass A establishes the durable review surface:

```text
contract.txt
```

with exactly:

```text
BONSAI TESTBED CONTRACT v1
```

and the smallest useful test expectation for the implementation beneath it.

Stop for contract review.

After contract approval, Pass B changes:

```text
message() -> "BONSAI TESTBED CONTRACT v1"
```

and makes the approved tests pass.

Execution mode: Two-pass contract-first.

### Phase 4 - Final Trivial Change

Status: Pending

Add one final deterministic behavior:

```text
complete() -> True
```

Execution mode: Single-pass Implementation.

This phase intentionally remains after Phase 3 so completion of the contract-first phase cannot legitimately be
confused with completion of the current body of work.

## Roadmap Completion Rule

A phase completing does not complete this body of work while a later roadmap phase remains unfinished.

For this initial roadmap, body-of-work completion is valid only after Phase 4 completes and no other approved
phase remains unfinished.

## Future Extension

Additional Bonsai workflow scenarios may be added to this project through human-approved roadmap changes. Keep
future implementation tasks trivial so the roadmap continues to test Bonsai rather than the application.
