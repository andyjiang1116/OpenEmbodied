# Grasping Models

> From grasp perception with parallel grippers to physically plausible pose generation and execution with dexterous hands.

[简体中文](README_ZH.md) · [All model families](../README.md)

## Two Grasping Regimes

### 🤏 Parallel Gripper

Parallel-gripper systems usually predict a rigid gripper pose, opening width, and confidence from RGB-D or point-cloud observations. They are practical for clutter removal and industrial picking because execution can be delegated to a conventional motion planner.

- [AnyGrasp](anygrasp.md) combines spatial grasp detection with temporal tracking for fast, stable grasp perception in clutter and dynamic scenes.

### ✋ Dexterous Hand

Dexterous hands add global hand pose, many articulated joint states, self-collision, object penetration, contact stability, and a harder execution problem. Pose generation and policy execution therefore need to be distinguished.

- [UniDexGrasp](unidexgrasp.md) separates diverse proposal generation from goal-conditioned grasp execution.
- [DexGraspNet 2.0](dexgraspnet-2.md) learns generative dexterous grasping in large-scale synthetic cluttered scenes.
- [DexGrasp Anything](dexgrasp-anything.md) introduces physics-aware guidance into diffusion training and sampling.

## Capability Map

| Work | End effector | Main input | Main output | Central contribution |
| --- | --- | --- | --- | --- |
| AnyGrasp | Parallel gripper | Scene point cloud | Tracked grasp poses | Spatial-temporal grasp perception |
| UniDexGrasp | Dexterous hand | Object point cloud | Proposals and execution policy | Two-stage universal grasping |
| DexGraspNet 2.0 | Dexterous hand | Cluttered-scene point cloud | Generative grasp poses | Scene-level grasp generation |
| DexGrasp Anything | Dexterous hand | Object geometry and conditions | Diverse hand poses | Physics-guided diffusion |

Raw success percentages should not be compared across these works: the end effector, input assumptions, object splits, simulator, collision rules, pose initialization, and success criteria differ.

## Foundations and Adjacent Resources

- [GraspNet-1Billion](https://graspnet.net/) supplies the large-scale parallel-gripper dataset and benchmark behind much of the modern ecosystem.
- [Graspness Discovery / GSNet](https://arxiv.org/abs/2406.11142) introduces graspability filtering used in the AnyGrasp lineage.
- [DexGraspNet](https://pku-epic.github.io/DexGraspNet/) provides 1.32 million simulated dexterous grasps and a scalable synthesis pipeline.
- [UniDexGrasp++](https://pku-epic.github.io/UniDexGrasp++/) focuses on universal dexterous policy learning with geometry-aware curriculum and generalist-specialist iteration.

These resources provide background on models, datasets, and benchmarks relevant to grasp generation.
