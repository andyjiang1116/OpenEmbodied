# 基准矩阵

[English](benchmark-matrix.md) · [专题概览](README_ZH.md) · [协议指南](protocol-guide_ZH.md) · [资料来源](sources.md)

| Benchmark | 主要研究问题 | Environment 与 embodiment | Task structure | 代表性报告方式 |
| --- | --- | --- | --- | --- |
| LIBERO | Lifelong 与 multitask knowledge transfer | robosuite/MuJoCo tabletop manipulation，7-DoF arm | Spatial、Object、Goal、10-task、90-task suites | Task success；用于 lifelong learning 时增加 transfer/forgetting metrics |
| CALVIN | Language-conditioned long-horizon control | PyBullet tabletop environment，Franka arm | 34 个 atomic tasks，组合为五条指令链 | 平均连续完成指令数，以及各 chain length 的 success |
| SimplerEnv | Simulation 是否能反映 real-world policy comparison | 基于 SAPIEN/ManiSkill 的常见 robot setup digital twins | 使用 visual matching 或 environment variants 重建真实任务 | Task success 与 sim-to-real correlation / ranking agreement |
| RoboTwin 2.0 | Scalable bimanual data generation 与 robust policy evaluation | 基于 SAPIEN 的 dual-arm manipulation，多种 embodiments | 50 个 tasks 与 domain-randomized scenes | Per-task 与 mean success，区分 clean/randomized settings |
| RoboDojo | Generalist policy 的 sim-and-real 综合评测 | Isaac Sim 与三种 bimanual embodiments 的标准化 real stations | 42 个 simulation tasks、18 个 real-world tasks、五个 capability dimensions | Per-task、per-dimension 与 aggregate score/success |
| RoboDyna | Dynamic physical reasoning 与 latency-aware manipulation | SAPIEN 3 dual-arm simulation，environment 持续按 physics 演化 | 20 个 conceptual tasks、10 个 household tasks、五类能力与四档 conceptual difficulty | 按 difficulty、capability 与 sync/async protocol 报告 success 和 progress score |

## Capability Coverage

| Capability | LIBERO | CALVIN | SimplerEnv | RoboTwin 2.0 | RoboDojo | RoboDyna |
| --- | --- | --- | --- | --- | --- | --- |
| Language-conditioned control | 核心 | 核心 | 取决于 policy/task | 支持 | Open-instruction tasks 的核心 | 核心 |
| Long-horizon composition | 受 suite/task 限制 | 核心 | 取决于 task | 部分任务包含 | 独立维度 | 部分 household tasks 包含 |
| Continual-learning transfer | 核心 | 非主要目标 | 非主要目标 | 非主要目标 | 非主要目标 | 非主要目标 |
| Sim-to-real evaluation | 间接 | 间接 | 核心 | 明确研究目标 | 直接包含 simulation 与 real-world tracks | Simulation-only benchmark |
| Bimanual manipulation | 否 | 否 | 经典 setup 中否 | 核心 | 核心 | 核心 |
| Memory diagnosis | 未独立隔离 | Sequence context 相关 | 未独立隔离 | 由独立 RMBench 扩展 | 独立维度 | State transition 需要 temporal tracking |
| Domain randomization | 有限或取决于配置 | Dataset split 与 scene variation | Visual matching 与 variant aggregation | 核心 | Controlled layouts 与 capability-specific tests | Composable task variations |
| Dynamic physics | 未独立隔离 | 有限 | 非主要目标 | 有限 | 非独立维度 | 核心 |
| Protocol 是否计入 inference latency | 否 | 否 | 否 | 否 | 否 | Paired sync/async evaluation |

## 解读边界

- LIBERO 平均成功率本身不能证明 forgetting 或 forward transfer。
- CALVIN chain score 不等于独立 single-task success，因为错误会终止后续 sequence。
- SimplerEnv 只有在 simulation 与 physical protocol 严格配对时，才支持 real-world proxy 结论。
- RoboTwin 2.0 的 clean 与 randomized result 必须分开标注。
- RoboDojo 的 overall result 应结合五个 capability dimensions 阅读，否则 aggregate 会掩盖集中 weakness。
- RoboDyna 的 synchronous 与 asynchronous results 不能互换，只有 asynchronous protocol 会将 measured inference time 计入任务结果。
- 不同 benchmark 的百分比不位于统一量尺上。
