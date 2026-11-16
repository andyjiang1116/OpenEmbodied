# Open VLA Landscape

> 哪些模型真正开放、可比较、可复现？

[English](README.md) · [详细模型矩阵](model-matrix.md) · [Benchmark 说明](benchmark-notes.md) · [来源清单](sources.md)

## 摘要

“开放 VLA”可能代表完全不同的开放程度：有的项目只公开推理代码，有的权重采用单独许可证，有的基础模型仍需面向具体任务微调，也有不同项目虽然都报告 LIBERO，却使用了不可直接比较的协议。

OpenEmbodied 第一版选择四条具有代表性的开源路线：

- [OpenVLA / OpenVLA-OFT](../../models/openvla.md)：建立在预训练 VLM 和 Open X-Embodiment 数据上的经典 7B VLA 路线。
- [SmolVLA](../../models/smolvla.md)：与 LeRobot 生态深度集成的 450M 轻量 flow-matching 策略。
- [π0 / π0-FAST / π0.5 与 openpi](../../models/openpi.md)：同时覆盖 flow matching 与自回归动作表示，并公开基础和任务权重。
- [Isaac GR00T N1.7](../../models/gr00t-n1.7.md)：提供跨机器人形态的微调、评测与部署链路。

核心结论是：**脱离机器人形态、任务、算力、许可证和评测协议，不存在唯一“最开放”或“最好”的 VLA。**

## 快速对比

| 项目 | 主要优势 | 动作生成 | 官方起点 | 实践门槛 |
| --- | --- | --- | --- | --- |
| OpenVLA | 经典研究基线和广泛 OXE 预训练 | 离散动作 token；OFT 使用连续动作 | 7B 权重、推理、微调与评测代码 | 中高 |
| SmolVLA | 模型轻量并连接低成本机器人工作流 | 连续动作与 flow matching | 450M 基础模型、LeRobot 训练和推理工具 | 低到中 |
| openpi | 多种 π 系列策略及基础、任务权重 | π0/π0.5 使用 flow matching；π0-FAST 使用自回归 token | 训练、推理、服务和 LIBERO 示例 | 中高 |
| GR00T N1.7 | 跨形态训练与部署工程栈 | diffusion-transformer 连续动作头 | 基础/微调权重、Benchmark 指南、策略服务 | 高 |

详细字段和来源限制见 [model-matrix.md](model-matrix.md)。

## 如何定义“开放”

OpenEmbodied 不使用单一的“开源/不开源”标签，而是分别记录：

1. **代码：** 推理、微调、预训练、评测和部署代码分别判断。
2. **权重：** 基础权重与任务权重可能采用不同发布方式或条款。
3. **数据：** 论文写出数据名称，不代表完整训练混合数据可以下载。
4. **许可证：** 代码、权重和底层模型可能受不同许可证约束。
5. **评测：** 相同 Benchmark 名称不代表任务、种子、视角、步数和统计方式相同。
6. **部署：** 能够启动策略服务，不等于已经在目标机器人上完成端到端验证。

## 主要发现

### 1. SmolVLA 最适合作为低成本起点

SmolVLA 提供 450M、Apache-2.0 的基础模型，使用连续动作和 flow matching，并接入 LeRobot 的数据、训练、评测与硬件工具。官方文档提供直接加载模型的路径，并明确基础模型需要针对具体任务微调。因此，它最适合作为 OpenEmbodied 第一个实际复现对象。

### 2. OpenVLA 仍是重要基线，但不能只看 MIT 标签

OpenVLA 仓库采用 MIT 许可证，并提供推理、微调、服务与评测材料；但公开的 7B 权重建立在 Llama 2 之上，模型使用条件不能只用仓库的 MIT 许可证概括。OpenVLA-OFT 还改变了动作预测等关键实现，因此比较时必须标注具体版本和训练配方。

### 3. openpi 对系统边界的说明很有价值

官方仓库明确区分 π0、π0-FAST 和 π0.5，发布基础权重及多种机器人、任务权重，给出显存预估并支持远程策略服务。它也明确提醒：把模型迁移到不同机器人上不一定成功。这类限制说明本身就是重要证据。

### 4. GR00T N1.7 的工程链路最完整

GR00T N1.7 文档覆盖数据转换、推理、微调、策略服务、TensorRT 部署，以及 LIBERO、SimplerEnv 和 SO100 的专用流程。代码采用 Apache-2.0，权重采用 NVIDIA Open Model License。工程覆盖面很广，但 gated backbone、子模块、GPU 依赖和平台差异也提高了入门成本。

### 5. 不能把 Benchmark 结果压缩成一个排行榜

LIBERO 结果可能受到任务套件、历史观测、图像视角、动作表示、微调配方、rollout 长度、随机种子和统计方式影响；SO100/SO101 真机实验还受到硬件与采集流程影响。因此本专题记录“结果 + 协议”，而不是对单个分数排序。详见 [benchmark-notes.md](benchmark-notes.md)。

## 按目标选择

- **第一次尝试 VLA 或算力有限：** 从 SmolVLA 和 LeRobot 开始。
- **研究经典开源 VLA 与 OXE 路线：** 先看 OpenVLA，再比较 OFT。
- **研究 flow matching、FAST tokenizer 或 DROID/ALOHA 适配：** 选择 openpi。
- **需要较完整的跨形态部署链路：** 评估 GR00T N1.7。
- **比较论文结果：** 先统一评测协议，不要只比较模型名称。

