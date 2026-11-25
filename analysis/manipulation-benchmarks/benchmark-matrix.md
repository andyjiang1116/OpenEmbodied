# Benchmark Matrix

[简体中文](benchmark-matrix_ZH.md)

[Overview](README.md) · [简体中文](README_ZH.md) · [Evaluation protocols](protocol-guide.md) · [References](references.md)

| Benchmark | Primary focus | Environment and embodiment | Task structure | Representative reporting |
| --- | --- | --- | --- | --- |
| LIBERO | Lifelong and multitask knowledge transfer | robosuite/MuJoCo tabletop manipulation with a 7-DoF arm | Spatial, object, goal, 10-task, and 90-task suites | Task success plus transfer/forgetting measures when used as a lifelong-learning benchmark |
| CALVIN | Language-conditioned long-horizon control | PyBullet tabletop environment with a Franka arm | 34 atomic tasks composed into five-instruction chains | Average consecutive instructions completed and success by chain length |
| SimplerEnv | Simulated evaluation of real-world policies | SAPIEN/ManiSkill-based digital twins of common robot setups | Real-evaluation tasks recreated with visual matching or environment variants | Task success together with sim-to-real correlation or policy-ranking agreement |
| RoboTwin 2.0 | Scalable bimanual data generation and robust policy evaluation | SAPIEN-based dual-arm manipulation; multiple supported embodiments | 50 tasks with diverse objects and domain-randomized scenes | Per-task and mean success, with clean and randomized settings identified |
| RoboDojo | Comprehensive generalist-policy evaluation in simulation and reality | Isaac Sim plus standardized real-robot stations across three bimanual embodiments | 42 simulation and 18 real-world tasks; five capability dimensions | Per-task, per-dimension, and aggregate score/success under the official protocol |
| RoboDyna | Dynamic physical reasoning and latency-aware manipulation | SAPIEN 3 dual-arm simulation with continuously evolving physics | 20 conceptual tasks, 10 household tasks, five capabilities, and four conceptual difficulty conditions | Success and progress score by difficulty, capability, and synchronous/asynchronous protocol |

## Capability Coverage

| Capability | LIBERO | CALVIN | SimplerEnv | RoboTwin 2.0 | RoboDojo | RoboDyna |
| --- | --- | --- | --- | --- | --- | --- |
| Language-conditioned control | Central | Central | Policy/task dependent | Supported | Central in open-instruction tasks | Central |
| Long-horizon composition | Limited by suite/task | Central | Task dependent | Present in selected tasks | Dedicated dimension | Present in selected household tasks |
| Continual-learning transfer | Central | Not the primary design | Not the primary design | Not the primary design | Not the primary design | Not the primary design |
| Sim-to-real evaluation | Indirect | Indirect | Central | Explicit research target | Direct simulation and real-world tracks | Simulation-only benchmark |
| Bimanual manipulation | No | No | No in the canonical setups | Central | Central | Central |
| Memory diagnosis | Not isolated | Sequence context matters | Not isolated | Extended by separate RMBench | Dedicated dimension | State transitions require temporal tracking |
| Domain randomization | Limited/configuration dependent | Dataset split and scene variation | Visual matching and variant aggregation | Central | Controlled layouts and capability-specific tests | Composable task variations |
| Dynamic physics | Not isolated | Limited | Not the primary design | Limited | Not a dedicated dimension | Central |
| Inference latency in protocol | No | No | No | No | No | Paired sync/async evaluation |

## Interpretation Boundaries

- A LIBERO success average does not by itself measure forgetting or forward transfer.
- CALVIN's chain score is not equivalent to independent single-task success because errors terminate progress through the sequence.
- SimplerEnv is meaningful as a real-world proxy only when the simulated and physical protocols are paired carefully.
- RoboTwin 2.0 clean and randomized results should not be merged without labels.
- RoboDojo's overall result should be read with its five capability dimensions; the aggregate can hide a concentrated weakness.
- RoboDyna synchronous and asynchronous results are not interchangeable: only the asynchronous protocol charges the policy for measured inference time.
- Percentages from different rows in this matrix are not on a common scale.
