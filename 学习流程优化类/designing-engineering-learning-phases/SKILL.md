---
name: designing-engineering-learning-phases
description: Use when designing, extending, or recalibrating staged engineering learning plans, Labs, practice gates, or course phases from prior learning evidence.
---

# Designing Engineering Learning Phases

Turn an engineering topic into a mastery-paced capability phase. Allocate depth
by global importance and evidence gap, not by calendar days or topic count.

## Required reference

Read [references/knowledge-to-task-model.md](references/knowledge-to-task-model.md)
before proposing tasks. It defines the knowledge-node schema, D0–D5 mastery
depths, P0–P3 importance, T0–T5 task layers, and the required output.

## Workflow

1. Inspect the local roadmap, previous phase, learner evidence, existing
   course structure, and repository conventions. Extract a structural contract:
   artifact roles, canonical paths, naming patterns, runnable entry points, and
   legacy exceptions. Build a cross-phase compatibility matrix for paths, file
   granularity, names, required sections, links/commands, and evidence records.
   Classify each predecessor pattern as canonical, legacy, incomplete, or an
   explicitly justified variation. Treat an explicit user structure constraint
   as the target contract; use older patterns only to plan migration. Separate
   proven evidence, learner claims, stale records, and unknowns.
2. State one observable capability question. Build the smallest knowledge graph
   needed to answer it; mark hard/soft dependencies, co-requisites, downstream
   consumers, and integration nodes.
3. For each retained node, classify type, current/target depth, global
   importance, importance rationale, and task layer. Do this before writing a
   task list.
4. Keep one to three P0 bottlenecks in a phase. If every node is P0, narrow
   the capability question or split the phase.
5. Order gates by hard dependencies. Map every learning artifact to an existing
   repository role before writing it: navigation, resource, task chain, runnable
   Lab, evidence record, or solution. Choose practice and verification that fit
   the type: trace/derivation, controlled implementation, command experiment,
   fault diagnosis, integration check, or operational drill.
6. Define or reuse one canonical phase artifact contract before writing the
   new phase. It must state names, file granularity, required section roles,
   link/command conventions, and evidence-record fields. Plan migration or a
   documented exception for every unexplained predecessor mismatch.
7. Scale intensity with importance and evidence gap. P0 needs independent
   application, variation or failure pressure, transfer, retrieval, and later
   revisit. P2/P3 should not receive a standalone Lab merely for symmetry.
8. Reuse the target repository's organization. If an artifact does not fit,
   state the migration reason and update all affected links and entry points;
   do not create a parallel folder pattern by convenience. Keep public
   materials answer-free; use hidden graders only when they aid independent
   learning.
9. Define completion with evidence, not elapsed time: required gates, unresolved
   P0 gaps, transfer check, explanation, failure evidence, and next capability.

## Output order

Return or write, in this order:

1. capability question and evidence caveats;
2. knowledge map with classification and intensity rationale;
3. dependency graph and scope/non-goals;
4. structural compatibility map: artifact role, canonical path, predecessor
   pattern, and required link/entry-point changes;
5. cross-phase conformance report: matrix, canonical/legacy classification,
   migration or justified-variation decisions, and contract fields;
6. knowledge-gated task chain and practice artifacts;
7. verification and completion gates, including structural and format checks;
8. next unlocked capability.

## Red flags

Stop and revise if tasks appear before the knowledge map; a day-by-day schedule
becomes the skeleton; all nodes receive equal depth; importance is inferred
from popularity or difficulty alone; a passing demo is called mastery; a hidden
grader is forced onto open-ended work; a new stage invents a parallel directory
pattern; `weeks/` absorbs resource or executable artifacts contrary to its
established role; links or runnable entry points are not checked after a move;
new phases copy a predecessor without classifying it; file names, granularity,
required headings, commands, or evidence formats drift without an explicit
exception; or a knowledge difference is used to excuse an artifact-format
difference;
or domain vocabulary leaks into this generic Skill.
