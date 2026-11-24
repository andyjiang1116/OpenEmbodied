# 机器人操作基准地图

> LIBERO、CALVIN、SimplerEnv、RoboTwin 2.0、RoboDojo 与 RoboDyna 分别在测什么？

[English](README.md) · [基准矩阵](benchmark-matrix_ZH.md) · [协议指南](protocol-guide_ZH.md) · [资料来源](sources.md)

## 概览

机器人操作基准并不是可以相互替换的测试集。它们所关注的能力、机器人与仿真器、示范数据来源、观测和动作接口，以及成功率汇总方式都不相同。一个模型在某个基准上分数更高，并不意味着它在另一个基准上也更强。

本文比较六个有代表性的 benchmark：

- [LIBERO](../../benchmarks/libero_ZH.md) 通过 language-conditioned tabletop tasks，研究 lifelong learning 和 multitask learning 中的 knowledge transfer。
- [CALVIN](../../benchmarks/calvin_ZH.md) 关注 language-conditioned long-horizon control，评估 policy 能连续完成多少条指令。
- [SimplerEnv](../../benchmarks/simplerenv_ZH.md) 研究 simulation evaluation 能否保持 real-robot policy ranking。
- [RoboTwin 2.0](../../benchmarks/robotwin-2_ZH.md) 将 scalable expert-data generation 与 strong domain randomization 下的 bimanual evaluation 结合起来。
- [RoboDojo](../../benchmarks/robodojo_ZH.md) 在 simulation 和标准化 real-robot setup 中，从多个 capability dimensions 评估 generalist policy。
- [RoboDyna](../../benchmarks/robodyna_ZH.md) 在 policy inference 期间仍持续演化的 dynamic scenes 中，评估 physical reasoning 与 time-critical action。

核心原则是：**从需要验证的研究结论出发选择基准，而不是从基准的流行度出发。**

## 六个 Benchmark 对应的核心问题

| 基准 | 主要回答的问题 |
| --- | --- |
| LIBERO | 从早期任务中学到的知识，能否迁移到后续操作任务？ |
| CALVIN | 策略能否理解语言，并连续完成多个相互依赖的任务？ |
| SimplerEnv | 仿真评测能否反映对应真实机器人上的策略相对表现？ |
| RoboTwin 2.0 | 双臂策略能否适应不同任务、物体、场景和视觉变化？ |
| RoboDojo | 通用策略在泛化、记忆、精细操作、长时程和开放指令方面表现如何？ |
| RoboDyna | Policy 能否理解 physical dynamics，并在不会为 inference 暂停的环境中及时行动？ |

## 各自的侧重点

### 🧠 LIBERO：跨任务知识迁移

LIBERO 面向终身机器人学习设计。不同套件分别改变空间关系、物体、目标和任务规模，适合研究前向迁移、知识保持、多任务学习和任务顺序的影响。它也经常作为模仿学习测试集使用，但普通成功率并不等于完整的持续学习实验；只有学习协议同时衡量迁移与遗忘时，才能支持相应结论。

### 🔗 CALVIN：语言条件长时程控制

CALVIN 在桌面环境中设置 Franka 机器人、34 个原子任务及对应语言标注。代表性评测会抽取由五条指令组成的任务链，统计策略连续完成的平均指令数，以及完成不同链长的成功率。因此，它尤其适合观察错误累积、恢复能力、语言落地和时间组合能力。

### 🌉 SimplerEnv：仿真对真机的预测能力

SimplerEnv 在仿真中重建常见的真实机器人评测环境。它的关键价值不只是增加一组仿真任务，而是研究仿真结果是否能够反映真实环境中的策略表现与相对排序。报告结果时应说明环境变体、机器人、视觉匹配或多变体汇总方式、策略检查点，以及对应的真机协议。

### 🦾 RoboTwin 2.0：可扩展双臂操作与鲁棒性

RoboTwin 2.0 提供专家数据生成流程和包含 50 个双臂任务的基准。其物体集合、任务程序、多种机器人形态与域随机化能力，适合研究合成数据生成、双臂协作、环境鲁棒性和仿真到真实迁移。干净场景与随机化场景回答的问题不同，应分别报告结果。

### 🥋 RoboDojo：仿真—真机综合能力评测

RoboDojo 的仿真部分包含 42 个任务，覆盖泛化、记忆、精细操作、长时程执行和开放词汇指令五个能力维度；真机部分包含三个双臂机器人形态上的 18 个任务。策略通过 XPolicyLab 统一接入。RoboDojo 以评测为核心，基准任务、场景布局、计分方式和结果产物与策略实现相互分离。

### ⏱️ RoboDyna：Dynamic Physics 与 Inference-Time Pressure

RoboDyna 在持续受到 gravity、friction、collision、contact 与 state transition 影响的场景中评估 language-conditioned dual-arm policy。Paired synchronous / asynchronous protocols 使用相同 seeds，区别在于 measured policy inference 期间 environment 是否继续演化。20 个 conceptual tasks 隔离五类 physical capabilities，10 个 household tasks 则将这些能力放入更丰富的 office 与 kitchen scenes。Inference latency 因此成为 benchmark 本身的一部分，而不只是 deployment statistic。

## 如何选择

- **持续学习或多任务迁移：** 选择 LIBERO，并保留其任务套件和学习顺序语义。
- **长时程指令执行：** 选择 CALVIN，并报告完整的五指令任务链曲线。
- **用仿真代替部分真机评测：** 选择 SimplerEnv，并检查仿真—真机相关性或排序一致性。
- **双臂数据生成和鲁棒性：** 选择 RoboTwin 2.0，区分干净与随机化设置。
- **诊断通用策略的综合能力：** 选择 RoboDojo，同时报告各能力维度和总体结果。
- **Dynamic physical reasoning 或 latency-aware control：** 选择 RoboDyna，并分开报告 synchronous 与 asynchronous results。

## 哪些结果可以比较

只有当基准版本、任务划分、观测、动作空间、回合长度、评测次数、随机种子、检查点选择和汇总规则一致时，结果才适合直接横向比较。即使基准名称相同，摄像头视角、本体状态、历史帧长度、语言输入或初始状态分布的变化，也可能实质性改变任务。

不同基准之间应比较能力覆盖范围与实验设计，而不是直接比较成功率百分比。更多细节见[协议指南](protocol-guide.md)和[基准矩阵](benchmark-matrix.md)。
