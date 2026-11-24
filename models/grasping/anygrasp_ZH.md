# AnyGrasp

[English](anygrasp.md) · [Grasping Models](README_ZH.md)

> 基于 point cloud 的 parallel-gripper grasp detection 与 tracking · [Project](https://graspnet.net/anygrasp.html) · [SDK](https://github.com/graspnet/anygrasp_sdk) · [Paper](https://arxiv.org/abs/2212.08333)

<p align="center">
  <img src="../../docs/assets/models/grasping/anygrasp-demo.gif" alt="AnyGrasp grasp perception demonstration" width="820" />
</p>

*图片来源：官方项目演示。*

## 概览

- **问题：** 在 cluttered 或 dynamic scene 中检测稳定的 6-DoF grasp pose，并在时间维度持续跟踪。
- **End effector：** Parallel gripper。
- **Observation：** 由 depth sensor 获取的 point cloud，也可以通过目标区域或 mask 进行裁剪。
- **Output：** Grasp pose、width、score，以及供下游 motion planning 使用的 tracked candidates。

## 为什么重要

很多 grasp detector 会独立处理每一帧。AnyGrasp 将 spatial grasp perception 与 temporal correspondence 结合，使机器人在相机、物体或本体运动时仍能保持稳定的 grasp candidates。官方演示覆盖 clutter removal、deformable object、transparent object 和 moving target，体现了它面向实际抓取吞吐量的定位。

## 技术结构

Spatial component 延续 GraspNet 与 Graspness / GSNet 路线中的 dense graspability reasoning，并结合 objectness filtering 和 model-free collision checking。Temporal component 在连续观测之间关联 grasp，从而降低 pose jitter，避免每一帧都从头生成候选。

官方 SDK 提供 dense prediction、object-mask filtering 与 collision detection 选项。Dense mode 会用更多显存和推理时间换取更密集的候选，官方将其定位为特殊场景选项，而不是默认设置。

## 部署边界

AnyGrasp 是 perception component，不是完整的 pick-and-place policy。实际机器人系统仍需要 calibrated RGB-D sensing、point-cloud preprocessing、robot–camera transform、candidate selection、inverse kinematics、motion planning、gripper control 和 failure recovery。

官方 SDK 列出的环境包括 Python 3.6–3.10、PyTorch 1.7.1+、CUDA、MinkowskiEngine 和编译后的 `pointnet2`。在把 demo 环境视为可部署方案之前，需要针对目标 GPU 与操作系统重新核对兼容性。

## 发布与 License 边界

官方仓库公开 SDK wrapper 与示例，但由于其声明的 IP 限制，AnyGrasp 核心 library 通过绑定机器的 license registration 分发。使用者需要提交 machine feature ID 并申请 license。这与完整开源实现有本质区别，在产品集成或复现结论中必须明确说明。

## 原始来源

- [Official project page](https://graspnet.net/anygrasp.html)
- [Official AnyGrasp SDK](https://github.com/graspnet/anygrasp_sdk)
- [AnyGrasp paper](https://arxiv.org/abs/2212.08333)
- [GraspNet project](https://graspnet.net/)
