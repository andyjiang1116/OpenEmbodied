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

Policy learning, grasp generation, and evaluation for robot manipulation tasks.

#### [Vision-Language-Action](models/vla/README.md)

Robot policies that map visual observations and language instructions to actions.

- [OpenVLA / OpenVLA-OFT](models/vla/openvla.md)
- [SmolVLA](models/vla/smolvla.md)
- [π0 / π0-FAST / π0.5](models/vla/openpi.md)
- [NVIDIA Isaac GR00T N1.7](models/vla/gr00t-n1.7.md)

##### VLA Model Comparison

Architecture, action representations, released resources, and evaluation protocols across open VLA systems.

- [Research Overview](maps/vla-landscape/README.md) — model families and the availability of code, weights, data, and deployment tools.
- [Technical Comparison](maps/vla-landscape/model-matrix.md) — architectures, action generation, and released resources.
- [Evaluation Comparability](maps/vla-landscape/benchmark-notes.md) — evaluation settings and limits on cross-model comparison.
- [References](maps/vla-landscape/references.md) — official papers, repositories, and documentation.

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

- [Benchmark Overview](maps/benchmark-map/README.md) — the focus and intended use of six manipulation benchmarks.
- [Benchmark Comparison](maps/benchmark-map/benchmark-matrix.md) — tasks, robots, environments, observations, and metrics side by side.
- [Evaluation Protocols](maps/benchmark-map/protocol-guide.md) — what to check before interpreting or reproducing a reported result.
- [References](maps/benchmark-map/references.md) — official papers, repositories, and documentation.

## 🛰️ Planned Research Topics

The next research topics span embodied capabilities and the data, simulation, and robot systems that support them:

| Theme | Technical focus |
| --- | --- |
| **Perception** | 3D scene understanding, visual grounding, affordance prediction, and active perception |
| **Embodied Reasoning** | spatial reasoning, task planning, memory, and decision making |
| **World Models** | dynamics prediction, video and action generation, and model-based planning |
| **Navigation** | visual-language navigation, localization, mapping, and exploration |
| **Data & Simulation** | embodied datasets, synthetic data generation, simulators, and evaluation environments |
| **Robotic Systems** | robot platforms, policy deployment, and sim-to-real transfer |

## 🤝 Contributing

Contributions to model and benchmark profiles, comparative analyses, and primary-source references are welcome.

Please cite the original papers, official repositories, or project documentation, and distinguish reported results from independently verified results. Open an Issue to propose a topic or report a correction.

## 🙏 Acknowledgments

OpenEmbodied is built on the work of researchers, engineers, educators, and open-source communities advancing embodied intelligence.

External papers, code, datasets, images, and other resources remain the property of their respective owners. Follow each source's license and citation requirements.
