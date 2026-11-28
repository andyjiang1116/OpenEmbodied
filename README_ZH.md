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

### 🦾 [Embodied Manipulation｜具身操作](manipulation/README_ZH.md)

涵盖机器人操作中的策略学习、世界动作建模、Agent 控制、抓取生成与性能评测。

#### [Vision-Language-Action](manipulation/models/vla/README_ZH.md)

将视觉观测与语言指令映射为机器人动作的策略模型。

- [OpenVLA / OpenVLA-OFT](manipulation/models/vla/openvla_ZH.md)
- [SmolVLA](manipulation/models/vla/smolvla_ZH.md)
- [openpi：π0 / π0-FAST / π0.5](manipulation/models/vla/openpi_ZH.md)
- [NVIDIA Isaac GR00T N1.7](manipulation/models/vla/gr00t-n1.7_ZH.md)

#### [世界动作模型（WAM）](manipulation/models/wam/README_ZH.md)

联合建模环境变化与机器人动作；不同方法在执行时是否显式生成未来观测方面存在区别。

- [Unified World Models](manipulation/models/wam/uwm_ZH.md) — 耦合视频与动作扩散建模。
- [DreamZero](manipulation/models/wam/dreamzero_ZH.md) — 基于视频世界模型的闭环控制。
- [Fast-WAM](manipulation/models/wam/fast-wam_ZH.md) — 使用视频联合训练，并在推理时直接生成动作。
- [OpenWAM](manipulation/models/wam/openwam_ZH.md) — 模块化世界动作预训练框架与 OpenWAM-α 策略。

#### [Agent 式具身操作](manipulation/agents/README_ZH.md)

结合多模态推理、机器人工具、执行反馈，以及可选的学习型动作策略，构成闭环控制系统。

- [GPT-6 Astra as an Embodied Policy](manipulation/agents/gpt-as-policy_ZH.md) — 直接控制与 π0.5 辅助控制。
- [π0.5 + Astra 按需介入](manipulation/agents/pi05-call-astra_ZH.md) — 针对恢复场景学习控制权切换。
- [GPT-Policy](manipulation/agents/gpt-policy_ZH.md) — 通过受约束工具接口进行上下文机器人学习。

#### [Grasping](manipulation/models/grasping/README_ZH.md)

涵盖平行夹爪的抓取检测与灵巧手的抓取姿态生成。

- [AnyGrasp](manipulation/models/grasping/anygrasp_ZH.md)
- [UniDexGrasp](manipulation/models/grasping/unidexgrasp_ZH.md)
- [DexGraspNet 2.0](manipulation/models/grasping/dexgraspnet-2_ZH.md)
- [DexGrasp Anything](manipulation/models/grasping/dexgrasp-anything_ZH.md)

---

#### [Manipulation Evaluation｜操作评测](manipulation/benchmarks/README_ZH.md)

覆盖知识迁移、长程控制、仿真与真实场景的一致性、鲁棒性及动态操作等评测主题。

- [LIBERO](manipulation/benchmarks/libero_ZH.md) — 跨任务套件的终身学习与多任务操作。
- [CALVIN](manipulation/benchmarks/calvin_ZH.md) — 语言条件下的长程操作任务。
- [SimplerEnv](manipulation/benchmarks/simplerenv_ZH.md) — 仿真评测与真实场景中策略排序的一致性。
- [RoboTwin 2.0](manipulation/benchmarks/robotwin-2_ZH.md) — 双臂操作数据生成与鲁棒性评测。
- [RoboDojo](manipulation/benchmarks/robodojo_ZH.md) — 仿真与真机环境中的通用操作策略评测。
- [RoboDyna](manipulation/benchmarks/robodyna_ZH.md) — 动态场景中的物理推理与时效性操作。

---

## 🛰️ 规划中的研究主题

后续研究主题覆盖具身能力，以及支撑这些能力的数据、仿真和机器人系统：

| 主题 | 技术重点 |
| --- | --- |
| **Perception｜感知** | 三维场景理解、视觉语义定位、可供性预测与主动感知 |
| **Embodied Reasoning｜具身推理** | 空间推理、任务规划、记忆与决策 |
| **World Models｜世界模型** | 面向操作策略之外的通用动力学预测、视频生成与基于模型的规划 |
| **Navigation｜导航** | 视觉语言导航、定位、建图与探索 |
| **Data & Simulation｜数据与仿真** | 具身数据集、合成数据生成、仿真平台与评测环境 |
| **Robotic Systems｜机器人系统** | 机器人平台、策略部署与 sim-to-real 迁移 |

## 🤝 参与贡献

欢迎补充模型与评测基准档案、横向分析及参考文献，并修正文档中的错误。

请优先引用论文、官方仓库或项目文档，并区分原作者报告的结果与独立验证结果。可通过 Issue 提议研究主题或提交勘误。

## 🙏 致谢

OpenEmbodied 建立在具身智能研究者、工程师、教育者与开源社区的工作之上。

本仓库引用的外部论文、代码、数据集、图片及其他资源，其权利归原作者所有。使用时请遵循相应的许可协议与引用要求。
