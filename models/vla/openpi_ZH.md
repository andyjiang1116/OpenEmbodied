# π0 / π0-FAST / π0.5 via openpi

[English](openpi.md)

> **类别：** 视觉—语言—动作模型 · [官方仓库](https://github.com/Physical-Intelligence/openpi) · [π0 项目介绍](https://www.pi.website/blog/pi0) · [π0.5 项目介绍](https://www.pi.website/blog/pi05) · [论文](https://arxiv.org/abs/2410.24164)

<p align="center">
  <img src="../../docs/assets/models/openpi-overview.jpg" alt="π0 model, data, and adaptation overview" width="820" />
</p>

<p align="center"><em>π0 的模型、数据与适配流程。图片来源：<a href="https://arxiv.org/abs/2410.24164">原论文</a>。</em></p>

## 概览

- **定位：** Physical Intelligence 机器人策略模型系列的公开实现。
- **主要变体：** π0、π0-FAST 与 π0.5。
- **动作生成：** π0 与当前公开的 π0.5 动作头使用流匹配；π0-FAST 使用自回归动作 token。

## 技术贡献

openpi 在同一模型系列中提供不同的动作表示，并发布基础权重及多个面向特定机器人或任务的权重。仓库还包含数据转换、归一化、训练、策略服务及机器人和仿真示例，覆盖从数据到部署的主要接口。

## 模型系列

- **π0** 结合预训练视觉语言模型与流匹配动作模块，生成连续动作。
- **π0-FAST** 使用 FAST 动作 token，并通过自回归预测生成动作序列。
- **π0.5** 扩展开放场景中的策略能力；openpi 当前实现支持其流匹配动作头。

这些名称对应不同的模型与动作生成方案。报告结果时需要明确具体权重，而不能将“openpi”视为单一策略。

## 数据与适配流程

官方资料描述的预训练数据来源包括大规模视觉语言数据、开放机器人数据集，以及 Physical Intelligence 的多机器人数据。公开仓库支持目标数据转换、归一化统计计算、机器人专用配置，以及 LoRA 或全参数微调。

部署时，策略进程可以通过 WebSocket 提供动作服务，机器人或仿真客户端独立提交观测数据。推理设备与机器人控制端因此可以分开运行，但仍需匹配观测和动作接口。

## 已开放内容

- Apache-2.0 repository code，以及 Gemma 等 upstream license notices。
- π0、π0-FAST 与 π0.5 base checkpoints。
- 面向 DROID、ALOHA 与 LIBERO 的 expert checkpoints。
- 以 JAX 为主的训练代码及公开 PyTorch support。
- LeRobot 格式转换、微调、本地推理与 WebSocket 服务。
- Docker 与 `uv` installation path。

## 官方硬件需求

仓库给出的单 GPU 估算为：inference 需要超过 8 GB GPU memory，LoRA fine-tuning 超过 22.5 GB，full fine-tuning 超过 70 GB。官方测试系统为 Ubuntu 22.04。这些是项目侧估算，不代表所有配置下的独立测量结果。

## 使用边界

- 官方说明：针对特定机器人开发的模型权重，不保证能够直接适配其他平台。
- Expert checkpoint 与 base checkpoint 的泛化表现不同，robot interface 与 normalization 必须匹配。
- 仓库许可与模型依赖项的使用条款需分别核对。
- LIBERO 结果只有在 checkpoint 与 protocol 对齐后才适合比较。

## 研究用途

openpi 提供流匹配、自回归动作 token、跨机器人形态适配和远程策略服务等不同技术路径。接入新机器人时需要校验观测和动作变换、归一化统计与控制频率。

## 参考资料

- [Official repository](https://github.com/Physical-Intelligence/openpi)
- [π0 project page](https://www.pi.website/blog/pi0)
- [π0.5 project page](https://www.pi.website/blog/pi05)
- [π0 paper](https://arxiv.org/abs/2410.24164)
