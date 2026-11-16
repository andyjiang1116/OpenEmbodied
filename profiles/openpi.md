---
title: openpi model family
area: vision-language-action
official_repo: https://github.com/Physical-Intelligence/openpi
---

# π0 / π0-FAST / π0.5 via openpi

## Snapshot

- **Role in the landscape:** an official implementation and release surface for Physical Intelligence robot-policy models.
- **Variants:** π0, π0-FAST, and π0.5.
- **Action generation:** flow matching for π0 and the currently supported π0.5 head; autoregressive action tokens for π0-FAST.

## Why It Matters

openpi makes architectural alternatives visible within one model family and publishes both base checkpoints and several task/robot-specific expert checkpoints. It also exposes data conversion, normalization, training, policy serving, and robot/simulation examples, which makes system boundaries easier to inspect.

## What Is Available

- Apache-2.0 repository code, with additional upstream license notices including Gemma-related terms.
- π0, π0-FAST, and π0.5 base checkpoints described as pretrained on more than 10k hours of robot data.
- expert checkpoints for DROID, ALOHA, and LIBERO use cases.
- JAX-centered training plus published PyTorch support.
- LeRobot-format data conversion, fine-tuning, local inference, and WebSocket remote serving.
- Docker and `uv` installation paths.

## Published Requirements

The official repository estimates, for a single GPU:

- inference: more than 8 GB GPU memory;
- LoRA fine-tuning: more than 22.5 GB;
- full fine-tuning: more than 70 GB;
- tested OS: Ubuntu 22.04, with other operating systems currently unsupported.

These are project estimates and have not been reproduced by OpenEmbodied.

## Caveats

- The official repository explicitly warns that a checkpoint developed for its robots may not adapt successfully to another platform.
- Expert checkpoints may generalize differently from base checkpoints; robot interface and normalization must match.
- Repository license and model dependency terms should be reviewed separately.
- Reported LIBERO performance should be compared only after aligning the exact checkpoint and protocol.

## Primary Sources

- [Official repository](https://github.com/Physical-Intelligence/openpi)
- [π0 project page](https://www.physicalintelligence.company/blog/pi0)
- [π0.5 project page](https://www.physicalintelligence.company/blog/pi05)
- [π0 paper](https://arxiv.org/abs/2410.24164)

