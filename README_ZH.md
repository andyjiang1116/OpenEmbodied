<p align="center">
  <img src="docs/assets/openembodied-logo.svg" alt="OpenEmbodied" width="820" />
</p>

<p align="center">
  <strong>具身智能领域的模型、评测基准与研究图谱。</strong>
</p>

![OpenEmbodied research atlas](docs/assets/openembodied-atlas.png)

<p align="center">
  <a href="README.md">English</a>
  &nbsp;·&nbsp;
  <a href="#-关于项目">关于项目</a>
  &nbsp;·&nbsp;
  <a href="#-研究方向">研究方向</a>
  &nbsp;·&nbsp;
  <a href="#-规划中的研究主题">规划中的研究主题</a>
  &nbsp;·&nbsp;
  <a href="#-参与贡献">参与贡献</a>
</p>

---

## 🌐 关于项目

OpenEmbodied 是面向具身智能研究的资料库，按研究方向组织模型与评测基准档案，并通过横向分析梳理技术路线、评测协议和已发表的研究成果。当前内容聚焦机器人操作，其他研究方向见下文。

## 🗂️ 研究方向

各研究方向汇集代表性方法、评测基准与横向分析。

### 🦾 Embodied Manipulation｜具身操作

聚焦机器人操作任务中的策略学习、抓取生成与性能评测。

#### [Vision-Language-Action](models/vla/README_ZH.md)

将视觉观测与语言指令映射为机器人动作的策略模型。

- [OpenVLA / OpenVLA-OFT](models/vla/openvla_ZH.md)
- [SmolVLA](models/vla/smolvla_ZH.md)
- [π0 / π0-FAST / π0.5](models/vla/openpi_ZH.md)
- [NVIDIA Isaac GR00T N1.7](models/vla/gr00t-n1.7_ZH.md)

##### VLA 模型对比

对比开放 VLA 系统的模型架构、动作表示、开放资源与评测协议。

- [研究概览](maps/vla-landscape/README_ZH.md) — 模型系列，以及代码、权重、数据和部署工具的开放情况。
- [技术对比](maps/vla-landscape/model-matrix_ZH.md) — 对照架构、动作生成方式与开放资源。
- [评测可比性](maps/vla-landscape/benchmark-notes_ZH.md) — 评测设置及跨模型比较的边界。
- [参考资料](maps/vla-landscape/references_ZH.md) — 官方论文、仓库与文档。

#### [Grasping](models/grasping/README_ZH.md)

涵盖平行夹爪的抓取检测与灵巧手的抓取姿态生成。

- [AnyGrasp](models/grasping/anygrasp_ZH.md)
- [UniDexGrasp](models/grasping/unidexgrasp_ZH.md)
- [DexGraspNet 2.0](models/grasping/dexgraspnet-2_ZH.md)
- [DexGrasp Anything](models/grasping/dexgrasp-anything_ZH.md)

#### Manipulation Evaluation｜操作评测

覆盖知识迁移、长程控制、仿真与真实场景的一致性、鲁棒性及动态操作等评测主题。[评测基准索引](benchmarks/README_ZH.md)。

- [LIBERO](benchmarks/libero_ZH.md) — 跨任务套件的终身学习与多任务操作。
- [CALVIN](benchmarks/calvin_ZH.md) — 语言条件下的长程操作任务。
- [SimplerEnv](benchmarks/simplerenv_ZH.md) — 仿真评测与真实场景中策略排序的一致性。
- [RoboTwin 2.0](benchmarks/robotwin-2_ZH.md) — 双臂操作数据生成与鲁棒性评测。
- [RoboDojo](benchmarks/robodojo_ZH.md) — 仿真与真机环境中的通用操作策略评测。
- [RoboDyna](benchmarks/robodyna_ZH.md) — 动态场景中的物理推理与时效性操作。

##### 操作评测基准对比

对比操作评测基准的任务、机器人平台、指标与实验协议。

- [评测概览](maps/benchmark-map/README_ZH.md) — 六项操作评测基准的侧重点与适用场景。
- [基准对比](maps/benchmark-map/benchmark-matrix_ZH.md) — 对照任务、机器人平台、环境、观测输入与指标。
- [评测协议](maps/benchmark-map/protocol-guide_ZH.md) — 解读或复现已报告结果前需要核对的条件。
- [参考资料](maps/benchmark-map/references_ZH.md) — 官方论文、仓库与文档。

## 🛰️ 规划中的研究主题

后续研究主题覆盖具身能力，以及支撑这些能力的数据、仿真和机器人系统：

| 主题 | 技术重点 |
| --- | --- |
| **Perception｜感知** | 三维场景理解、视觉语义定位、可供性预测与主动感知 |
| **Embodied Reasoning｜具身推理** | 空间推理、任务规划、记忆与决策 |
| **World Models｜世界模型** | 动力学预测、视频与动作生成、基于模型的规划 |
| **Navigation｜导航** | 视觉语言导航、定位、建图与探索 |
| **Data & Simulation｜数据与仿真** | 具身数据集、合成数据生成、仿真平台与评测环境 |
| **Robotic Systems｜机器人系统** | 机器人平台、策略部署与 sim-to-real 迁移 |

## 🤝 参与贡献

欢迎补充模型与评测基准档案、横向分析及参考文献，并修正文档中的错误。

请优先引用论文、官方仓库或项目文档，并区分原作者报告的结果与独立验证结果。可通过 Issue 提议研究主题或提交勘误。

## 🙏 致谢

OpenEmbodied 建立在具身智能研究者、工程师、教育者与开源社区的工作之上。

本仓库引用的外部论文、代码、数据集、图片及其他资源，其权利归原作者所有。使用时请遵循相应的许可协议与引用要求。
