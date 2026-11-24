# RoboDyna

[English](robodyna.md)

> **类别：** Robot Manipulation Benchmark · [Repository](https://github.com/RoboDyna/robodyna) · [Project Page](https://robodyna.github.io/robodyna/) · [Paper](https://arxiv.org/abs/2611.26969) · [Data & Assets](https://huggingface.co/RoboDyna)

<p align="center">
  <img src="https://robodyna.github.io/robodyna/figures/fig1_teaser.png" alt="RoboDyna benchmark overview" width="860" />
</p>

<p align="center"><em>RoboDyna 在 policy 思考期间仍持续演化的环境中评估 language-conditioned dual-arm manipulation。图片来源：<a href="https://robodyna.github.io/robodyna/">official project page</a>。</em></p>

## 概览

- **主要目标：** 评估 dynamic scenes 中的 physical understanding 与 closed-loop action。
- **环境：** SAPIEN 3 中的 language-conditioned dual-arm manipulation。
- **任务组织：** 5 个 capability categories、20 个 conceptual tasks 与 10 个 household tasks。
- **数据：** 由 task-specific controllers 生成的 3,500 条 expert demonstrations。
- **关键协议：** 在相同 seeds 上配对进行 synchronous 与 asynchronous evaluation。

## 为什么重要

多数 manipulation benchmark 会在 policy inference 时暂停环境，得到 action 后才继续 simulation。这种设计使 computation time 不会影响任务。RoboDyna 中的环境持续受到 gravity、friction、collision、contact 与 state changes 影响；在 asynchronous protocol 下，场景会在真实 inference latency 内继续演化，因此一个正确但过晚的 action 也可能失败。

RoboDyna 由此将三个问题拆开：policy 是否理解 physical dynamics、是否选择了有效 action，以及能否足够快地生成该 action。

## Capability Categories

- **Trajectory Prediction：** 预测 moving object 的未来位置，包括 contact 或 collision 改变后的轨迹。
- **Periodic Pattern：** 识别重复运动规律，并在短暂 opportunity window 中行动。
- **Dynamic Avoidance：** 绕开独立移动的 objects 与 obstacles 规划 robot motion。
- **State Transition：** 跟踪无法仅通过 pose 表达的变化，例如 ripeness、doneness 或 availability。
- **Static to Dynamic：** 预测 robot 通过 pushing、striking 或 releasing 主动触发的运动。

每类包含 4 个 scene clutter 很少的 conceptual tasks。10 个 household tasks 则在更丰富的 office 与 kitchen scenes 中评测类似能力，并加入 rising liquids、overflow、dispensing 和 spreading spills 等现象。

## Difficulty Design

每个 conceptual task 有四种条件：

- `base`：easy condition；
- `var1` 与 `var2`：分别加入一种 task-specific variation 的 medium conditions；
- `var1+2`：组合两种变化且不参与训练的 hard condition。

这种设计可以区分对单个已知变化的 robustness，与对组合条件的 compositional generalization。

## Synchronous 与 Asynchronous Evaluation

两套 protocol 使用相同 tasks 与 seeds，但对 inference time 的处理不同：

- **Synchronous：** Policy 计算下一步 action 时，environment 实际上被冻结。
- **Asynchronous：** Action 执行前，environment 会按照测得的 inference latency 继续演化。

官方研究显示，latency 会改变 5–12% episodes 的最终结果，虽然平均 success rate 的变化更小。因此只报告 aggregate average 可能掩盖重要的 timing failures。

## Metrics 与 Baselines

RoboDyna 同时报告 binary success 与 progress score；后者根据 task milestones 提供 partial credit，并对错误进行惩罚。论文在 5.4K episodes 中评估 π0.5、X-VLA 与 FastWAM，并在相同 seeds 上提供 human baselines。结果按 difficulty、household tasks、capability category、metric 与 sync/async protocol 拆分。

这些结果只代表 released checkpoints 与 official protocol 下的发现，不能视为 model family 的永久排名。Human performance 也区分 teleoperation 与 scene-interactive control，因为 low-level control cost 会改变任务难度。

## 结果解读

- 分开报告 synchronous 与 asynchronous results，不能只给平均值。
- 记录 measured inference latency 以及对应 hardware。
- 说明使用 `base`、`var1`、`var2` 还是 held-out `var1+2`。
- 区分 conceptual 与 household tasks，它们的 clutter 和 semantic complexity 不同。
- 在 partial completion 有意义时同时报告 success rate 与 progress score。
- 不混合 policy 与不同 human control modes。

## 适用场景

RoboDyna 适合研究 dynamic physical reasoning、time-critical action、latency-aware evaluation，以及 physically grounded motion 下的 compositional generalization。它用于补充 static manipulation suites，并不能替代专门研究 lifelong transfer、long-horizon instruction chains 或标准化 real-robot evaluation 的 benchmark。

## 原始来源

- [Official repository](https://github.com/RoboDyna/robodyna)
- [Project page and task gallery](https://robodyna.github.io/robodyna/)
- [Paper](https://arxiv.org/abs/2611.26969)
- [Data and assets](https://huggingface.co/RoboDyna)
