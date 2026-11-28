# VLA Architecture and Interface Matrix

[简体中文](model-matrix_ZH.md)

This matrix separates facts published by project owners from OpenEmbodied's interpretation. “Available” means an official artifact or documented path was found; it does not mean OpenEmbodied has executed it.

## Architecture and Interface

| Field | OpenVLA / OFT | SmolVLA | openpi | GR00T N1.7 |
| --- | --- | --- | --- | --- |
| Main scope | Manipulation VLA | Affordable, efficient VLA | π0, π0-FAST, π0.5 policy family | Cross-embodiment generalist robot skills |
| Approx. size | OpenVLA flagship: 7B | 450M / model card reports ~0.5B | Not summarized as one size in the repo; variant-dependent | Released base checkpoint: 3B |
| Visual/language base | Prismatic VLM; DINOv2 + SigLIP vision, Llama 2 language model for flagship | SmolVLM-family backbone | Gemma-family dependencies; variant-dependent | Cosmos-Reason2-2B / Qwen3-VL-based VLM backbone |
| Action approach | Flagship uses discretized action tokens; OFT documents continuous actions | Continuous actions, flow matching | π0 and π0.5: flow matching; π0-FAST: autoregressive action tokens | Flow-matching action transformer over continuous action chunks |
| Typical inputs | Image + language; exact multi-view/state support depends on recipe | Multi-view images + state + optional language | Robot observations + prompt; schema depends on robot config | Images + language + proprioceptive state, configured by embodiment |
| Typical outputs | Robot action, unnormalized for dataset/robot | Continuous action chunks | Action chunks | Continuous action chunks |

## Openness and Delivery

| Field | OpenVLA / OFT | SmolVLA | openpi | GR00T N1.7 |
| --- | --- | --- | --- | --- |
| Repository code | Available | Available through LeRobot | Available | Available |
| Code license | MIT for OpenVLA repo | Apache-2.0 for LeRobot | Apache-2.0; additional upstream notices exist | Apache-2.0 |
| Base weights | Available | `lerobot/smolvla_base` | π0, π0-FAST, π0.5 base checkpoints | `nvidia/GR00T-N1.7-3B`; backbone access is gated |
| Task weights | Official checkpoints listed for selected datasets/tasks | Community and official fine-tunes available on Hub | DROID, ALOHA, LIBERO and other expert checkpoints listed | LIBERO and other fine-tuned checkpoints documented |
| Weight-license caveat | Flagship derives from Llama 2; model restrictions are not identical to repo MIT license | Base model card: Apache-2.0 | Repo has `LICENSE_GEMMA.txt`; inspect model-specific terms | NVIDIA Open Model License for weights |
| Training data openness | OXE mixture details published; availability and licenses remain dataset-specific | Official claim: compatibly licensed community LeRobot datasets | Base checkpoints described as trained on 10k+ robot-data hours; exact full mixture is not presented as one downloadable dataset | Diverse robot and human-video mixture described; exact complete training mixture is not one fully downloadable artifact |
| Inference code | Available | Available | Available | Available |
| Fine-tuning code | LoRA and full fine-tuning documented | LeRobot training workflow | Available for own LeRobot-format data | Available for own data and modality config |
| Deployment interface | REST serving example | LeRobot robot/policy interfaces | WebSocket remote policy serving | ZMQ policy server; TensorRT/platform deployment guides |

## Documented Compute and Environment

| Field | OpenVLA / OFT | SmolVLA | openpi | GR00T N1.7 |
| --- | --- | --- | --- | --- |
| OS emphasis | Linux/Python stack | LeRobot-supported Python environments | Official repo says Ubuntu 22.04; other OS unsupported | Linux plus documented x86_64, DGX Spark, Jetson Thor/Orin paths |
| Published inference requirement | Recipe-dependent; 7B model and optional quantization/serving paths | Described as consumer-hardware and CPU capable; measure locally before relying on latency | Official estimate: >8 GB GPU memory | Platform-dependent; official TensorRT rates reported for RTX PRO 6000 and Jetson Thor |
| Published fine-tuning requirement | LoRA/full paths documented; verify exact recipe | Official docs say roughly four hours for 20k steps on one A100 for an example setup | Official estimate: >22.5 GB for LoRA, >70 GB for full fine-tuning | Single/multi-GPU commands documented; actual memory depends on embodiment and recipe |
| Environment complexity | Medium–high | Low–medium | Medium–high | High |

## Evaluation Surface

| Field | OpenVLA / OFT | SmolVLA | openpi | GR00T N1.7 |
| --- | --- | --- | --- | --- |
| Simulation references | SimplerEnv and newer recipe-specific evaluations | LIBERO and Meta-World claims; LeRobot supports LIBERO evaluation | LIBERO workflow and checkpoint | LIBERO and SimplerEnv guides |
| Real-robot references | Bridge/WidowX and other manipulation settings | SO100/SO101 | DROID, ALOHA, UR5 examples | SO100 and multiple humanoid/bimanual embodiments |
| Protocol caution | Do not merge vanilla OpenVLA and OFT results | Community data and task-specific fine-tuning matter | Checkpoint-to-robot mismatch is explicitly warned | Embodiment tags and environment prefixes must match |

## Reading the Matrix as a System Diagram

The architecture row describes how each policy turns observations into actions. It does not describe the entire robot stack. An image passes through a vision encoder; language and state information condition the action prediction; the resulting action is decoded, unnormalized, mapped to the robot controller, and executed. A change in any stage can alter measured performance without changing the model weights. This is why input fields, action representation, normalization, and deployment interface appear alongside parameter count.

The openness rows describe separate artifacts. Public inference code permits a checkpoint to run; fine-tuning code permits adaptation; a released dataset allows inspection of the training distribution; and an evaluation script fixes part of the measurement protocol. None of these automatically implies the others. For example, access to a base checkpoint does not guarantee that its full pretraining mixture can be reconstructed. License terms also attach to different artifacts, so the code license is insufficient to characterize the weights.

The compute row should be read as a published configuration rather than a hardware ranking. Memory depends on precision, image resolution, action horizon, batch size, optimizer state, and whether parameters are frozen or adapted with LoRA. A comparable resource study would run the exact checkpoints under one measurement procedure and report throughput and latency as well as peak memory.

## Comparison Boundaries

- **Compact LeRobot workflow:** SmolVLA connects a smaller model to LeRobot data and policy APIs.
- **Original open VLA and OXE lineage:** OpenVLA exposes tokenized actions, 7B-scale VLM adaptation, and the associated weight-license distinction.
- **Action-generation variants in one repository:** openpi includes flow-based and autoregressive policies.
- **Multi-embodiment deployment documentation:** GR00T N1.7 spans data, fine-tuning, evaluation, inference, and platform-specific deployment.

These categories describe documented interfaces and released artifacts; they are not reproduced performance rankings.

