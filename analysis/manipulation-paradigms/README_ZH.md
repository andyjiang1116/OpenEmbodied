# 具身操作技术范式

[English](README.md) · [研究分析](../README_ZH.md) · [首页](../../README_ZH.md)

机器人操作系统在预测目标、控制决策位置和观测反馈频率方面存在差异。以下分类用于说明系统设计，不代表能力排名；一个系统也可以组合多种方法。

## 视觉—语言—动作策略

[VLA 模型](../../models/vla/README_ZH.md) 根据视觉观测、语言指令及机器人状态，生成动作 token 或连续动作片段。OpenVLA、SmolVLA、openpi 和 GR00T 在模型主干、动作表示、训练数据和机器人形态接口上各不相同。VLA 的动作输出也可作为 Agent 系统的底层控制组件。详见 [VLA 模型对比](../vla/README_ZH.md)。

## 世界动作模型

[世界动作模型](../../models/wam/README_ZH.md) 联合学习动作与观测随时间的变化。[Unified World Models](../../models/wam/uwm_ZH.md) 耦合视频与动作扩散；[DreamZero](../../models/wam/dreamzero_ZH.md) 利用预训练视频模型联合预测环境与动作；[Fast-WAM](../../models/wam/fast-wam_ZH.md) 保留视频联合训练，但推理时不显式生成未来视频。[OpenWAM](../../models/wam/openwam_ZH.md) 提供模块化研究框架，并发布 OpenWAM-α 预训练策略。因此，WAM 并不对应单一的“先想象、后执行”流程。

## Agent 式控制

[Agent 式具身操作](../../systems/agents/README_ZH.md) 将多模态推理模型放入“观测—决策—执行—反馈”闭环。Agent 可以直接生成受约束的机器人指令、审查学习型策略提出的轨迹，也可以仅在需要恢复时接管控制。[GPT-6 Astra as an Embodied Policy](../../systems/agents/gpt-as-policy_ZH.md)、[π0.5 + Astra 按需介入](../../systems/agents/pi05-call-astra_ZH.md) 和 [GPT-Policy](../../systems/agents/gpt-policy_ZH.md) 分别展示这些控制接口。工具校验与底层控制也是系统的一部分，实验结果不能只归因于语言模型。

## 抓取组件

[抓取模型](../../models/grasping/README_ZH.md) 估计候选抓取，或生成灵巧手配置，可为 VLA、WAM 和 Agent 系统提供感知结果与动作建议。预测的抓取姿态仍需经过坐标变换、可行性检查、运动规划与实际执行。

## 对照维度

| 维度 | 应记录的问题 |
| --- | --- |
| 预测目标 | 输出机器人动作、未来观测、抓取姿态，还是工具调用？ |
| 控制接口 | 使用关节动作、末端执行器目标、技能调用，还是审查候选策略？ |
| 训练信号 | 使用机器人示教、视频预测、无动作标注视频，还是上下文示例？ |
| 执行闭环 | 动作片段长度、观测频率、推理延迟和物理时间如何处理？ |
| 系统边界 | 哪些规划器、控制器、逆运动学、安全约束与恢复逻辑位于模型之外？ |
| 评测设置 | 任务集合、机器人形态、随机种子、成功判定、运行时间和对照基线是什么？ |

只有任务与协议对齐，基准分数才适合直接比较。具体差异见[操作评测基准对比](../manipulation-benchmarks/README_ZH.md)。
