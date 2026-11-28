<p align="center">
  <img src="docs/assets/openembodied-logo.svg" alt="OpenEmbodied" width="820" />
</p>

<p align="center">
  <strong>Models, benchmarks, and research maps for embodied intelligence.</strong>
</p>

![OpenEmbodied research atlas](docs/assets/openembodied-atlas.png)

<p align="center">
  <a href="README_ZH.md">简体中文</a>
  &nbsp;·&nbsp;
  <a href="#-about">About</a>
  &nbsp;·&nbsp;
  <a href="#-research-directions">Research Directions</a>
  &nbsp;·&nbsp;
  <a href="#-planned-research-topics">Planned Research Topics</a>
  &nbsp;·&nbsp;
  <a href="#-contributing">Contributing</a>
</p>

---

## 🌐 About

OpenEmbodied is a curated reference for embodied AI research. It organizes model and benchmark profiles by research direction, with comparative analyses of technical choices, evaluation protocols, and published research. The current collection focuses on robotic manipulation; the broader scope is outlined below.

## 🗂️ Research Directions

Research directions bring together representative methods, evaluation benchmarks, and comparative analyses.

### 🦾 Embodied Manipulation

Robot manipulation through learned policies, world-action modeling, agent-based control, grasp generation, and evaluation.

[Manipulation Paradigms](analysis/manipulation-paradigms/README.md) — how these approaches differ in world modeling, action generation, control frequency, and evaluation.

#### [Vision-Language-Action](models/vla/README.md)

Robot policies that map visual observations and language instructions to actions.

- [OpenVLA / OpenVLA-OFT](models/vla/openvla.md)
- [SmolVLA](models/vla/smolvla.md)
- [openpi: π0 / π0-FAST / π0.5](models/vla/openpi.md)
- [NVIDIA Isaac GR00T N1.7](models/vla/gr00t-n1.7.md)

#### [World Action Models](models/wam/README.md)

Joint modeling of world dynamics and robot actions. The approaches differ in whether future observations are generated during execution.

- [Unified World Models](models/wam/uwm.md) — coupled video and action diffusion.
- [DreamZero](models/wam/dreamzero.md) — video-based world modeling for closed-loop control.
- [Fast-WAM](models/wam/fast-wam.md) — video co-training with direct action generation at inference.
- [OpenWAM](models/wam/openwam.md) — modular world-action pretraining and the OpenWAM-α policy.

#### [Agent-Based Manipulation](systems/agents/README.md)

Closed-loop control systems that combine multimodal reasoning, robot tools, execution feedback, and, in some cases, learned action policies.

- [GPT-6 Astra as an Embodied Policy](systems/agents/gpt-as-policy.md) — direct control and π0.5-assisted control.
- [π0.5 + Astra with Selective Intervention](systems/agents/pi05-call-astra.md) — learned handoff for recovery.
- [GPT-Policy](systems/agents/gpt-policy.md) — in-context robot learning through a constrained tool interface.

##### VLA Model Comparison

Architecture, action representations, released resources, and evaluation protocols across open VLA systems.

- [Research Overview](analysis/vla/README.md) — model families and the availability of code, weights, data, and deployment tools.
- [Technical Comparison](analysis/vla/model-matrix.md) — architectures, action generation, and released resources.
- [Evaluation Comparability](analysis/vla/benchmark-notes.md) — evaluation settings and limits on cross-model comparison.
- [References](analysis/vla/references.md) — official papers, repositories, and documentation.

#### [Grasping](models/grasping/README.md)

Grasp detection for parallel grippers and grasp synthesis for dexterous hands.

- [AnyGrasp](models/grasping/anygrasp.md)
- [UniDexGrasp](models/grasping/unidexgrasp.md)
- [DexGraspNet 2.0](models/grasping/dexgraspnet-2.md)
- [DexGrasp Anything](models/grasping/dexgrasp-anything.md)

#### Manipulation Evaluation

Evaluation suites covering transfer, long-horizon control, sim-to-real evaluation, robustness, and dynamic manipulation. [Benchmark index](benchmarks/README.md).

- [LIBERO](benchmarks/libero.md) — lifelong and multitask manipulation across task suites.
- [CALVIN](benchmarks/calvin.md) — language-conditioned long-horizon manipulation.
- [SimplerEnv](benchmarks/simplerenv.md) — simulation-based evaluation and real-world ranking alignment.
- [RoboTwin 2.0](benchmarks/robotwin-2.md) — scalable bimanual data generation and robustness evaluation.
- [RoboDojo](benchmarks/robodojo.md) — generalist manipulation policy evaluation in simulation and on real robots.
- [RoboDyna](benchmarks/robodyna.md) — dynamic physical reasoning and latency-aware manipulation.

##### Manipulation Benchmark Comparison

Tasks, embodiments, metrics, and protocol differences across manipulation benchmarks.

- [Benchmark Overview](analysis/manipulation-benchmarks/README.md) — the focus and intended use of six manipulation benchmarks.
- [Benchmark Comparison](analysis/manipulation-benchmarks/benchmark-matrix.md) — tasks, robots, environments, observations, and metrics side by side.
- [Evaluation Protocols](analysis/manipulation-benchmarks/protocol-guide.md) — what to check before interpreting or reproducing a reported result.
- [References](analysis/manipulation-benchmarks/references.md) — official papers, repositories, and documentation.

## 🛰️ Planned Research Topics

The next research topics span embodied capabilities and the data, simulation, and robot systems that support them:

| Theme | Technical focus |
| --- | --- |
| **Perception** | 3D scene understanding, visual grounding, affordance prediction, and active perception |
| **Embodied Reasoning** | spatial reasoning, task planning, memory, and decision making |
| **World Models** | general-purpose dynamics prediction, video generation, and model-based planning beyond manipulation policies |
| **Navigation** | visual-language navigation, localization, mapping, and exploration |
| **Data & Simulation** | embodied datasets, synthetic data generation, simulators, and evaluation environments |
| **Robotic Systems** | robot platforms, policy deployment, and sim-to-real transfer |

## 🤝 Contributing

Contributions to model and benchmark profiles, comparative analyses, and primary-source references are welcome.

Please cite the original papers, official repositories, or project documentation, and distinguish reported results from independently verified results. Open an Issue to propose a topic or report a correction.

## 🙏 Acknowledgments

OpenEmbodied is built on the work of researchers, engineers, educators, and open-source communities advancing embodied intelligence.

External papers, code, datasets, images, and other resources remain the property of their respective owners. Follow each source's license and citation requirements.
