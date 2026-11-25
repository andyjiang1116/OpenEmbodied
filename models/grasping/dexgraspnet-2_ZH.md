# DexGraspNet 2.0

[English](dexgraspnet-2.md) · [Grasping Models](README_ZH.md)

> 面向大规模合成杂乱场景的灵巧手抓取生成方法 · [代码仓库](https://github.com/PKU-EPIC/DexGraspNet2) · [论文](https://openreview.net/forum?id=885c47df6263f6be3a883d6b1bcd3e55048d7f2d)

<p align="center">
  <img src="../../docs/assets/models/grasping/dexgraspnet-2-teaser.png" alt="DexGraspNet 2.0 cluttered-scene dexterous grasping" width="820" />
</p>

*图片来源：官方项目仓库。*

## 概览

- **研究问题：** 在包含邻近障碍物的杂乱场景中生成灵巧手抓取姿态。
- **输入：** 包含目标物体及周边几何信息的场景点云。
- **输出：** 考虑碰撞约束的灵巧手抓取姿态。
- **发表信息：** CoRL 2024。

## 从单物体数据到杂乱场景

原始 DexGraspNet 主要研究孤立物体的稳定抓取姿态生成。DexGraspNet 2.0 将任务扩展到合成杂乱场景，使抓取生成同时考虑目标物体与附近障碍物的几何关系。

该方法使用以局部场景特征为条件的生成模型。公开流程包含合成场景构建、有符号距离计算、抓取生成与评测，也提供了场景级灵巧手抓取数据的处理工具。

## 评估边界

结果受到场景生成、目标选择、碰撞几何、手部模型、仿真验证方式和成功判据影响。单物体评测与杂乱场景评测的任务定义不同，分数不能直接合并比较。

论文包含真机实验；将生成姿态用于具体机器人仍需要感知标定、手部与物体配准、接近路径规划、控制器设计和硬件接触处理。

## 复现说明

官方环境列出 Ubuntu 20.04、Python 3.8、CUDA 11.7、PyTorch 2.0.1、PyTorch3D、TorchSDF 及其他有符号距离工具。多个编译依赖紧密耦合，复现实验时需要保持版本一致。

## 参考资料

- [Official repository](https://github.com/PKU-EPIC/DexGraspNet2)
- [CoRL 2024 paper](https://openreview.net/forum?id=885c47df6263f6be3a883d6b1bcd3e55048d7f2d)
- [DexGraspNet project](https://pku-epic.github.io/DexGraspNet/)
