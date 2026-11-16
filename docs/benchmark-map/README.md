# Robot Manipulation Benchmark Map

> LIBERO vs CALVIN vs SimplerEnv vs RoboTwin 2.0 vs RoboDojo: what does each benchmark actually measure?

[简体中文](README_ZH.md) · [Benchmark matrix](benchmark-matrix.md) · [Protocol guide](protocol-guide.md) · [Sources](sources.md)

## Executive Summary

Robot manipulation benchmarks are not interchangeable test sets. They differ in the capability being isolated, the robot and simulator, the source of demonstrations, the observation and action interface, and the way success is aggregated. A higher number on one benchmark does not imply superiority on another.

This guide compares five representative benchmarks:

- [LIBERO](../../benchmarks/libero.md) studies knowledge transfer in lifelong and multitask robot learning through language-conditioned tabletop manipulation suites.
- [CALVIN](../../benchmarks/calvin.md) emphasizes language-conditioned, long-horizon control and evaluates how many instructions a policy completes in sequence.
- [SimplerEnv](../../benchmarks/simplerenv.md) asks whether simulation can preserve real-world policy rankings on common robot setups.
- [RoboTwin 2.0](../../benchmarks/robotwin-2.md) combines scalable expert-data generation with a strongly randomized benchmark for robust bimanual manipulation.
- [RoboDojo](../../benchmarks/robodojo.md) evaluates generalist manipulation policies across complementary capability dimensions in simulation and on standardized real-robot setups.

The central lesson is: **choose a benchmark from the claim you want to test, not from its popularity.**

## The Five Questions

| Benchmark | Main question |
| --- | --- |
| LIBERO | Does knowledge learned from earlier tasks transfer to later manipulation tasks? |
| CALVIN | Can a policy follow language and complete several dependent tasks in sequence? |
| SimplerEnv | Does simulated evaluation track how policies compare on a corresponding real robot setup? |
| RoboTwin 2.0 | Can a bimanual policy remain effective across tasks, objects, scenes, and visual variation? |
| RoboDojo | How broadly capable is a generalist policy across generalization, memory, precision, long-horizon, and open-instruction challenges? |

## How They Differ

### 🧠 LIBERO: transfer across task suites

LIBERO was designed for lifelong robot learning. Its suites vary spatial relations, objects, goals, and longer task collections. The benchmark is useful when the research claim concerns forward transfer, knowledge retention, multitask learning, or the effect of task ordering. It is also widely used as an imitation-learning evaluation suite, but a standard success-rate result should not be mistaken for a full continual-learning study unless the learning protocol measures transfer and forgetting.

### 🔗 CALVIN: long-horizon language control

CALVIN places a Franka robot in a tabletop environment with 34 atomic tasks and language annotations. Its best-known evaluation samples chains of five instructions and reports the average number completed consecutively, together with success at each chain length. This makes it especially informative about recovery, compounding error, language grounding, and temporal composition.

### 🌉 SimplerEnv: sim-to-real evaluation fidelity

SimplerEnv reconstructs common real-robot evaluation setups in simulation. Its key contribution is not merely another simulated task suite: it studies whether simulation reflects real-world policy performance and ranking. Results should therefore identify the environment variant, robot, visual-matching or variant-aggregation setup, policy checkpoint, and corresponding real-world protocol.

### 🦾 RoboTwin 2.0: scalable bimanual robustness

RoboTwin 2.0 provides an expert data-generation pipeline and a benchmark of 50 dual-arm tasks. Its object collection, task programs, multiple embodiments, and domain randomization support research on scalable synthetic data, bimanual coordination, robustness, and sim-to-real transfer. Clean and randomized evaluations answer different questions and should be reported separately.

### 🥋 RoboDojo: broad sim-and-real capability evaluation

RoboDojo contains 42 simulation tasks organized around five capability dimensions—generalization, memory, precision, long-horizon execution, and open-vocabulary instruction following—plus 18 real-world tasks across three bimanual embodiments. It uses XPolicyLab as the shared policy integration layer. RoboDojo is evaluation-oriented: the benchmark, layouts, scoring, and result artifacts are separate from the policy implementation.

## Choosing a Benchmark

- **Continual or multitask transfer:** use LIBERO and preserve its task-suite and learning-order semantics.
- **Long-horizon instruction following:** use CALVIN and report the full five-instruction chain curve.
- **A simulation proxy for real-world evaluation:** use SimplerEnv and examine sim-to-real correlation or ranking agreement.
- **Bimanual data generation and robustness:** use RoboTwin 2.0, separating clean from randomized settings.
- **Broad generalist-policy diagnosis:** use RoboDojo and report per-dimension as well as aggregate results.

## What Can Be Compared

Results are directly comparable only when the benchmark version, task split, observations, action space, rollout horizon, number of episodes, seeds, checkpoint selection, and aggregation rule agree. Even within one named benchmark, changes to camera views, proprioception, history length, language inputs, or initial-state distributions can materially change the task.

Across different benchmarks, compare capability coverage and experimental design—not raw success percentages. See the [protocol guide](protocol-guide.md) for a practical reading checklist and the [benchmark matrix](benchmark-matrix.md) for a compact overview.
