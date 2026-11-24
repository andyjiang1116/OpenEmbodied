# Models

> Technical profiles organized by the capability a model contributes to an embodied system.

[简体中文](README_ZH.md)

## Model Families

### 🧠 [Vision-Language-Action Models](vla/README.md)

Generalist policies that connect visual observations and language instructions to robot actions. This collection currently covers OpenVLA, SmolVLA, π0 / π0-FAST / π0.5, and NVIDIA Isaac GR00T N1.7.

### ✋ [Grasping Models](grasping/README.md)

Methods for parallel-gripper grasp perception and dexterous-hand pose generation or execution. The collection connects AnyGrasp, UniDexGrasp, DexGraspNet 2.0, and DexGrasp Anything through a shared grasping taxonomy.

## Organization

Model profiles live under capability-oriented directories rather than framework or institution names. New families can be added without flattening unrelated methods into one list—for example `world-models/`, `navigation/`, or `humanoid-control/` when those collections become substantial.

Each profile separates the research contribution from the released implementation, data, checkpoints, runtime dependencies, license, and deployment boundary.
