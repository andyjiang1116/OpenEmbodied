---
title: OpenVLA and OpenVLA-OFT
area: vision-language-action
evidence_level: L0
last_verified: 2026-11-16
official_repo: https://github.com/openvla/openvla
---

# OpenVLA / OpenVLA-OFT

## Snapshot

- **Role in the landscape:** influential open VLA baseline and Open X-Embodiment lineage.
- **Flagship size:** 7B parameters.
- **Inputs/outputs:** image and language to robot action; exact state, view, and action interfaces depend on checkpoint and recipe.
- **Action representation:** flagship OpenVLA discretizes actions as tokens; OFT documents a continuous-action fine-tuning recipe.
- **Evidence:** L0 — official sources reviewed, not locally executed.

## Why It Matters

OpenVLA made a generalist 7B VLA, checkpoints, inference, fine-tuning, evaluation, and serving material publicly accessible. It remains a useful reference point for studying how pretrained VLMs are adapted to robot control and how Open X-Embodiment data is mixed for generalist manipulation policies.

## Architecture and Data

The flagship model fine-tunes a Prismatic-7B VLM combining DINOv2 and SigLIP visual features with a Llama 2 language backbone. The official project reports pretraining on roughly 970k robot episodes from the Open X-Embodiment collection. Actions are decoded for the target dataset/robot using the appropriate normalization statistics.

## What Is Available

- MIT-licensed repository code.
- `openvla-7b` and an earlier `openvla-v01-7b` checkpoint.
- lightweight Hugging Face-style inference interface;
- LoRA, quantized LoRA, full fine-tuning, training, evaluation, and REST-serving paths;
- OpenVLA-OFT as a newer optimized recipe with continuous actions and faster control-oriented inference.

## Openness Caveats

- Repository code and model weights do not have identical licensing context: the flagship weights derive from Llama 2 and inherit relevant restrictions.
- Open X-Embodiment is a collection of datasets with dataset-specific availability and terms; a published mixture does not make every source uniformly redistributable.
- “OpenVLA result” is ambiguous unless the checkpoint and recipe—vanilla, FAST-related work, or OFT—are named.

## Reproduction Plan

1. Pin the exact OpenVLA/OFT repository revision.
2. Select inference-only or fine-tuning scope and record model terms.
3. Run one official inference example with its expected normalization key.
4. Record GPU memory, latency, inputs, and action output shape.
5. Attempt a benchmark only after fixing the evaluation protocol.

## Primary Sources

- [Official repository](https://github.com/openvla/openvla)
- [Project page](https://openvla.github.io/)
- [Paper](https://arxiv.org/abs/2406.09246)
- [OpenVLA-OFT](https://openvla-oft.github.io/)

