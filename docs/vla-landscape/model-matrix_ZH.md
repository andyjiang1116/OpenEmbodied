# Open VLA 模型矩阵

[English](model-matrix.md) · [专题概览](README_ZH.md) · [Benchmark 说明](benchmark-notes_ZH.md) · [来源清单](sources.md)

本矩阵区分项目官方公开的事实与 OpenEmbodied 的归纳。“Available” 表示存在官方 artifact 或明确文档路径，不代表 OpenEmbodied 已经实际运行。

## Architecture 与 Interface

| 项目 | OpenVLA / OFT | SmolVLA | openpi | GR00T N1.7 |
| --- | --- | --- | --- | --- |
| 主要定位 | 经典开放 VLA baseline 与 OXE pretraining | LeRobot 中的 compact VLA | π-family models 与 robot adaptation | Cross-embodiment training 和 deployment stack |
| 代表规模 | 7B | 450M | π0 / π0-FAST / π0.5 family | 3B released checkpoint |
| 动作生成 | 原版为 discrete action tokens；OFT 使用 continuous head | Flow matching continuous action chunks | π0/π0.5 使用 flow matching；π0-FAST 使用 autoregressive tokens | Diffusion-transformer continuous action head |
| 主要生态 | PyTorch、Hugging Face、Open X-Embodiment | LeRobot datasets、training 与 hardware | JAX/PyTorch、LeRobot-format data、WebSocket serving | LeRobot-format data、ZMQ、TensorRT、Isaac ecosystem |
| 入门门槛 | 中高 | 低至中 | 中高 | 高 |

## Code、Weights 与 Data

| 项目 | Code | Weights | Training data 可见性 | License 要点 |
| --- | --- | --- | --- | --- |
| OpenVLA | Inference、fine-tuning、training、evaluation 与 serving | 公开 7B checkpoints | 公开 OXE mixture 说明，各 source dataset 条款不同 | Repository 为 MIT；weights 还涉及 Llama 2 terms |
| SmolVLA | LeRobot 内提供 training、inference 与 evaluation | `lerobot/smolvla_base` | 使用开放社区 LeRobot datasets，官方说明少于 3 万 episodes | Code 与 base model card 为 Apache-2.0 |
| openpi | Training、configuration、data conversion 与 serving | Base 与部分 expert checkpoints | 官方说明超过 1 万小时 robot data，完整 proprietary mixture 不公开 | Apache-2.0 code，同时需要检查 upstream model terms |
| GR00T N1.7 | Training、inference、serving 与 deployment | Base 与 selected fine-tuned checkpoints | 支持公开与自定义 LeRobot-format data | Apache-2.0 code；weights 使用 NVIDIA Open Model License |

## 输入、动作与适配

| 项目 | 典型输入 | 动作接口 | 新 Robot 的适配方式 |
| --- | --- | --- | --- |
| OpenVLA | Image、language，部分 recipe 加入 state/history | Dataset-specific normalized actions | Dataset conversion、normalization statistics、LoRA/full fine-tuning |
| SmolVLA | 多 camera images、robot state、可选 language | Continuous action chunks | 在 LeRobot dataset 与 policy config 上 fine-tune |
| openpi | 多图像、language、proprioception | Continuous flow actions 或 FAST tokens | Data conversion、robot config、normalization、LoRA/full tuning |
| GR00T N1.7 | Images、language、robot state | Embodiment-specific continuous chunks | LeRobot conversion、embodiment config、fine-tuning 与 serving |

## 选择建议

- 理解经典开放 VLA architecture 与 OXE 路线：选择 OpenVLA，并区分原版与 OFT。
- 以较低成本完成第一个 end-to-end VLA experiment：选择 SmolVLA。
- 比较 flow matching、FAST tokenization 或研究 remote policy serving：选择 openpi。
- 研究 cross-embodiment deployment、TensorRT 或 NVIDIA robotics stack：选择 GR00T N1.7。

这些项目在不同 benchmark、observation、action interface 与 adaptation recipe 下报告结果。本矩阵用于理解系统设计，不构成统一性能排名。
