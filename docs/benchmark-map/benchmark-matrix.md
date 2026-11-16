# Benchmark Matrix

[Overview](README.md) · [简体中文](README_ZH.md) · [Protocol guide](protocol-guide.md) · [Sources](sources.md)

| Benchmark | Primary focus | Environment and embodiment | Task structure | Representative reporting |
| --- | --- | --- | --- | --- |
| LIBERO | Lifelong and multitask knowledge transfer | robosuite/MuJoCo tabletop manipulation with a 7-DoF arm | Spatial, object, goal, 10-task, and 90-task suites | Task success plus transfer/forgetting measures when used as a lifelong-learning benchmark |
| CALVIN | Language-conditioned long-horizon control | PyBullet tabletop environment with a Franka arm | 34 atomic tasks composed into five-instruction chains | Average consecutive instructions completed and success by chain length |
| SimplerEnv | Simulated evaluation of real-world policies | SAPIEN/ManiSkill-based digital twins of common robot setups | Real-evaluation tasks recreated with visual matching or environment variants | Task success together with sim-to-real correlation or policy-ranking agreement |
| RoboTwin 2.0 | Scalable bimanual data generation and robust policy evaluation | SAPIEN-based dual-arm manipulation; multiple supported embodiments | 50 tasks with diverse objects and domain-randomized scenes | Per-task and mean success, with clean and randomized settings identified |
| RoboDojo | Comprehensive generalist-policy evaluation in simulation and reality | Isaac Sim plus standardized real-robot stations across three bimanual embodiments | 42 simulation and 18 real-world tasks; five capability dimensions | Per-task, per-dimension, and aggregate score/success under the official protocol |

## Capability Coverage

| Capability | LIBERO | CALVIN | SimplerEnv | RoboTwin 2.0 | RoboDojo |
| --- | --- | --- | --- | --- | --- |
| Language-conditioned control | Central | Central | Policy/task dependent | Supported | Central in open-instruction tasks |
| Long-horizon composition | Limited by suite/task | Central | Task dependent | Present in selected tasks | Dedicated dimension |
| Continual-learning transfer | Central | Not the primary design | Not the primary design | Not the primary design | Not the primary design |
| Sim-to-real evaluation | Indirect | Indirect | Central | Explicit research target | Direct simulation and real-world tracks |
| Bimanual manipulation | No | No | No in the canonical setups | Central | Central |
| Memory diagnosis | Not isolated | Sequence context matters | Not isolated | Extended by separate RMBench | Dedicated dimension |
| Domain randomization | Limited/configuration dependent | Dataset split and scene variation | Visual matching and variant aggregation | Central | Controlled layouts and capability-specific tests |

## Interpretation Boundaries

- A LIBERO success average does not by itself measure forgetting or forward transfer.
- CALVIN's chain score is not equivalent to independent single-task success because errors terminate progress through the sequence.
- SimplerEnv is meaningful as a real-world proxy only when the simulated and physical protocols are paired carefully.
- RoboTwin 2.0 clean and randomized results should not be merged without labels.
- RoboDojo's overall result should be read with its five capability dimensions; the aggregate can hide a concentrated weakness.
- Percentages from different rows in this matrix are not on a common scale.
