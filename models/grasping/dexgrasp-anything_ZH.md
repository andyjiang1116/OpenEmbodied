# DexGrasp Anything

[English](dexgrasp-anything.md) · [Grasping Models](README_ZH.md)

> 基于物理约束与扩散模型的灵巧手抓取生成方法 · [项目主页](https://dexgraspanything.github.io/) · [代码仓库](https://github.com/4DVLab/DexGrasp-Anything) · [论文](https://arxiv.org/abs/2503.08257)

<p align="center">
  <img src="../../docs/assets/models/grasping/dexgrasp-anything-overview.png" alt="DexGrasp Anything overview and benchmark comparison" width="820" />
</p>

*图片来源：官方项目仓库。*

## 概览

- **研究问题：** 面向不同类别物体生成多样且物理可行的高自由度灵巧手抓取姿态。
- **技术方法：** 在条件扩散模型的训练和采样阶段引入物理约束。
- **机器人手：** 公开实验与数据主要使用 Shadow Hand。
- **发表信息：** CVPR 2025 Highlight。

## 融合物理约束的抓取生成

DexGrasp Anything 将灵巧手抓取建模为条件生成问题。物体几何信息形成语义与空间条件，扩散模型通过逐步去噪生成手部关节配置。物理约束既参与训练阶段的姿态估计，也通过采样阶段的引导机制影响最终输出。

仅依赖数据拟合时，视觉上合理的手部姿态仍可能穿透物体、超出关节限位，或无法形成稳定接触。该方法在生成过程中纳入物理约束；生成姿态仍需要在仿真或真机环境中验证。

## 数据集与跨数据集评测

项目发布的数据集包含超过 340 万个抓取姿态，覆盖超过 1.5 万个物体。论文在 DexGraspNet、UniDexGrasp、MultiDex、RealDex 和 DexGRAB 等数据设置下，报告抓取成功率、穿透程度与姿态多样性等指标。

这些数据集在手部姿态定义、物体预处理、数据划分和评测脚本方面存在差异。解读结果时需要确认坐标变换，以及所用配置是否包含物理引导采样或语言模型生成的条件。

## 复现条件

官方仓库提供代码、数据集、模型权重，以及训练、采样和仿真测试流程。其发布环境使用 Python 3.8、特定版本的 PyTorch/CUDA、PyTorch3D、CSDF 和 Isaac Gym Preview 4；复现时需要核对 GPU 与依赖版本的兼容性。

代码仓库声明使用 MIT 许可证；数据集和上游资源的再分发条件需要分别核对。

## 参考资料

- [Official project page](https://dexgraspanything.github.io/)
- [Official repository](https://github.com/4DVLab/DexGrasp-Anything)
- [CVPR 2025 paper](https://arxiv.org/abs/2503.08257)
- [CVF open-access paper](https://openaccess.thecvf.com/content/CVPR2025/html/Zhong_DexGrasp_Anything_Towards_Universal_Robotic_Dexterous_Grasping_with_Physics_Awareness_CVPR_2025_paper.html)
