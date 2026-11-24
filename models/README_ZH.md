# 模型

> 按照模型在 Embodied System 中承担的能力组织技术档案。

[English](README.md)

## 模型家族

### 🧠 [Vision-Language-Action Models](vla/README_ZH.md)

将视觉观测、语言指令与机器人动作连接起来的 generalist policy。目前收录 OpenVLA、SmolVLA、π0 / π0-FAST / π0.5 和 NVIDIA Isaac GR00T N1.7。

### ✋ [Grasping Models](grasping/README_ZH.md)

覆盖 parallel gripper 的 grasp perception，以及 dexterous hand 的 grasp pose generation 与 execution。当前通过统一的 grasping taxonomy 串联 AnyGrasp、UniDexGrasp、DexGraspNet 2.0 和 DexGrasp Anything。

## 组织原则

模型档案按照 capability domain 划分，而不是按照 framework 或研究机构分类。后续当内容达到一定规模时，可以自然增加 `world-models/`、`navigation/` 或 `humanoid-control/`，避免把无关方法堆叠在同一目录。

每篇档案会区分 research contribution 与实际发布的代码、数据、checkpoint、运行依赖、license 和 deployment boundary。
