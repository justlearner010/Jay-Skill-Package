# Skill-Assisted Green Validation

The three scenarios in `scenarios.md` were rerun with
`designing-engineering-learning-phases` loaded from the repository source.

| Scenario | Result | Evidence |
| --- | --- | --- |
| Transformer attention | Pass | Produced a knowledge map before tasks, hard/co-requisite/downstream roles, P0–P3 reasons, T0–T5 gates, and no calendar skeleton. |
| Python CLI boundaries | Pass | Distinguished domain, adapter, testing, and diagnostic nodes; calibrated P0 boundary and testability work above familiar syntax. |
| Linux process diagnosis | Pass | Ranked signal semantics, reaping, and diagnosis integration as P0; kept tool lookup and advanced topics lighter; used gate-based progression. |

The three original scenarios met the seven original rubric criteria in
`scenarios.md`:

1. classification and current/target depth;
2. hard and soft dependency mapping;
3. global P0–P3 importance;
4. selective T0–T5 task layers;
5. unequal intensity rationale;
6. coherent phase output;
7. scenario fidelity without a calendar skeleton.

## Structural compatibility validation

Scenario 4 was rerun after adding the structural-compatibility model. The
scenario explicitly required `resources/week-01/` even though Week 0 retained
the legacy `resources/week-00.md` layout.

| Scenario | Result | Evidence |
| --- | --- | --- |
| Curriculum structure compatibility | Pass | Used `resources/week-01/` because an explicit target structure overrides a legacy predecessor; limited `weeks/week-01/` to README navigation; placed runnable work in `labs/week-01/`; required links, paths, test discovery, and grader entry points to be checked. |

The expanded rubric now passes 8/8: the original seven criteria plus structural
compatibility. Future changes must preserve the original scenario behavior and
the explicit-constraint-over-legacy rule.
