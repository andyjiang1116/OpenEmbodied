![OpenEmbodied](docs/assets/openembodied-logo.svg)

### 系统化的 Embodied AI Research Atlas

`感知` · `推理` · `世界模型` · `导航` · `操作` · `部署`

![OpenEmbodied research atlas](docs/assets/openembodied-atlas.png)

[English](README.md) · [关于项目](#-关于项目) · [技术目录](#-技术目录) · [研究地图](#-研究地图) · [参与贡献](#-参与贡献)

---

## 🌐 关于项目

Embodied AI 不是单一模型或 Benchmark，而是一个贯穿 perception、reasoning、prediction、planning、control、evaluation、simulation 与 physical deployment 的系统问题。

**OpenEmbodied 将这个领域组织为一张彼此连接的技术地图。** 项目把分散的论文、代码仓库、Dataset、Benchmark 和机器人系统整理为清晰的研究路径，说明每项工作贡献了什么、不同组件如何关联，以及哪些结果可以或不可以直接比较。

目标不是收集所有内容，而是让这个领域更容易理解、检索，并能够在已有工作之上继续构建。

## ✨ OpenEmbodied 的内容结构

OpenEmbodied 通过三个相互连接的层次组织具身智能研究：

- **Research Atlas｜技术版图：** 将 perception、reasoning、world models、planning 与 control 组成的 intelligence，同 navigation、manipulation、datasets、simulators、robots 和 real-world deployment 连接起来。
- **Technical Catalog｜技术目录：** 提供 models、policies、benchmarks 及其关联资源的结构化档案。
- **Research Maps｜研究地图：** 连接相关工作，按照一致的技术维度进行比较，同时避免把不同任务和 protocol 简化为同一排名。

这一结构面向长期扩展。新的专题会进入稳定的 capability map，而不是继续堆叠成彼此割裂的论文列表。

## 🗂️ 技术目录

### 🧠 [Models & Policies｜模型与策略](models/README_ZH.md)

按 capability 组织 VLA、grasp perception、dexterous grasp generation，以及后续扩展的模型家族。

[VLA Models →](models/vla/README_ZH.md) · [Grasping Models →](models/grasping/README_ZH.md)

### 📏 [Evaluation Benchmarks｜评测基准](benchmarks/README_ZH.md)

理解不同 evaluation suite 测量的能力、关键 protocol，以及如何正确阅读报告结果。

[浏览 Benchmarks →](benchmarks/README_ZH.md)

## 🧭 研究地图

### 🔭 [Open VLA Landscape](docs/vla-landscape/README_ZH.md)

从 architecture、action generation、adaptation、compute、evaluation 与 deployment surface 对比开放 VLA 路线。

[Model Matrix →](docs/vla-landscape/model-matrix_ZH.md)

### 🦾 [Manipulation Benchmark Map](docs/benchmark-map/README_ZH.md)

理解 LIBERO、CALVIN、SimplerEnv、RoboTwin 2.0、RoboDojo 与 RoboDyna 分别测试哪些能力。

[Benchmark Matrix →](docs/benchmark-map/benchmark-matrix_ZH.md) · [Protocol Guide →](docs/benchmark-map/protocol-guide_ZH.md)

### 持续扩展的 Atlas

仓库将逐步建设以下独立专题：

`perception` · `reasoning` · `world-models` · `navigation` · `datasets` · `simulators` · `robots` · `deployment`

每个专题遵循一致原则：范围清晰、taxonomy 稳定、基于 primary sources、进行有意义的比较，并保留明确的 system context。

## 🤝 参与贡献

OpenEmbodied 欢迎内容纠错、新增技术档案、完善 Research Landscape、Benchmark 分析和实际实现经验。

高质量贡献应当基于事实和原始来源，具有清晰的技术范围，并说明实际发布了什么、测量了什么，以及哪些部分仍不确定。可以通过 Issue 推荐新方向、资源或提交纠错。

## 🙏 致谢

OpenEmbodied 建立在具身智能研究者、工程师、教育者与开源社区的工作之上。

本仓库引用的外部论文、代码、Dataset、图片及其他资源，其权利归原作者所有。使用时请遵循各来源的 License 与引用要求。
