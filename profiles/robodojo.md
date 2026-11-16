---
title: RoboDojo
area: robot-manipulation-benchmark
official_repo: https://github.com/RoboDojo-Benchmark/RoboDojo
---

# RoboDojo

## Snapshot

- **Primary purpose:** comprehensive evaluation of generalist robot manipulation policies.
- **Coverage:** 42 simulation tasks and 18 real-world tasks.
- **Capability dimensions:** generalization, memory, precision, long-horizon execution, and open-vocabulary instruction following.
- **Policy integration:** XPolicyLab provides a common serving and deployment interface.

## Why It Matters

Many manipulation benchmarks compress performance into one task-average success rate. RoboDojo instead groups challenging tasks by the capability they are intended to probe and connects simulation with a standardized real-world evaluation track. This makes it useful for finding where a generalist policy fails rather than only assigning it a single rank.

## Simulation and Real-World Evaluation

The simulation benchmark uses Isaac Sim and supports heterogeneous parallel execution across tasks and scenes. RoboDojo-RealEval standardizes hardware, resets, evaluation protocol, and deployment interfaces for physical testing, including remote evaluation. The real-world track covers three bimanual embodiments.

RoboDojo is evaluation-only in its released architecture: policies are integrated through XPolicyLab, while RoboDojo owns the environments, tasks, layouts, validation, scoring, and result artifacts. XPolicyLab also supports RoboTwin, but the two benchmarks remain distinct.

## Reading Results

- Inspect per-dimension results before the aggregate score.
- Distinguish simulation results from real-robot results.
- Record the submitted checkpoint, XPolicyLab adapter, layout/seed protocol, action interface, and evaluation track.
- Use the official protocol for comparisons with verified leaderboard entries.
- Do not treat RoboDojo and RoboTwin 2.0 scores as comparable merely because they share policy infrastructure.

## Primary Sources

- [Official repository](https://github.com/RoboDojo-Benchmark/RoboDojo)
- [Project page](https://robodojo-benchmark.com/)
- [Paper](https://arxiv.org/abs/2607.04434)
- [Leaderboard](https://robodojo-benchmark.com/leaderboard)
- [XPolicyLab](https://github.com/XPolicyLab/XPolicyLab)
