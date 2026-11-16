# Benchmark 可比性说明

[English](benchmark-notes.md) · [专题概览](README_ZH.md) · [模型矩阵](model-matrix_ZH.md) · [来源清单](sources.md)

## 为什么需要单独说明

模型名称和 benchmark score 不足以支撑公平比较。VLA evaluation 对 policy checkpoint、task suite、observation pipeline、action representation、fine-tuning data、rollout settings 与 success aggregation 都非常敏感。

## 阅读 VLA 结果时需要确认

1. **Checkpoint 与 recipe：** 区分 base、task-specific、LoRA、full fine-tuning、OFT 或其他优化方案。
2. **Training data：** 是否加入 benchmark demonstrations、extra robot data 或 synthetic data。
3. **Observations：** Camera 数量、resolution、proprioception、language 与 history。
4. **Actions：** Joint 或 Cartesian、absolute 或 delta、control frequency 与 action chunk length。
5. **Evaluation：** Task list、episodes、seeds、horizon、reset 与 success definition。
6. **Aggregation：** 先按 episode、task 还是 suite 平均，是否报告 variance。

## LIBERO

LIBERO 是开放 VLA 论文中常见的共同 benchmark，但不同实现仍可能改变 observation history、camera inputs、action chunking、rollout length 与 suite aggregation。应报告 Spatial、Object、Goal 与 Long 等具体 suite，不能只给出缺少上下文的总分。

## SimplerEnv

SimplerEnv 的核心价值是比较 simulation 与对应 real-world evaluation 的一致性。结果应说明 robot setup、task variant、visual matching 或 environment aggregation、policy checkpoint，以及 paired real result。单独的 simulated success 不能证明 sim-to-real fidelity。

## Real-Robot Evaluation

真实 robot 结果还受到 hardware revision、camera calibration、controller、reset procedure、operator intervention、trial count 与 safety termination 的影响。不同实验室中的同名任务通常不能视为统一 benchmark。

## 建议报告格式

```text
Model and checkpoint:
Adaptation recipe and data:
Benchmark and task suite:
Observations and actions:
Episodes, seeds, and horizon:
Metric and aggregation:
Hardware and control frequency:
Source:
```

这些信息让结果更容易理解与复查，但不会自动使不同 protocol 下的数字可比。
