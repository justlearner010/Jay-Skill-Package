# Designing Engineering Learning Phases Skill Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build, validate, locally install, and publish a domain-neutral Skill that converts engineering knowledge maps into importance-calibrated, dependency-ordered learning phases.

**Architecture:** The repository is the source of truth. Category folders organize reusable Skills, while the Skill keeps its procedural core in `SKILL.md` and its detailed knowledge taxonomy in one reference file. Eval scenarios live outside the Skill so validation evidence does not bloat runtime context. A local symlink exposes the repository copy to Codex without creating a drifting duplicate.

**Tech Stack:** Markdown, YAML, Codex Agent Skills, Git, GitHub CLI, skill-creator validation scripts.

---

## File map

- Modify: `README.md` — repository purpose, category index, contribution workflow, and Skill index.
- Create: `学习流程优化类/README.md` — category boundary and current Skills.
- Create: `学习流程优化类/designing-engineering-learning-phases/SKILL.md` — concise trigger and workflow.
- Create: `学习流程优化类/designing-engineering-learning-phases/agents/openai.yaml` — UI metadata.
- Create: `学习流程优化类/designing-engineering-learning-phases/references/knowledge-to-task-model.md` — knowledge classification, depth, dependency, priority, intensity, task-layer, and output schema.
- Create: `项目流程优化类/README.md` — category boundary.
- Create: `学习技巧类/README.md` — category boundary.
- Create: `工作实用类/README.md` — category boundary.
- Create: `skill设计思考/README.md` — lightweight note index and writing template.
- Create: `tests/designing-engineering-learning-phases/scenarios.md` — domain-diverse eval prompts and expected invariants.
- Create: `tests/designing-engineering-learning-phases/baseline.md` — observed no-Skill failure patterns.

### Task 1: Preserve the RED baseline

**Files:**
- Create: `tests/designing-engineering-learning-phases/scenarios.md`
- Create: `tests/designing-engineering-learning-phases/baseline.md`

- [ ] **Step 1: Write three reusable scenarios**

Record Transformer mechanism, Python CLI boundary, and Linux process diagnosis prompts. Each expected result must require this pre-task decision order:

```text
classify knowledge type and current/target depth
→ map hard/soft dependencies
→ rank P0–P3 global importance
→ select T0–T5 task layers
→ scale evidence intensity
→ emit the phase
```

- [ ] **Step 2: Record the already observed baseline failures**

Document these exact cross-scenario patterns:

```text
Transformer: reverted to Day 1–Day 7 despite flexible pacing.
Python CLI: produced a strong task ladder but did not classify knowledge nodes or justify unequal intensity.
Linux diagnosis: produced a strong gate ladder but treated nearly every gate as uniformly deep and skipped explicit global-importance ranking.
```

- [ ] **Step 3: Verify eval files are complete**

Run:

```bash
rg -n "Transformer|Python CLI|Linux|P0|T0|baseline" tests/designing-engineering-learning-phases
```

Expected: every search handle appears in the eval artifacts.

### Task 2: Initialize the Skill skeleton

**Files:**
- Create: `学习流程优化类/designing-engineering-learning-phases/SKILL.md`
- Create: `学习流程优化类/designing-engineering-learning-phases/agents/openai.yaml`
- Create: `学习流程优化类/designing-engineering-learning-phases/references/`

- [ ] **Step 1: Run the official initializer**

Run:

```bash
python /Users/jay/.codex/skills/.system/skill-creator/scripts/init_skill.py \
  designing-engineering-learning-phases \
  --path 学习流程优化类 \
  --resources references \
  --interface 'display_name=Engineering Learning Phase Designer' \
  --interface 'short_description=Design mastery-based engineering learning phases' \
  --interface 'default_prompt=Use $designing-engineering-learning-phases to turn this engineering topic into a dependency-aware learning phase.'
```

Expected: one Skill folder with `SKILL.md`, `agents/openai.yaml`, and `references/`.

- [ ] **Step 2: Confirm no placeholder resources remain**

Run:

```bash
rg -n "TODO|TBD|placeholder" 学习流程优化类/designing-engineering-learning-phases
```

Expected: initializer placeholders are visible before replacement; after Tasks 3–4 the same command returns no matches.

### Task 3: Write the knowledge-to-task decision model

**Files:**
- Create: `学习流程优化类/designing-engineering-learning-phases/references/knowledge-to-task-model.md`

- [ ] **Step 1: Define the knowledge-node schema**

The reference must define this record without domain-specific vocabulary:

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

- [ ] **Step 2: Define decision rules**

Include these invariants:

```text
Task layer comes from knowledge type plus target depth.
Task order comes from hard/soft dependency edges.
Intensity comes from global importance, evidence gap, centrality, recurrence, and failure cost.
P0 receives greater independence, variation, failure pressure, verification, retrieval, and transfer than P1–P3.
Time and task count do not define intensity.
If every node is P0, shrink or clarify the phase.
Unknown evidence is not failure and is not mastery.
```

- [ ] **Step 3: Define the output schema**

Require every designed phase to contain:

```text
capability question
current evidence and caveats
knowledge map with classification and intensity rationale
dependency graph
scope and non-goals
knowledge-gated task chain
verification matched to knowledge type
completion gates
next unlocked capability
```

### Task 4: Write the concise Skill workflow

**Files:**
- Modify: `学习流程优化类/designing-engineering-learning-phases/SKILL.md`
- Verify: `学习流程优化类/designing-engineering-learning-phases/agents/openai.yaml`

- [ ] **Step 1: Replace initializer content**

Use exactly two YAML frontmatter fields:

```yaml
---
name: designing-engineering-learning-phases
description: Use when designing, extending, or recalibrating staged engineering learning plans, Labs, practice gates, or course phases from prior learning evidence.
---
```

The body must instruct the agent to read the reference, inspect local evidence, classify before inventing tasks, propose scope when ambiguous, calibrate intensity, preserve answer-free assessment, and verify artifacts.

- [ ] **Step 2: Add explicit red flags**

The Skill must stop and revise when it notices:

```text
day-by-day scheduling used as the course skeleton
all nodes receiving the same practice depth
importance inferred only from difficulty or popularity
tasks written before the knowledge map
passing demo treated as mastery
hidden grader forced onto unsuitable open-ended work
domain-specific terminology leaking into the generic Skill
```

- [ ] **Step 3: Keep runtime context compact**

Run:

```bash
wc -w 学习流程优化类/designing-engineering-learning-phases/SKILL.md
```

Expected: fewer than 700 words; detailed taxonomy remains in the reference.

### Task 5: Build the repository taxonomy

**Files:**
- Modify: `README.md`
- Create: `学习流程优化类/README.md`
- Create: `项目流程优化类/README.md`
- Create: `学习技巧类/README.md`
- Create: `工作实用类/README.md`
- Create: `skill设计思考/README.md`

- [ ] **Step 1: Define category boundaries**

Use these distinctions:

```text
学习流程优化类: sequencing, assessment, review loops, evidence, and course design.
项目流程优化类: planning, implementation, testing, review, release, and maintenance workflows.
学习技巧类: focused cognitive techniques such as retrieval, explanation, memory, and problem solving.
工作实用类: reusable professional operations, documents, communication, analysis, and automation.
```

- [ ] **Step 2: Add a root index**

The root README must link all categories, list the new Skill under `学习流程优化类`, explain that category folders contain discoverable Skill folders, and state that validated Skills should include `SKILL.md` plus optional `agents/`, `references/`, `scripts/`, or `assets/` only when needed.

- [ ] **Step 3: Add the design-thinking entry**

`skill设计思考/README.md` must offer this lightweight note structure:

```text
问题或触发场景
没有 Skill 时的失败模式
核心抽象
适用边界与反例
验证场景
迭代后的结论
```

### Task 6: Validate and forward-test the Skill

**Files:**
- Verify: all Skill and eval files.

- [ ] **Step 1: Run structural validation**

Run:

```bash
python /Users/jay/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  学习流程优化类/designing-engineering-learning-phases
```

Expected: validation passes.

- [ ] **Step 2: Run repository checks**

Run:

```bash
rg -n "TODO|TBD|placeholder" README.md 学习流程优化类 项目流程优化类 学习技巧类 工作实用类 skill设计思考 tests
git diff --check
```

Expected: no placeholders and no whitespace errors.

- [ ] **Step 3: Re-run all three scenarios with the Skill**

Give fresh agents the Skill path and one raw scenario each. Success requires:

```text
classification before tasks
explicit dependency and importance reasoning
unequal P0–P3 intensity
task layers consistent with target depth
no day schedule unless explicitly requested
domain-appropriate verification
```

- [ ] **Step 4: Refactor and revalidate**

If a scenario misses an invariant, update only the Skill or reference rule that caused the gap, then rerun the failed scenario and `quick_validate.py`.

### Task 7: Install without duplicating the source

**Files:**
- Create symlink: `/Users/jay/.codex/skills/designing-engineering-learning-phases`

- [ ] **Step 1: Check for an existing installation**

Run:

```bash
ls -ld /Users/jay/.codex/skills/designing-engineering-learning-phases
```

Expected: absent, or already pointing to this repository copy.

- [ ] **Step 2: Create the source-of-truth symlink**

Run:

```bash
ln -s /Users/jay/Documents/Jay-Skill-Package/学习流程优化类/designing-engineering-learning-phases \
  /Users/jay/.codex/skills/designing-engineering-learning-phases
```

- [ ] **Step 3: Validate through the installed path**

Run:

```bash
python /Users/jay/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  /Users/jay/.codex/skills/designing-engineering-learning-phases
```

Expected: validation passes through the symlink.

### Task 8: Publish the package change

**Files:**
- Commit all intended files from Tasks 1–7 except the machine-local symlink.

- [ ] **Step 1: Review scope**

Run:

```bash
git status --short
git diff --check
git diff --stat
```

Expected: only package taxonomy, Skill, eval, and plan files are present.

- [ ] **Step 2: Commit intentionally**

Run:

```bash
git add README.md docs 学习流程优化类 项目流程优化类 学习技巧类 工作实用类 skill设计思考 tests
git commit -m "add engineering learning phase design skill"
```

- [ ] **Step 3: Push the feature branch**

Run:

```bash
git push -u origin codex/add-engineering-learning-phase-skill
```

- [ ] **Step 4: Open a draft pull request**

Create a draft PR targeting `main` with a body covering the general knowledge model, category structure, RED/GREEN scenarios, validation commands, and local installation strategy.
