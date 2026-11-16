---
title: NVIDIA Isaac GR00T N1.7
area: vision-language-action
official_repo: https://github.com/NVIDIA/Isaac-GR00T
---

# NVIDIA Isaac GR00T N1.7

## Snapshot

- **Role in the landscape:** cross-embodiment VLA and deployment stack for manipulation and humanoid skills.
- **Released checkpoint:** `nvidia/GR00T-N1.7-3B`.
- **Backbone:** Cosmos-Reason2-2B / Qwen3-VL-based vision-language model.
- **Action generation:** diffusion-transformer head that denoises continuous actions.

## Why It Matters

GR00T N1.7 covers a broad engineering surface: LeRobot-format data, embodiment configurations, fine-tuning, PyTorch inference, server-client deployment, TensorRT paths, simulation benchmarks, and humanoid whole-body workflows.

## What Is Available

- Apache-2.0 repository code.
- weights under the NVIDIA Open Model License.
- base and selected fine-tuned checkpoints.
- single- and multi-GPU fine-tuning commands.
- benchmark guides for LIBERO, SimplerEnv Fractal/Bridge, and SO100.
- ZMQ policy server and documented TensorRT/platform paths.
- workflows for x86_64 dGPU, DGX Spark, Jetson AGX Thor, and Jetson Orin.

## Openness and Environment Caveats

- The model's VLM backbone is gated on Hugging Face and requires access/authentication.
- The repository uses submodules and Git LFS for some assets.
- GPU packages, FlashAttention, TorchCodec, FFmpeg versions, CUDA generations, and platform activation scripts create meaningful environment complexity.
- The official repository reports TensorRT rates on specific NVIDIA hardware; those numbers should not be generalized to other devices.
- Weight terms differ from the Apache-2.0 code license.

## Benchmark Surface

The repository provides benchmark-specific workflows rather than one universal command. Embodiment tags, environment prefixes, action spaces, checkpoint variants, and runtime backends must be recorded for a comparable result.

## Primary Sources

- [Official repository](https://github.com/NVIDIA/Isaac-GR00T)
- [GR00T N1 publication](https://research.nvidia.com/publication/2025-03_nvidia-isaac-gr00t-n1-open-foundation-model-humanoid-robots)
- [GR00T N1 paper](https://arxiv.org/abs/2503.14734)

