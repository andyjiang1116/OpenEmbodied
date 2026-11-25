# 协议指南

[English](protocol-guide.md) · [专题概览](README_ZH.md) · [基准矩阵](benchmark-matrix_ZH.md) · [资料来源](sources.md)

## 比较两个结果之前

需要从 paper、repository 或 evaluation config 中核对：

1. **Benchmark release 与 task suite：** 是否使用相同 tasks、split、assets 与 simulator version。
2. **Training data：** 区分 official demonstrations、extra robot data、synthetic data 与 benchmark-specific fine-tuning。
3. **Observation interface：** Camera views、resolution、proprioception、language、history 与 privileged state。
4. **Action interface：** Joint/Cartesian、absolute/delta、control frequency、action chunking 与 post-processing。
5. **Initial-state distribution：** Scene seeds、object placements、clean/randomized setting 与 reset rules。
6. **Rollout protocol：** Time limit、termination condition、episodes、seeds 与 retry policy。
7. **Checkpoint selection：** 区分 last checkpoint、validation-selected 与 task-selected checkpoints。
8. **Metric aggregation：** 确认结果平均的是 tasks、episodes、suites、chain lengths、capability dimensions 还是 robot stations。
9. **Inference timing：** 说明 environment 是否会在 policy inference 时暂停；如果 task dynamics 持续演化，需要记录 measured latency。

## Benchmark-Specific Reading

### LIBERO

- 说明 `LIBERO-Spatial`、`LIBERO-Object`、`LIBERO-Goal`、`LIBERO-10` 或 `LIBERO-90`。
- 区分 multitask training 与 sequential lifelong learning。
- Lifelong-learning 结论需要报告 task order 与 transfer/forgetting metric，而不只是 final success。
- 记录 image views、state inputs、demonstrations per task 与 rollout horizon。

### CALVIN

- 说明 dataset split，以及 evaluation 是否使用 language annotations。
- 报告连续完成至少 1 至 5 条指令的五个数值与 average sequence length。
- 说明 policy 是否观察 history，以及 internal state 是否在 subtasks 间 reset。
- 不应使用独立 atomic-task success 代替 official chained evaluation，却保留相同 benchmark label。

### SimplerEnv

- 说明 robot 与 task family，例如 Google Robot 或 WidowX setup。
- 说明使用 visual matching 还是 environment-variant aggregation。
- Policy checkpoint、observation preprocessing 与 action transforms 应与目标 real-world evaluation 匹配。
- 提出 sim-to-real fidelity 结论时，报告与 paired real result 的 correlation 或 ranking agreement。

### RoboTwin 2.0

- 说明 task list 与 robot embodiment。
- 分开报告 clean 与 randomized evaluation，并描述启用的 randomizations。
- 记录 episodes per task、scene seeds、language variants 与 step limits。
- 区分使用 RoboTwin-generated training data、zero-shot 或 externally trained policy 的结果。

### RoboDojo

- 分别报告 Generalization、Memory、Precision、Long-Horizon 与 Open 五个 simulation dimensions。
- 区分 simulation、remote real-world evaluation 与本地复刻的 setup。
- 记录 benchmark layouts、seeds、XPolicyLab adapter、action interface 与 submitted checkpoint。
- 与 public leaderboard 比较时使用 official scoring 与 verification protocol。

### RoboDyna

- 在相同 task conditions 与 seeds 上分开报告 synchronous 和 asynchronous results。
- 记录 measured policy latency、inference hardware，以及是否包含 communication 或 preprocessing time。
- 说明 conceptual / household task，以及 `base`、`var1`、`var2` 或 held-out `var1+2` condition。
- Partial completion 有意义时，同时报告 success rate 与 progress score。
- 不能把 frozen-world result 与 real-time result 当成相同 protocol 直接比较。

## 最低结果记录

```text
Model and checkpoint:
Training data and adaptation:
Benchmark version and tasks:
Robot and simulator:
Observations and actions:
Episodes, seeds, and horizon:
Metric and aggregation:
Hardware and policy frequency:
Inference latency and timing protocol:
Source:
```

这些信息不会让不同 benchmark 的数字自动可比，但能让每个结果更容易理解与复现。
