# SimplerEnv

[English](simplerenv.md)

> **类别：** Robot Manipulation Benchmark · [Repository](https://github.com/simpler-env/SimplerEnv) · [Project Page](https://simpler-env.github.io/) · [Paper](https://arxiv.org/abs/2405.05941)

<p align="center">
  <img src="../docs/assets/benchmarks/simplerenv-teaser.jpg" alt="SimplerEnv simulated and real robot evaluation" width="820" />
</p>

<p align="center"><em>SimplerEnv 将 simulated scenes 与对应的 real-robot evaluation 配对。图片来源：<a href="https://simpler-env.github.io/">official project page</a>。</em></p>

## 概览

- **主要目标：** 在 simulation 中评估 real-world robot policies。
- **环境：** 基于 SAPIEN/ManiSkill，对常见 real-robot setup 进行模拟。
- **代表性系统：** Google Robot 与 WidowX manipulation environments。
- **核心分析：** Simulation 与 real-world policy performance 的一致性。

## 为什么重要

Real-robot evaluation 成本高、速度慢且难以复现。SimplerEnv 通过配对 simulated 与 physical setup，研究受控 simulation 能否作为可靠 proxy。它关注的不是 simulator 看起来是否足够逼真，而是 simulation 得出的 policy 结论能否反映 real-world result。

## Evaluation Approaches

SimplerEnv 支持 visual matching，通过调整模拟场景的前景物体、robot appearance 与背景来接近真实观测；也支持 environment-variant aggregation，在多种视觉和物理变化下汇总结果。项目使用 task success、correlation 与 ranking-oriented metric 分析 real-to-sim agreement。

## 环境与 Policy Interface

项目基于 SAPIEN 和 ManiSkill 重建 Google Robot 与 WidowX 相关任务。统一的 Gym-style interface 让 policy wrapper 读取 camera observations 和 robot state，再将预测动作转换到 simulator control space。

两种策略用于减小 reality gap：

- **Visual matching：** 调整 foreground objects、robot appearance 与 backgrounds，使其接近真实场景。
- **Variant aggregation：** 在多个合理的视觉与物理配置中评测，而不是依赖单一 digital twin。

## Metrics 的含义

Pearson correlation 衡量 simulated 与 real performance 的线性一致性，但在 policy score 范围很窄时可能不稳定。SimplerEnv 因此提出 Mean Maximum Rank Violation，用于惩罚与 real-world performance gap 相矛盾的 simulator ranking。两类 metric 都不能替代 per-task success，它们回答的是 simulation 是否支持与真实评测相同的比较结论。

## 结果解读

- 说明 robot、task、environment variant 与 policy checkpoint。
- Observation preprocessing 与 action transforms 必须匹配真实系统。
- 没有 paired real result 时，高 simulated success 不能证明 real-world fidelity。
- Correlation 取决于参与比较的 policies 与 tasks，不是 simulator 永久不变的属性。

## 适用场景

SimplerEnv 适合判断 simulation 是否能降低一组固定 real-robot policies 的评测成本。它不是主要用于生成 training data 的 benchmark，也不意味着 simulation 可以完整替代真实世界。

## 原始来源

- [Official repository](https://github.com/simpler-env/SimplerEnv)
- [Project page](https://simpler-env.github.io/)
- [Paper](https://arxiv.org/abs/2405.05941)
