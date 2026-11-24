# Grasping Models

> 从 parallel gripper 的 grasp perception，延伸到 dexterous hand 的物理可行姿态生成与执行。

[English](README.md) · [全部模型家族](../README_ZH.md)

## 两类 Grasping Regime

### 🤏 Parallel Gripper

Parallel-gripper system 通常从 RGB-D 或 point cloud 预测刚性 gripper pose、opening width 和 confidence。由于抓取执行可以交给传统 motion planner，这类方法更容易用于 clutter removal 和 industrial picking。

- [AnyGrasp](anygrasp_ZH.md) 将 spatial grasp detection 与 temporal tracking 结合，用于 clutter 和 dynamic scene 中快速、稳定的 grasp perception。

### ✋ Dexterous Hand

Dexterous hand 除了 global hand pose，还需要处理大量 articulated joint states、self-collision、object penetration、contact stability 和更复杂的 execution。因此需要明确区分 pose generation 与 policy execution。

- [UniDexGrasp](unidexgrasp_ZH.md) 将 diverse proposal generation 与 goal-conditioned grasp execution 拆分为两个阶段。
- [DexGraspNet 2.0](dexgraspnet-2_ZH.md) 面向大规模 synthetic cluttered scenes 学习 generative dexterous grasping。
- [DexGrasp Anything](dexgrasp-anything_ZH.md) 将 physics-aware guidance 引入 diffusion training 与 sampling。

## 能力地图

| 工作 | End effector | 主要输入 | 主要输出 | 核心贡献 |
| --- | --- | --- | --- | --- |
| AnyGrasp | Parallel gripper | Scene point cloud | Tracked grasp poses | Spatial-temporal grasp perception |
| UniDexGrasp | Dexterous hand | Object point cloud | Proposals 与 execution policy | Two-stage universal grasping |
| DexGraspNet 2.0 | Dexterous hand | Cluttered-scene point cloud | Generative grasp poses | Scene-level grasp generation |
| DexGrasp Anything | Dexterous hand | Object geometry 与 conditions | Diverse hand poses | Physics-guided diffusion |

这些工作的 raw success rate 不能直接横向比较，因为 end effector、输入假设、object split、simulator、collision rule、pose initialization 和 success criterion 并不一致。

## 基础工作与关联资源

- [GraspNet-1Billion](https://graspnet.net/) 提供大规模 parallel-gripper dataset 与 benchmark，是现代 grasping ecosystem 的重要基础。
- [Graspness Discovery / GSNet](https://arxiv.org/abs/2406.11142) 提出 graspability filtering，并进入 AnyGrasp 技术路线。
- [DexGraspNet](https://pku-epic.github.io/DexGraspNet/) 提供 132 万个 simulated dexterous grasps 和可扩展的 synthesis pipeline。
- [UniDexGrasp++](https://pku-epic.github.io/UniDexGrasp++/) 通过 geometry-aware curriculum 与 generalist-specialist iteration 研究 universal dexterous policy learning。

这些资源同时跨越 model、dataset 和 benchmark。后续建立 `datasets/` catalog 时，dataset profile 应放入独立目录，而不是在这里重复维护。
