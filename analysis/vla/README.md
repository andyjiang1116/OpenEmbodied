# VLA Model Comparison

> Architecture, action representations, released resources, and evaluation protocols.

[简体中文](README_ZH.md) · [Technical comparison](model-matrix.md) · [Evaluation comparability](benchmark-notes.md) · [References](references.md)

## Overview

“Open VLA” can mean very different things. A project may publish inference code but not training data, release weights under a separate license, provide a base checkpoint that still needs task-specific fine-tuning, or report results under a protocol that is not directly comparable with another project.

This comparison covers four VLA model families with publicly documented implementations or checkpoints:

- [OpenVLA / OpenVLA-OFT](../../models/vla/openvla.md): the influential 7B open-source VLA line built on a pretrained VLM and Open X-Embodiment data.
- [SmolVLA](../../models/vla/smolvla.md): a compact 450M flow-matching policy integrated with the LeRobot ecosystem.
- [π0 / π0-FAST / π0.5 via openpi](../../models/vla/openpi.md): Physical Intelligence's flow-based and autoregressive policy family with released base and task checkpoints.
- [Isaac GR00T N1.7](../../models/vla/gr00t-n1.7.md): NVIDIA's cross-embodiment VLA stack with documented fine-tuning, evaluation, and deployment paths.

These models differ in action representation, adaptation path, released artifacts, and supported robot interfaces. Performance claims must be read alongside the task, embodiment, training data, and evaluation protocol.

## Quick Comparison

| Model family | Action generation | Released resources | Integration considerations |
| --- | --- | --- | --- |
| OpenVLA | Discrete action tokens; OFT uses a continuous-action head | 7B checkpoints, inference, fine-tuning, and evaluation code | Robot-specific action normalization; original and OFT recipes differ |
| SmolVLA | Continuous action chunks generated with flow matching | 450M base model and LeRobot training/inference tools | Task-specific demonstrations and adaptation are generally required |
| openpi | Flow matching for π0/π0.5; autoregressive tokens for π0-FAST | Base and task checkpoints, training and serving examples | Robot-specific data schema and action interface |
| GR00T N1.7 | Continuous action chunks from a flow-matching action transformer | Checkpoints, fine-tuning workflows, benchmark guides, policy server | Platform-specific dependencies and embodiment configuration |

See the [technical comparison](model-matrix.md) for detailed fields and comparison boundaries.

## What “Open” Means Here

OpenEmbodied records openness across separate dimensions instead of using one binary label:

1. **Code** — inference, fine-tuning, pretraining, evaluation, and deployment code are tracked separately.
2. **Weights** — base and task-specific checkpoints may have different availability or terms.
3. **Data** — published dataset names do not imply that the exact training mixture is downloadable.
4. **License** — repository code and model weights may use different licenses or inherit upstream restrictions.
5. **Evaluation** — a benchmark name alone does not prove that task suites, seeds, horizons, image inputs, or success aggregation match.
6. **Deployment** — a runnable policy server is different from a validated end-to-end robot integration.

## Technical Observations

### SmolVLA: compact model and integrated tooling

SmolVLA publishes a 450M Apache-2.0 base model, uses continuous actions and flow matching, and is integrated into LeRobot's dataset, training, evaluation, and hardware workflows. The official documentation describes model loading and task-specific fine-tuning. The smaller model size reduces compute requirements, while task performance still depends on the data and robot configuration.

### OpenVLA: distinguish code, weights, and adaptation recipe

The OpenVLA repository is MIT-licensed and provides inference, fine-tuning, serving, and evaluation material. Its published 7B checkpoints derive from Llama 2, so the model terms are not described by the repository's MIT license alone. OpenVLA-OFT also changes important implementation choices, including continuous action prediction, so results should identify the exact recipe rather than use “OpenVLA” as a single undifferentiated label.

### openpi: multiple policy formulations and robot interfaces

The official repository distinguishes π0, π0-FAST, and π0.5; releases base checkpoints and several robot/task-specific checkpoints; documents GPU-memory expectations; and provides remote policy serving. It also notes that adaptation to a different robot may fail. Checkpoint availability does not establish transfer to an unsupported embodiment.

### GR00T N1.7: documented training and deployment workflows

GR00T N1.7 documents data conversion, inference, fine-tuning, policy serving, TensorRT deployment, and benchmark-specific workflows for LIBERO, SimplerEnv, and SO100. Its code is Apache-2.0, while weights use the NVIDIA Open Model License. Reproduction depends on model access, submodules, GPU packages, and platform-specific installation paths.

### Evaluation: preserve the experimental protocol

LIBERO results can differ through task suite, observation history, image views, action representation, fine-tuning recipe, rollout horizon, seed count, and aggregation. Real-robot SO100/SO101 results introduce another set of hardware and data-collection variables. Results must therefore be interpreted together with their protocols. See [evaluation comparability](benchmark-notes.md).

## Selecting a Relevant Reference

- **Compact model and LeRobot integration:** SmolVLA.
- **Discrete action tokens and Open X-Embodiment pretraining:** OpenVLA; OFT represents a separate continuous-action adaptation recipe.
- **Flow matching, FAST tokenization, and published task checkpoints:** openpi.
- **Cross-embodiment fine-tuning and policy serving:** GR00T N1.7.
- **Reported benchmark performance:** task suites, observations, training data, and rollout protocols determine whether results are comparable.

