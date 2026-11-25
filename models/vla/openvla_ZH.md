# OpenVLA / OpenVLA-OFT

[English](openvla.md)

> **类别：** 视觉—语言—动作模型 · [官方仓库](https://github.com/openvla/openvla) · [项目主页](https://openvla.github.io/) · [论文](https://arxiv.org/abs/2406.09246) · [OpenVLA-OFT](https://openvla-oft.github.io/)

<p align="center">
  <img src="../../docs/assets/models/openvla-model.jpg" alt="OpenVLA model architecture" width="820" />
</p>

<p align="center"><em>OpenVLA 根据图像与语言指令生成离散化的机器人动作。图片来源：<a href="https://openvla.github.io/">官方项目主页</a>。</em></p>

## 概览

- **研究定位：** 基于 Open X-Embodiment 数据训练的开放 VLA 模型。
- **模型规模：** 原始模型约 70 亿参数。
- **输入与输出：** 根据图像和语言指令预测机器人动作；状态输入、相机视角及动作接口取决于具体权重与适配方案。
- **动作表示：** 原始 OpenVLA 使用离散动作 token；OpenVLA-OFT 引入连续动作预测。

## 技术贡献

OpenVLA 公开了模型权重和推理、微调、评测、策略服务代码。其技术路线展示了如何将预训练视觉语言模型适配为机器人策略，以及如何利用 Open X-Embodiment 数据进行跨数据集训练。

## 架构与数据

原始模型基于 Prismatic-7B 视觉语言模型，由 DINOv2 与 SigLIP 提取视觉特征，Llama 2 处理多模态序列。官方资料报告使用约 97 万段 Open X-Embodiment 机器人轨迹进行训练。预测动作需使用对应机器人或数据集的归一化统计量还原。

整体流程可以拆为四步：

1. DINOv2 与 SigLIP 编码机器人相机图像。
2. 投影层将视觉特征映射到语言模型的嵌入空间。
3. Llama 2 主干模型结合视觉表示与自然语言指令预测动作 token。
4. 将动作 token 解码，并按目标机器人的统计量进行反归一化。

这种设计将动作预测表示为下一个 token 的预测任务，能够复用预训练视觉语言模型；离散化精度与逐 token 推理延迟则是需要考虑的控制因素。

## 适配与控制

原始仓库支持全参数微调、LoRA 和量化 LoRA。适配新机器人或数据集时，需要匹配数据标识和动作归一化统计量，因为相同的归一化输出在不同机器人上可能对应不同的实际动作。仓库也提供 REST 策略服务，允许推理端与机器人客户端分开运行。

OpenVLA-OFT 是独立的优化微调方案，并非原始权重的改名。它采用连续动作头与动作分块等设计。引用结果时需要同时说明基础权重和适配方案。

## 已开放内容

- MIT-licensed repository code。
- `openvla-7b` 与较早的 `openvla-v01-7b` checkpoint。
- 与 Hugging Face 生态兼容的推理接口。
- LoRA、quantized LoRA、full fine-tuning、training、evaluation 与 REST serving。
- 使用 continuous actions 的 OpenVLA-OFT recipe。

## 开放性与使用边界

- 仓库代码与模型权重适用的许可条款不同；主要权重基于 Llama 2，还需遵守其相关条款。
- Open X-Embodiment 由多个 dataset 构成，各数据源的开放范围与 license 并不统一。
- “OpenVLA result” 过于宽泛，必须进一步说明使用的是原始方案、OFT，还是其他后续 recipe。

## 研究用途

OpenVLA 可用于研究开放 VLA 架构、Open X-Embodiment 预训练，以及约 70 亿参数策略的参数高效适配。对比 SmolVLA、openpi 和 GR00T 时，应同时考虑模型规模、动作表示与部署条件的差异。

## 参考资料

- [Official repository](https://github.com/openvla/openvla)
- [Project page](https://openvla.github.io/)
- [Paper](https://arxiv.org/abs/2406.09246)
- [OpenVLA-OFT](https://openvla-oft.github.io/)
