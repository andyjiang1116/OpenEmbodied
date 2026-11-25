# Models

> Technical profiles organized by the capability a model contributes to an embodied system.

[简体中文](README_ZH.md)

## Model Families

### 🧠 [Vision-Language-Action Models](vla/README.md)

Generalist policies that connect visual observations and language instructions to robot actions. This collection currently covers OpenVLA, SmolVLA, π0 / π0-FAST / π0.5, and NVIDIA Isaac GR00T N1.7.

### 🌐 [World Action Models](wam/README.md)

Methods that learn robot actions alongside world evolution. Unified World Models, DreamZero, and Fast-WAM illustrate coupled video-action learning and different inference-time designs.

### ✋ [Grasping Models](grasping/README.md)

Methods for parallel-gripper grasp perception and dexterous-hand pose generation or execution. The collection connects AnyGrasp, UniDexGrasp, DexGraspNet 2.0, and DexGrasp Anything through a shared grasping taxonomy.

Each profile describes the research objective, model inputs and outputs, method design, available artifacts, evaluation setting, and integration constraints. Reported performance is attributed to the corresponding publication or project documentation.

Agent-based control systems are indexed separately under [Agent-Based Manipulation](../systems/agents/README.md), because they combine models with tools, control interfaces, and feedback loops.
