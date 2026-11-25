# 抓取模型

> 涵盖平行夹爪的抓取检测、灵巧手的抓取姿态生成与执行。

[English](README.md) · [全部模型家族](../README_ZH.md)

## 抓取任务与末端执行器

### 🤏 平行夹爪

平行夹爪方法通常根据 RGB-D 图像或点云预测夹爪的六自由度姿态、开口宽度与候选评分。感知结果还需经过碰撞检测、运动规划和控制执行，才能转化为实际抓取。

- [AnyGrasp](anygrasp_ZH.md) 将空间抓取检测与时序跟踪结合，用于杂乱和动态场景中的抓取候选估计。

### ✋ 灵巧手

灵巧手抓取除了全局手部姿态，还涉及多个关节自由度、自碰撞、物体穿透、接触稳定性与执行控制。因此，抓取姿态的生成质量与端到端执行成功率需要分开评估。

- [UniDexGrasp](unidexgrasp_ZH.md) 将多样化候选姿态生成与目标条件控制分为两个阶段。
- [DexGraspNet 2.0](dexgraspnet-2_ZH.md) 在大规模合成杂乱场景中生成灵巧手抓取姿态。
- [DexGrasp Anything](dexgrasp-anything_ZH.md) 在扩散模型训练与采样阶段引入物理约束。

## 方法对比

| 方法 | 末端执行器 | 主要输入 | 主要输出 | 技术侧重点 |
| --- | --- | --- | --- | --- |
| AnyGrasp | 平行夹爪 | 场景点云 | 可跟踪的抓取姿态 | 空间检测与时序关联 |
| UniDexGrasp | 灵巧手 | 物体点云 | 候选姿态与执行策略 | 分阶段生成与控制 |
| DexGraspNet 2.0 | 灵巧手 | 杂乱场景点云 | 场景条件抓取姿态 | 邻近障碍物约束 |
| DexGrasp Anything | 灵巧手 | 物体几何与条件信息 | 多样化手部姿态 | 物理约束引导的扩散生成 |

这些方法的成功率不能直接横向比较：末端执行器、输入条件、物体划分、仿真环境、碰撞规则、初始姿态和成功判据均可能不同。

## 基础工作与关联资源

- [GraspNet-1Billion](https://graspnet.net/) 提供大规模 parallel-gripper dataset 与 benchmark，是现代 grasping ecosystem 的重要基础。
- [Graspness Discovery / GSNet](https://arxiv.org/abs/2406.11142) 提出 graspability filtering，并进入 AnyGrasp 技术路线。
- [DexGraspNet](https://pku-epic.github.io/DexGraspNet/) 提供 132 万个 simulated dexterous grasps 和可扩展的 synthesis pipeline。
- [UniDexGrasp++](https://pku-epic.github.io/UniDexGrasp++/) 通过 geometry-aware curriculum 与 generalist-specialist iteration 研究 universal dexterous policy learning。

上述资源分别涉及模型、数据集和评测基准，阅读结果时应区分姿态生成指标与完整执行指标。
