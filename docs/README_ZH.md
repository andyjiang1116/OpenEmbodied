# 专题文档

> 收录研究全景、基准地图、复现报告与公共文档。

[English](README.md) · [模型](../models/README_ZH.md) · [基准](../benchmarks/README_ZH.md)

## 研究专题

### 🔭 [Open VLA Landscape](vla-landscape/README_ZH.md)

从模型设计、动作生成、训练与适配、开放程度、算力和评测等方面比较 OpenVLA、SmolVLA、openpi 与 GR00T N1.7。

### 🦾 [机器人操作基准地图](benchmark-map/README_ZH.md)

解释 LIBERO、CALVIN、SimplerEnv、RoboTwin 2.0 和 RoboDojo 分别评测什么、协议有何差异，以及哪些结果适合比较。

## 仓库结构

```text
models/       模型与策略档案
benchmarks/   评测基准档案
datasets/     数据集档案
simulators/   仿真器与环境档案
robots/       机器人平台与形态档案
docs/         跨实体专题、复现报告与公共素材
```

实体目录使用稳定的小写名称，每个实体只维护一篇主档案。专题文档通过链接引用实体档案，不重复维护同一组技术事实，方便后续持续扩展和更新。
