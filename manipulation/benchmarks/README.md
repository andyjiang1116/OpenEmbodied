# Benchmarks

> Technical notes on robot manipulation evaluation suites.

[简体中文](README_ZH.md) · [Embodied Manipulation](../README.md)

| Benchmark | Focus |
| --- | --- |
| [LIBERO](libero.md) | Lifelong learning and transfer across language-conditioned tasks |
| [CALVIN](calvin.md) | Long-horizon language-conditioned task chains |
| [SimplerEnv](simplerenv.md) | Simulation as a proxy for real-robot policy evaluation |
| [RoboTwin 2.0](robotwin-2.md) | Bimanual data generation and domain-randomized robustness |
| [RoboDojo](robodojo.md) | Generalist-policy diagnosis across simulation and real robots |
| [RoboDyna](robodyna.md) | Dynamic physical reasoning and latency-aware manipulation evaluation |

Each note explains the capability being measured, environment and embodiment, task and data design, metrics, protocol boundaries, research use, and references.

## What Each Benchmark Measures

**LIBERO** studies transfer among language-conditioned tabletop tasks. Its Spatial, Object, and Goal suites isolate different changes; LIBERO-90 and LIBERO-10 have different roles in the original LIBERO-100 continual-learning protocol. A final task-success average measures a fixed policy, whereas forgetting or forward transfer requires a sequential learning order and repeated evaluation.

**CALVIN** measures how many dependent language instructions a Franka policy can complete in one persistent scene. Its five-instruction curve exposes accumulated error: success on the first instruction does not imply that later instructions remain reachable. Report the full success-at-1 through success-at-5 sequence and average completed length.

**SimplerEnv** tests whether simulated evaluations of Google Robot or WidowX-style policies agree with corresponding real-robot evaluations. A simulator success rate alone is insufficient for this purpose; policy ranking and correlation require paired real results. The chosen visual-matching or environment-variant protocol is part of the measurement.

**RoboTwin 2.0** connects task construction, expert demonstration generation, policy training, and dual-arm evaluation. Clean and randomized settings test different conditions. Results should identify the robot embodiment, task configuration, training demonstrations, randomization settings, and scene seeds.

**RoboDojo** evaluates generalist manipulation along generalization, memory, precision, long-horizon, and open-instruction dimensions. Its simulation and standardized real-robot tracks are separate. The policy is integrated through XPolicyLab; an aggregate score should be read with its per-dimension results.

**RoboDyna** probes dynamic physical reasoning in scenes that continue evolving. Its paired synchronous and asynchronous modes differ in whether measured policy inference time advances the world. Success and progress should be reported by capability, difficulty, and timing mode.

## Reading an Evaluation Result

Before comparing two policies, record the benchmark release, task split, robot and simulator, training data, observation and action interfaces, checkpoint, rollout length, reset procedure, episode count, seeds, and success rule. Also record whether inference time advances the environment. Differences in any of these fields can change a score without changing the policy architecture. A result from one benchmark cannot be numerically ranked against a result from another, because the tasks and score denominators differ.

The linked benchmark articles explain each protocol in detail. They are the entry points for task definitions, dataset and model interfaces, result interpretation, and official references.
