---
title: SimplerEnv
area: robot-manipulation-benchmark
official_repo: https://github.com/simpler-env/SimplerEnv
---

# SimplerEnv

## Snapshot

- **Primary purpose:** evaluate real-world robot policies in simulation.
- **Setting:** SAPIEN/ManiSkill-based simulated counterparts of common real-robot setups.
- **Representative systems:** Google Robot and WidowX manipulation environments.
- **Key analysis:** agreement between simulated and real-world policy performance.

## Why It Matters

Real-robot evaluation is costly, slow, and difficult to reproduce. SimplerEnv tests whether a controlled simulation can serve as a useful proxy by comparing policies in paired simulated and physical setups. Its central question is not whether a simulator looks realistic in isolation, but whether conclusions drawn from it track real-world results.

## Evaluation Approaches

SimplerEnv supports visual matching, which adjusts simulated appearance toward real observations, and environment-variant aggregation, which evaluates across visual and physical variations. The project analyzes real-to-sim agreement using task success together with correlation and ranking-oriented measures.

## Reading Results

- Name the robot, task, environment variant, and policy checkpoint.
- Match observation preprocessing and action transforms to the policy's real setup.
- A high simulated success rate is not evidence of real-world fidelity without paired real results.
- Correlation depends on which policies and tasks are included; it is not a permanent property of the simulator.

## Primary Sources

- [Official repository](https://github.com/simpler-env/SimplerEnv)
- [Project page](https://simpler-env.github.io/)
- [Paper](https://arxiv.org/abs/2405.05941)
