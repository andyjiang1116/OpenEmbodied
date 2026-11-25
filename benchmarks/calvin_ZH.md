# CALVIN

[English](calvin.md)

> **类别：** 机器人操作评测基准 · [官方仓库](https://github.com/mees/calvin) · [项目主页](http://calvin.cs.uni-freiburg.de/) · [论文](https://arxiv.org/abs/2112.03227)

<p align="center">
  <img src="../docs/assets/benchmarks/calvin-teaser.jpg" alt="CALVIN long-horizon manipulation benchmark" width="820" />
</p>

<p align="center"><em>CALVIN 将语言条件桌面操作技能组合为长程任务序列。图片来源：<a href="https://github.com/mees/calvin">官方仓库</a>。</em></p>

## 概览

- **主要目标：** 评估语言条件下的长程机器人操作。
- **环境：** 基于 PyBullet 的 Franka 机械臂桌面场景。
- **任务组织：** 34 个原子任务，可组合成连续指令序列。
- **代表性指标：** 五条指令组成的序列中连续完成的平均任务数。

## 评测目标

CALVIN 评估连续指令执行，而非单次抓取成功率。策略需要根据变化的语言目标，在子任务之间保持场景状态并连续控制机器人。早期步骤的失败会影响后续任务，因此该协议能够呈现长程执行中的误差累积。

## 数据与评测

数据集包含遥操作采集的自由交互轨迹及相应片段的语言标注。标准长程评测使用五条指令组成的序列，通常报告连续完成至少 1 至 5 条指令的成功率，以及平均完成长度。

## 环境与任务设计

仿真桌面包含 Franka Panda 机械臂、抽屉、滑门、按钮、积木与灯光开关等交互元素。34 项原子任务描述共享环境中的状态变化。后续任务从前一条指令结束时的状态继续，因此策略需要连续处理场景变化。

数据以自由交互轨迹形式采集，而非为每条指令单独录制示教。语言标注对应能够完成目标状态变化的轨迹片段，支持序列建模和技能复用研究。

## 评测指标

对于五条指令链，评测记录按顺序至少完成 1 至 5 个任务的比例。平均完成长度可以概括整体曲线，但完整曲线更能展示错误从何处开始累积。只能稳定完成第一条指令，与从一开始就普遍失败，是两种不同的 limitation。

## 结果解读

- 明确 dataset split，并确认使用 official task-chain evaluation。
- 检查 history、language relabeling、auxiliary data 与 pretrained vision-language components。
- Atomic-task success 与 chained success 不能互换。
- 第一条任务成功率高但随 chain length 快速下降，通常反映 transition 或 long-horizon 问题。

## 研究用途

CALVIN 适合研究 language grounding、history、subtask transition 与 compounding error。如果目标只是隔离单一 manipulation skill，应选择 independent-task benchmark。

## 参考资料

- [Official repository](https://github.com/mees/calvin)
- [Project page](http://calvin.cs.uni-freiburg.de/)
- [Paper](https://arxiv.org/abs/2112.03227)
