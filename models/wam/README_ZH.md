# 世界动作模型

[English](README.md) · [模型目录](../README_ZH.md) · [具身操作技术范式](../../analysis/manipulation-paradigms/README_ZH.md)

世界动作模型（WAM）将机器人动作预测与环境变化建模结合起来。不同方法的训练目标和推理流程并不相同：未来视频的生成可能发生在训练阶段、执行阶段，或两者兼有。

| 方法 | 世界与动作的建模方式 | 推理方式 |
| --- | --- | --- |
| [Unified World Models](uwm_ZH.md) | 联合进行视频与动作扩散，并分别控制两种模态的扩散时间步 | 同一模型可用于策略与世界预测 |
| [DreamZero](dreamzero_ZH.md) | 基于预训练视频扩散模型联合建模未来视频与动作 | 生成环境与动作轨迹，执行闭环控制 |
| [Fast-WAM](fast-wam_ZH.md) | 通过视频预测联合训练学习世界表征 | 无需显式生成未来视频，直接预测动作 |

比较这些方法时，应同时考察视频数据的作用、动作表示、训练数据、观测接口、推理延迟与机器人形态。详见[跨范式分析](../../analysis/manipulation-paradigms/README_ZH.md)。
