# Reusable Evaluation Scenarios

These scenarios evaluate whether a learning-phase designer reasons about the knowledge map before producing tasks. They are reusable: the evaluator may change the learner profile or time budget, but must preserve the required decisions and invariants.

## Required decision order

Every response must make these decisions explicitly and in this order:

1. Classify each material knowledge node and state its current and target depth.
2. Map hard dependencies separately from soft dependencies.
3. Rank global importance with P0-P3, including at least one explicit lower-priority or deferred node.
4. Select task layers with T0-T5 and explain why each selected layer is necessary.
5. Calibrate evidence intensity unequally from importance, dependency role, learner gap, and failure risk.
6. Emit a coherent learning phase with outcomes, ordered work, evidence, gates, and exit criteria.

The response may define its own knowledge-type and depth vocabulary, but it must use both consistently. P0 is the highest global importance. T0-T5 are task-layer labels, not a six-step checklist: selecting all six requires justification.

## Scenario 1: Transformer mechanism learning

### Prompt

Design a flexible learning phase for a learner who can use PyTorch tensor operations and call a Transformer layer, but cannot yet explain or debug the mechanism. The target is to explain scaled dot-product attention, implement a minimal single-head attention path, extend it to multi-head attention, and diagnose shape and mask failures. Include Q/K/V projections, similarity scores and scaling, softmax, masking, head splitting/concatenation, output projection, residual connections, layer normalization, positional information, and feed-forward layers in the knowledge map. Do not turn the phase into a Day 1-Day 7 schedule; pacing must advance by evidence and gates.

Before proposing exercises, classify the knowledge types and current/target depths, distinguish hard and soft dependencies, rank every material node P0-P3, choose justified T0-T5 task layers, calibrate unequal evidence intensity, and then emit the phase.

### Expected invariants

- Tensor shapes, Q/K/V flow, score scaling, softmax, and mask semantics are treated as mechanism-critical dependencies before multi-head implementation and diagnosis.
- The map distinguishes the attention mechanism from surrounding Transformer-block concepts; not every named node receives equal priority or depth.
- At least one task requires an observable implementation artifact, and at least one task requires diagnosis from a malformed shape or mask.
- Progression is gate-based and flexibly paced. Calendar-day labels are absent.
- The final phase traces each high-intensity task and gate back to a classified node, depth gap, dependency, and P0-P3 decision.

## Scenario 2: Python CLI application boundaries

### Prompt

Design a learning phase for a learner who can write small Python scripts with `argparse`, but tends to place parsing, business rules, file I/O, formatting, and process termination in one function. The target is a testable command-line application with clear boundaries among argument parsing, orchestration, domain logic, adapters for external I/O, presentation, and the executable entry point. Include validation, exit-code ownership, exception translation, dependency injection at the composition root, unit tests, and one subprocess-level acceptance test.

Before proposing the task ladder, classify the knowledge types and current/target depths, distinguish hard and soft dependencies, rank every material node P0-P3, choose justified T0-T5 task layers, calibrate unequal evidence intensity, and then emit the phase. Explicitly justify why boundary-defining and integration work should or should not receive more evidence than familiar syntax.

### Expected invariants

- The response separates declarative knowledge about boundaries from procedural refactoring skill and diagnostic judgment about leakage or ownership.
- Pure domain logic and explicit side-effect boundaries precede subprocess integration; useful testing or packaging conveniences may be soft dependencies rather than universal gates.
- Global importance differentiates architectural boundaries and exit/error ownership from already-familiar `argparse` syntax.
- The phase contains a thin vertical slice, focused boundary tests, and an end-to-end CLI check with observable exit code and output.
- Unequal intensity is justified per node or cluster; a strong task ladder alone does not satisfy the scenario.

## Scenario 3: Linux process and signal diagnosis

### Prompt

Design a learning phase for a learner who knows basic shell commands but cannot reliably diagnose a process that ignores termination, becomes a zombie, or leaves a pipeline hanging. The target is to explain process identity and parent/child relationships, distinguish process state from process control, inspect signal dispositions and masks, choose safe signals, interpret permissions, use `ps`, `/proc`, `kill`, `wait`, `strace`, and shell job-control evidence, and diagnose three failures: ignored `SIGTERM`, an unreaped child, and a process blocked around a pipe.

Before proposing diagnostic gates, classify the knowledge types and current/target depths, distinguish hard and soft dependencies, rank every material node P0-P3, choose justified T0-T5 task layers, calibrate unequal evidence intensity, and then emit the phase. Do not make every command or gate equally deep merely because it appears in the workflow.

### Expected invariants

- Process identity, parent/child relationships, process states, signal semantics, and wait/reaping form explicit hard dependencies for the relevant diagnoses.
- Tool syntax and optional deep tracing are separated from the conceptual model; `strace` is not automatically a prerequisite for every case.
- P0-P3 ranking is global across the phase and distinguishes safety-critical signal reasoning from lookup-level command details.
- Each diagnosis gate requires a hypothesis, selected evidence, interpretation, and safe next action rather than command execution alone.
- Intensity varies by consequence and learner gap; evidence for safe signaling and causal diagnosis is stronger than evidence for memorizing flags.

## Compact evaluation rubric

Score each item 0 or 1 against a scenario response:

| # | Criterion | Pass condition |
| --- | --- | --- |
| 1 | Classification and depth | Material nodes have consistent knowledge types plus explicit current and target depths. |
| 2 | Dependencies | Hard and soft edges are separate, directional, and materially affect ordering. |
| 3 | Global importance | Material nodes are ranked P0-P3 globally, with meaningful differentiation. |
| 4 | Task layers | T0-T5 choices are explicit, selective or justified, and linked to node needs. |
| 5 | Intensity | Evidence intensity is unequal and justified by importance, dependency, gap, or risk. |
| 6 | Phase output | Outcomes, ordered work, evidence, gates, and exit criteria form one coherent phase. |
| 7 | Scenario fidelity | All scenario-specific invariants are satisfied without replacing gates with a fixed-day schedule. |

Passing requires 7/7. Criteria 1-6 are hard invariants: a polished task ladder cannot compensate for omitting any pre-task decision.
