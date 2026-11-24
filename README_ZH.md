<p align="center">
  <img src="docs/assets/openembodied-logo.svg" alt="OpenEmbodied" width="820" />
</p>

<p align="center">
  <strong>从感知与推理出发，连接机器人行动、评测体系与真实世界部署。</strong>
</p>

<p align="center">
  👁️ 感知 &nbsp;·&nbsp; 🧠 推理 &nbsp;·&nbsp; 🌐 世界模型<br/>
  🧭 导航 &nbsp;·&nbsp; 🦾 操作 &nbsp;·&nbsp; 🤖 部署
</p>

![OpenEmbodied research atlas](docs/assets/openembodied-atlas.png)

<p align="center">
  <a href="README.md">English</a>
  &nbsp;·&nbsp;
  <a href="#-关于项目">关于项目</a>
  &nbsp;·&nbsp;
  <a href="#-技术目录">技术目录</a>
  &nbsp;·&nbsp;
  <a href="#-研究地图">研究地图</a>
  &nbsp;·&nbsp;
  <a href="#-参与贡献">参与贡献</a>
</p>

---

## 🌐 关于项目

OpenEmbodied 是一个面向 Embodied AI 的结构化研究图谱，覆盖从 perception、reasoning、world models 到 navigation、manipulation 与 real-world deployment 的完整技术链路。仓库不以堆积链接为目标，而是基于原始资料梳理 methods、evaluation systems 与 embodied platforms 之间的关系。

- **探索技术方法：** 通过结构化档案理解 model family、核心思路、开放资源与实际应用场景。
- **理解评测体系：** 通过 Benchmark 页面厘清 task、embodiment、protocol、metric 与结果的比较边界。
- **把握研究全景：** 通过 Research Maps 连接 models、benchmarks、datasets、simulators、robots 与 deployment stacks。

## 🗂️ 技术目录

### 🧠 Models & Policies｜模型与策略

#### [Vision-Language-Action Models](models/vla/README_ZH.md)

将视觉观测和语言指令连接到机器人动作的 generalist policy。

- [OpenVLA / OpenVLA-OFT](models/vla/openvla_ZH.md)
- [SmolVLA](models/vla/smolvla_ZH.md)
- [π0 / π0-FAST / π0.5](models/vla/openpi_ZH.md)
- [NVIDIA Isaac GR00T N1.7](models/vla/gr00t-n1.7_ZH.md)

#### [Grasping Models](models/grasping/README_ZH.md)

覆盖 parallel-gripper perception、dexterous grasp generation 与 grasp execution 的方法。

- [AnyGrasp](models/grasping/anygrasp_ZH.md)
- [UniDexGrasp](models/grasping/unidexgrasp_ZH.md)
- [DexGraspNet 2.0](models/grasping/dexgraspnet-2_ZH.md)
- [DexGrasp Anything](models/grasping/dexgrasp-anything_ZH.md)

### 📏 [Evaluation Benchmarks｜评测基准](benchmarks/README_ZH.md)

- [LIBERO](benchmarks/libero_ZH.md) — lifelong 与 multitask robot learning 中的 knowledge transfer。
- [CALVIN](benchmarks/calvin_ZH.md) — language-conditioned long-horizon manipulation。
- [SimplerEnv](benchmarks/simplerenv_ZH.md) — simulation-to-real evaluation fidelity。
- [RoboTwin 2.0](benchmarks/robotwin-2_ZH.md) — scalable bimanual data generation 与 robustness evaluation。
- [RoboDojo](benchmarks/robodojo_ZH.md) — simulation 与 real robot 上的 generalist-policy evaluation。
- [RoboDyna](benchmarks/robodyna_ZH.md) — dynamic physical reasoning 与 latency-aware manipulation。

## 🧭 研究地图

### 🔭 Open VLA Landscape

从 architecture、action generation、adaptation、compute、evaluation 与 deployment surface 对比开放 VLA 路线。

- [Landscape Overview](docs/vla-landscape/README_ZH.md)
- [Model Matrix](docs/vla-landscape/model-matrix_ZH.md)
- [Benchmark Notes](docs/vla-landscape/benchmark-notes_ZH.md)
- [Primary Sources](docs/vla-landscape/sources.md)

### 🦾 Manipulation Benchmark Map

理解不同 manipulation benchmark 测量什么，以及哪些结果可以合理比较。

- [Benchmark Map Overview](docs/benchmark-map/README_ZH.md)
- [Benchmark Matrix](docs/benchmark-map/benchmark-matrix_ZH.md)
- [Protocol Guide](docs/benchmark-map/protocol-guide_ZH.md)
- [Primary Sources](docs/benchmark-map/sources.md)

## 🛰️ 持续扩展的 Atlas

| 研究方向 | 计划覆盖范围 |
| --- | --- |
| **Perception｜感知** | 3D vision、grounding、mapping、affordance 与 active perception |
| **Embodied Reasoning｜具身推理** | spatial/temporal reasoning、planning、memory 与 decision making |
| **World Models｜世界模型** | environment prediction、video-action generation、simulation 与 policy improvement |
| **Navigation｜导航** | visual-language navigation、exploration、localization 与 mobile interaction |
| **Datasets & Simulators** | embodied data、synthetic generation、physics engines 与 evaluation environments |
| **Robots & Deployment** | embodiments、interfaces、policy serving、sim-to-real 与 real-world systems |

## 🤝 参与贡献

OpenEmbodied 欢迎内容纠错、新增技术档案、完善 Research Landscape、Benchmark 分析和实际实现经验。

高质量贡献应当基于事实和原始来源，具有清晰的技术范围，并说明实际发布了什么、测量了什么，以及哪些部分仍不确定。可以通过 Issue 推荐新方向、资源或提交纠错。

## 🙏 致谢

OpenEmbodied 建立在具身智能研究者、工程师、教育者与开源社区的工作之上。

本仓库引用的外部论文、代码、Dataset、图片及其他资源，其权利归原作者所有。使用时请遵循各来源的 License 与引用要求。
