---
title: SmolVLA
area: vision-language-action
official_repo: https://github.com/huggingface/lerobot
---

# SmolVLA

## Snapshot

- **Role in the landscape:** compact VLA designed for affordable experimentation and LeRobot workflows.
- **Size:** 450M in official materials; the Hub model card displays approximately 0.5B parameters.
- **Inputs:** multiple camera images, robot state, and optional language instruction.
- **Output:** continuous action chunks.
- **Training objective:** flow matching.

## Why It Matters

SmolVLA connects a relatively small policy to a maintained data, training, evaluation, and robot-control ecosystem. Its official model card provides a direct load-and-infer example, and the project is explicitly designed for task-specific fine-tuning and lower-cost hardware.

## Architecture and Data

Official materials describe a compact VLM-based architecture with a flow-matching action expert, reduced visual tokens, and attention choices designed for efficient inference. The model was pretrained on compatible, community-shared LeRobot datasets; the official article describes fewer than 30k training episodes.

## What Is Available

- Apache-2.0 LeRobot code and Apache-2.0 base model card.
- `lerobot/smolvla_base` checkpoint.
- documented installation, model loading, training, and real-robot evaluation paths.
- integration with LeRobot datasets and supported robot interfaces.
- official examples involving LIBERO, Meta-World, SO100, and SO101 contexts.

## Evidence and Caveats

- The base model is intended to be fine-tuned for a target use case; loading the checkpoint is not equivalent to having a successful robot policy.
- Official guidance suggests collecting repeated demonstrations across task variations and notes that insufficient data can produce poor results.
- “Runs on consumer hardware” is a project claim that still needs device-specific latency and memory measurement.

## Primary Sources

- [LeRobot repository](https://github.com/huggingface/lerobot)
- [Official SmolVLA documentation](https://github.com/huggingface/lerobot/blob/main/docs/source/smolvla.mdx)
- [Base model card](https://huggingface.co/lerobot/smolvla_base)
- [Official article](https://huggingface.co/blog/smolvla)
- [Paper](https://arxiv.org/abs/2506.01844)

