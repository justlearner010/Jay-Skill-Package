# Knowledge-to-Task Model

## Node schema

```yaml
knowledge_node:
  name: string
  primary_type: fact | concept | mechanism | procedure | contract | diagnosis | integration | operation
  secondary_type: optional
  current_depth: D0 | D1 | D2 | D3 | D4 | D5 | unknown
  target_depth: D0 | D1 | D2 | D3 | D4 | D5
  dependency_role: hard | soft | corequisite | downstream | integration
  importance: P0 | P1 | P2 | P3
  importance_reason: string
  task_layer: T0 | T1 | T2 | T3 | T4 | T5
  evidence: list
```

## Classify before designing tasks

| Axis | Values | Decision use |
| --- | --- | --- |
| Type | fact, concept, mechanism, procedure, contract, diagnosis, integration, operation | Select practice form and verification. |
| Current/target depth | D0 locate, D1 explain, D2 reproduce, D3 apply independently, D4 diagnose/transfer, D5 design/evaluate | Set the maximum justified task layer. |
| Dependency role | hard, soft, corequisite, downstream, integration | Set order and identify bottlenecks. |
| Importance | P0 bottleneck, P1 core, P2 support, P3 orientation | Set intensity. |

Current depth must come from evidence. `unknown` is neither failure nor mastery.

## Select task layers

| Layer | Requirement |
| --- | --- |
| T0 map | Locate an authoritative reference or recognition handle. |
| T1 explain | Trace, compare, draw, or predict a minimal example. |
| T2 guided practice | Reproduce a bounded example with visible support. |
| T3 constrained Lab | Implement or operate inside an explicit contract with checks. |
| T4 diagnosis and variation | Handle faults, discriminate hypotheses, or transfer to a changed case. |
| T5 independent integration | Design and verify a new composition with reduced scaffolding. |

Task layer derives from `type + target_depth`; dependency role determines order.
Do not assign a T3 Lab to P3 orientation knowledge. Do not accept only T1 for
a P0 node that requires D4.

## Calibrate intensity

| Priority | Minimum evidence intensity |
| --- | --- |
| P0 | Multiple representations, prediction before action, independent application, variation or failure case, transfer, retrieval, regression/revisit. |
| P1 | One complete explain-practice-verify loop, one boundary/failure case, and one variation. |
| P2 | Bounded explanation plus one focused guided practice or observation. |
| P3 | Orientation or lookup handle only. |

Raise intensity when the depth gap, failure cost, recurrence, downstream
centrality, or target-role relevance is high. Lower it when recent evidence is
strong. Intensity means independence, variation, diagnostic pressure,
verification rigor, repetition, and transfer distance; it does not mean more
reading or more tasks.

## Build a phase

1. Name one observable capability.
2. Draw the minimum graph; preserve only nodes needed for that capability.
3. Classify nodes and document P0/P1 reasons.
4. Put hard prerequisites before their consumers; keep P2/P3 lightweight.
5. Choose one dominant mode: mechanism, contract, diagnosis, integration, or
   operation. Match verification to that mode.
6. Require every later integration gate to consume earlier verified contracts
   or evidence rather than silently reimplementing them.

## Required phase output

```text
capability question
current evidence and caveats
knowledge map: type, depth, dependency, importance, task layer, rationale
dependency graph
scope and non-goals
knowledge-gated tasks
verification matched to knowledge type
completion gates and unresolved P0 rule
next unlocked capability
```

## Practice selection

| Node type | Suitable practice |
| --- | --- |
| mechanism | derivation, trace, controlled experiment, property check |
| procedure | command or API exercise with interpreted output |
| contract | boundary tests and consumer example |
| diagnosis | seeded fault, hypotheses, root cause, regression |
| integration | explicit interfaces, end-to-end check, trade-off note |
| operation | metrics, runbook, recovery drill |

Use public checks, black-box harnesses, review rubrics, or hidden graders only
when they fit the practice. Preserve answer-free learning artifacts whenever
independent reasoning matters.
