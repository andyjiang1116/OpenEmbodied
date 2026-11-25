# RoboTwin 2.0

[English](robotwin-2.md)

> **类别：** 双臂机器人操作平台与评测基准 · [官方仓库](https://github.com/RoboTwin-Platform/RoboTwin) · [项目主页](https://robotwin-platform.github.io/) · [文档](https://robotwin-platform.github.io/doc/) · [论文](https://arxiv.org/abs/2506.18088)

<p align="center">
  <img src="../docs/assets/benchmarks/robotwin-overview.jpg" alt="RoboTwin 2.0 overview" width="820" />
</p>

<p align="center"><em>RoboTwin 2.0 将任务生成、专家数据合成与双臂策略评测结合起来。图片来源：<a href="https://robotwin-platform.github.io/">官方项目主页</a>。</em></p>

## 概览

- **主要目标：** 支持可扩展的示教数据生成与双臂操作策略评测。
- **环境：** 基于 SAPIEN 的双臂机器人仿真，支持多种机器人形态。
- **任务组织：** 官方资料描述约 50 项双臂操作任务及多类物体资源。
- **评测设置：** 区分基础场景与经过域随机化的场景。

## 评测目标

RoboTwin 2.0 将任务构建、专家示教生成和策略评测结合在同一仿真平台。其双臂协作与多物体设置覆盖了单臂桌面任务较少涉及的操作条件。

## 数据与评测

框架包含可编程任务专家、自动任务代码生成工具、RoboTwin Object Dataset 和策略评测流程。官方资料介绍了 50 项任务、来自 147 个类别的 731 个物体，以及 5 种机器人形态。域随机化覆盖物体、场景干扰、光照、背景、桌面高度和语言指令。

## 系统组成

1. **RoboTwin-OD** 提供 rigid、articulated 与多种视觉外观的 assets，并包含 semantic 和 manipulation-relevant annotations。
2. **任务生成：** 结合多模态语言模型与仿真反馈，生成可执行的任务程序。
3. **Expert collection** 运行 task-specific scripted solutions，大规模生成 demonstrations。
4. **Policy evaluation** 在受控 scene variations 下测试 dual-arm tasks。

RoboTwin 同时是 data-generation framework 与 evaluation benchmark。论文可能只使用其中一种功能，因此 “trained on RoboTwin” 与 “evaluated on RoboTwin” 应分开说明。

## 评测维度

50 个任务覆盖 coordinated picking、placement、handover、tool use、articulation、stacking 等 dual-arm skills。Clean scene 测试标准设置下的执行能力；randomized scene 引入 clutter、illumination、background、table height、object 与 language variation。更大的 framework 支持多种 embodiments，但每个结果仍与实际使用的 embodiment 绑定。

## 结果解读

- 说明所用任务集合与机器人形态。
- 分开报告 clean 与 randomized results。
- 说明 training 是否使用 RoboTwin-generated demonstrations，以及数据规模。
- 记录 scene seeds、episodes、step limits、language variants 与 randomization configuration。
- RoboTwin 2.0 与 RoboDojo 可以共享 XPolicyLab integration，但任务和 evaluation design 不同。

## 研究用途

RoboTwin 2.0 适合 scalable synthetic demonstrations、bimanual coordination 与 structured domain variation 下的 robustness 研究。若重点是仿真与标准化真机环境中的 capability-oriented diagnosis，则更适合使用 RoboDojo。

## 参考资料

- [Official repository](https://github.com/RoboTwin-Platform/RoboTwin)
- [Project page](https://robotwin-platform.github.io/)
- [Documentation](https://robotwin-platform.github.io/doc/)
- [Paper](https://arxiv.org/abs/2506.18088)
- [Leaderboard](https://robotwin-platform.github.io/leaderboard/)
