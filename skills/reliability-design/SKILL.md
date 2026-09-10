---
name: reliability-design
description: Assess risky workflows and legacy migrations involving durable state, external side effects, money, callbacks,
  retries, concurrency, compensation, reconciliation, or irreversible operations; choose the smallest adequate design and
  define regression proof before implementation.
---

# Reliability Design

Turn concrete failure modes into the smallest reliable design. Patterns are tools,
not goals: retain straightforward flow code when it already makes the required
invariants and recovery behavior clear and testable.

## Assess

1. Read the nearest repository instructions and inspect the current execution path,
   persistence, adapters, tests, and operational entry points. Prefer current code
   and runtime evidence over an assumed architecture.
2. State the observable outcome, business invariants, failure modes, and a checkable
   success criterion. Distinguish confirmed behavior, inference, and behavior that
   still needs live verification.
3. Identify where the workflow crosses requests, processes, databases, queues,
   timers, webhooks, or external providers. For each side effect, record its owner,
   idempotency mechanism, durable evidence, retry safety, and recovery path.
4. Choose the smallest pattern that addresses an identified risk. Reject patterns
   whose value is only hypothetical.

## Pattern Selection

Use these as decision criteria, not a checklist to implement wholesale:

- **Pure function plus discriminated union:** synchronous decisions and small flows
  whose valid outcomes fit in one request.
- **Functional core plus imperative shell:** business decisions need exhaustive,
  deterministic tests while I/O obscures their causes and outcomes. Keep rules and
  transitions pure; pass data in and return decisions or commands. Keep databases,
  providers, clocks, randomness, logging, and command execution in the shell.
- **Interface plus adapters:** behavior varies across real and fake providers, or a
  dependency must be replaced in tests. Treat the caller-facing interface as the
  test seam; avoid exposing provider mechanics through it.
- **State machine:** lifecycle state persists across requests or restarts, invalid
  transitions matter, and at least one external event, concurrent actor,
  irreversible side effect, compensation, or reconciliation path exists. Model
  facts as states and events; emit commands for side effects rather than hiding
  provider calls inside transitions.
- **Saga or process manager:** one business operation coordinates multiple systems
  and requires explicit compensations or manual recovery.
- **Transactional Outbox and Inbox:** state changes and outbound work must not split
  across a crash, or inbound events may be duplicated or reordered.
- **Idempotency key plus optimistic concurrency:** an operation may be delivered more
  than once or multiple actors may advance the same record. Persist stable operation
  identity and fence transitions with a revision, lease, or compare-and-swap.
- **Reconciliation:** a remote operation may succeed while its response or webhook
  is lost. Represent unknown as a real state and query authoritative evidence; do
  not translate a timeout directly into failure.
- **Effect:** a module has substantial typed failure, retry, timeout, cancellation,
  resource-lifecycle, concurrency, or dependency-injection complexity. Effect does
  not replace durable state, idempotency, a state machine, or reconciliation. Keep
  existing Promise-facing interfaces during a bounded adoption unless a wider
  migration is explicitly approved.
- **Strangler Fig or Branch by Abstraction:** a risky legacy implementation must be
  replaced without a big-bang cutover. Put old and new implementations behind one
  stable seam, prove them against the same observable contract, route a reversible
  slice at a time, and follow the migration gates below.

Do not introduce event sourcing, CQRS, a workflow engine, or a new infrastructure
surface merely because a smaller pattern appears elsewhere in this list.

## Decision Gate

Before changing code, summarize:

```text
Risk signals:
Business invariants:
Smallest sufficient design:
Rejected alternatives:
Operational and maintenance cost:
Regression proof:
Approval required: yes/no
```

Proceed without interrupting the user when the design is local, uses established
repository patterns, preserves public behavior, and stays within the requested
scope. Explain the choice in the handoff when it is consequential.

Ask before implementation when the proposal introduces or materially changes any
of the following:

- a runtime dependency or architectural convention;
- persistent state, schema, or migration semantics;
- a public interface or business-state meaning;
- a queue, worker, cron, durable actor, or other operational component;
- payment, refund, registration, deletion, or other irreversible behavior;
- a data migration, rollout strategy, or meaningful scope expansion.

Present the expected benefit, cost, migration sequence, verification plan, and
rollback path with the question. Do not ask merely to use a pure function, an
existing adapter seam, a fake, or another established local pattern.

## Preserve Behavior During Repair and Migration

For a bug or legacy workflow migration:

1. Reproduce the exact failure with the narrowest test that crosses the same seam
   as callers. When a deterministic reproduction is possible, make the test red
   before the fix.
2. Apply and verify the smallest coherent repair before broad restructuring. Use
   real or sandbox evidence when the failure depends on a provider, while avoiding
   irreversible acceptance actions unless authorized.
3. Add characterization and contract tests for the correct externally observable
   behavior. Avoid coupling these tests to private functions that the migration
   will replace.
4. **Branch by abstraction:** introduce one seam, retain the old implementation
   behind it, and run the old and new implementations against the same contract
   suite. Use differential or read-only shadow execution when it is safe and
   materially useful.
5. Add fault tests for applicable crash points, timeouts before and after remote
   success, duplicate and out-of-order delivery, stale reads, concurrency,
   idempotency, compensation, and reconciliation.
6. **Strangler cutover:** switch the smallest reversible slice. Remove the old
   implementation only after the new path passes the agreed gates and the rollback
   path is known.

For a new workflow, establish its invariants and acceptance tests first, then apply
the same pattern and fault-test selection without inventing legacy behavior.

## Prove

Run the narrowest relevant unit, contract, integration, concurrency, and recovery
checks. Coverage alone is not proof: verify the assertions exercise the identified
failure modes. Inspect the final diff and report separately what local tests,
sandbox/provider checks, and production acceptance did or did not establish.
