<div align="center">
  <img src="docs/assets/openembodied-wordmark.png" alt="OpenEmbodied" width="760" />

  <p><strong>以证据为核心的具身智能研究地图</strong></p>
  <p>追踪前沿 · 横向比较 · 复现关键工作</p>
  <p>
    <a href="README.md">English</a>
    ·
    <a href="#-为什么是-openembodied">为什么是 OpenEmbodied</a>
    ·
    <a href="#-内容导航">内容导航</a>
  </p>
</div>

---

## 🌐 关于项目

具身智能发展迅速，但更多信息并不一定带来更好的理解。论文使用不同的数据集、评测协议、硬件与报告口径；许多仓库只展示成功结果，却没有记录运行条件和失败过程。

**OpenEmbodied 希望把分散的资源转化为结构化、可比较、可验证的知识。**

本项目不止收集链接，而是记录一项工作解决了什么问题、方法如何运行、证据是否充分、复现需要付出什么成本，以及它在哪些条件下不再适用。

> [!IMPORTANT]
> OpenEmbodied 目前处于基础建设阶段。我们将先建立内容标准和首批旗舰专题，再逐步扩展覆盖范围。

## ✨ 为什么是 OpenEmbodied

| 常见问题 | OpenEmbodied 的处理方式 |
| --- | --- |
| 论文列表很长，但缺少上下文 | 使用统一结构的 Research Profile |
| 不同工作的结果难以比较 | 补充数据集、基准、指标与评测协议 |
| “开源”但复现条件不透明 | 明确代码、权重、数据、许可、算力与环境状态 |
| 只展示成功 Demo | 记录限制、失败模式与尚未解决的问题 |
| 结论缺少明确依据 | 提供原始来源、适用范围与可复现上下文 |

## 🧭 内容导航

### 🔭 [Open VLA Landscape](comparisons/vla-landscape/README_ZH.md)

从架构、动作生成、开放程度、算力和评测等角度，对比 OpenVLA、SmolVLA、openpi 与 GR00T N1.7。

### 🦾 [机器人操作基准地图](comparisons/benchmark-map/README_ZH.md)

梳理 LIBERO、CALVIN、SimplerEnv、RoboTwin 2.0 和 RoboDojo 分别在测什么，以及哪些结果可以合理比较。

## 🗂️ 仓库内容结构

```text
追踪前沿 → 理解工作 → 验证结果 → 结合场景做出选择
```

- **Frontier Watch｜前沿追踪：** 关注重要进展，并解释其价值。
- **Research Profiles｜研究档案：** 简明整理模型、论文、数据集和基准的事实信息与原始来源。
- **Reproduction Reports｜复现报告：** 记录可运行实验、实际结果与失败情况。
- **Comparison Guides｜对比指南：** 将独立工作组织成面向实际选择的专题地图，例如上面的两篇指南。

## 🤝 参与贡献

OpenEmbodied 欢迎内容纠错、原始资料更新、Research Profile、Benchmark 笔记与复现报告。

一项有价值的贡献应尽量包含：

- 官方来源与公开时间；
- 所属研究方向；
- 客观简介与收录理由；
- 代码、权重、数据和许可证状态；
- 可用的评测或复现证据；
- 已知限制与尚未解决的问题。

贡献模板将在第一版仓库结构中提供。在此之前，可以通过 Issue 推荐资源或提交纠错。

## 🙏 致谢

感谢推动具身智能发展的研究者、工程师、教育者与开源贡献者。

本仓库收录的外部论文、代码、数据集及其他资源，其权利归原作者所有。使用时请遵循各来源的许可与引用要求。
