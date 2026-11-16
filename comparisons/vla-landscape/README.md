# Open VLA Landscape 2026

> What is actually open, comparable, and reproducible?

[简体中文](README_ZH.md) · [Model matrix](model-matrix.md) · [Benchmark notes](benchmark-notes.md) · [Sources](sources.md)

**Status:** Research release v0.1 · **Evidence level:** L0 — Reviewed · **Last verified:** 2026-11-16

## Executive Summary

“Open VLA” can mean very different things. A project may publish inference code but not training data, release weights under a separate license, provide a base checkpoint that still needs task-specific fine-tuning, or report results under a protocol that is not directly comparable with another project.

This first OpenEmbodied landscape compares four representative open VLA stacks:

- [OpenVLA / OpenVLA-OFT](../../profiles/openvla.md): the influential 7B open-source VLA line built on a pretrained VLM and Open X-Embodiment data.
- [SmolVLA](../../profiles/smolvla.md): a compact 450M flow-matching policy integrated with the LeRobot ecosystem.
- [π0 / π0-FAST / π0.5 via openpi](../../profiles/openpi.md): Physical Intelligence's flow-based and autoregressive policy family with released base and task checkpoints.
- [Isaac GR00T N1.7](../../profiles/gr00t-n1.7.md): NVIDIA's cross-embodiment VLA stack with documented fine-tuning, evaluation, and deployment paths.

The main conclusion is simple: **there is no single “most open” or “best” VLA independent of the intended robot, task, compute budget, license constraints, and evaluation protocol.**

## Quick Comparison

| Project | Primary strength | Action generation | Published starting point | Practical entry barrier |
| --- | --- | --- | --- | --- |
| OpenVLA | Established research baseline and broad OXE pretraining | Discrete action tokens; OFT adds continuous actions | 7B checkpoints, inference, LoRA/full fine-tuning, evaluation code | Medium–high |
| SmolVLA | Small model and integrated low-cost robotics workflow | Continuous actions with flow matching | 450M base model, LeRobot training/inference tools | Low–medium |
| openpi | Multiple π-family policies and released base/task checkpoints | Flow matching for π0/π0.5; autoregressive tokens for π0-FAST | Base and expert checkpoints, training, serving, LIBERO examples | Medium–high |
| GR00T N1.7 | Cross-embodiment engineering and deployment stack | Continuous actions with a diffusion-transformer head | Base/fine-tuned checkpoints, benchmark guides, policy server | High |

See [model-matrix.md](model-matrix.md) for the detailed comparison and source-level caveats.

## What “Open” Means Here

OpenEmbodied records openness across separate dimensions instead of using one binary label:

1. **Code** — inference, fine-tuning, pretraining, evaluation, and deployment code are tracked separately.
2. **Weights** — base and task-specific checkpoints may have different availability or terms.
3. **Data** — published dataset names do not imply that the exact training mixture is downloadable.
4. **License** — repository code and model weights may use different licenses or inherit upstream restrictions.
5. **Evaluation** — a benchmark name alone does not prove that task suites, seeds, horizons, image inputs, or success aggregation match.
6. **Deployment** — a runnable policy server is different from a validated end-to-end robot integration.

## Findings

### 1. SmolVLA is the clearest low-cost starting point

SmolVLA publishes a 450M Apache-2.0 base model, uses continuous actions and flow matching, and is integrated into LeRobot's dataset, training, evaluation, and hardware workflows. The official documentation includes a direct model-loading path and positions the model for task-specific fine-tuning. This makes it the strongest candidate for OpenEmbodied's first L1/L2 reproduction attempt.

### 2. OpenVLA remains a useful reference baseline, but “MIT” needs context

The OpenVLA repository is MIT-licensed and provides inference, fine-tuning, serving, and evaluation material. Its published 7B checkpoints derive from Llama 2, so the model terms are not described by the repository's MIT license alone. OpenVLA-OFT also changes important implementation choices, including continuous action prediction, so results should identify the exact recipe rather than use “OpenVLA” as a single undifferentiated label.

### 3. openpi exposes unusually useful system boundaries

The official repository distinguishes π0, π0-FAST, and π0.5; releases base checkpoints and several robot/task-specific checkpoints; documents GPU-memory expectations; and provides remote policy serving. It also explicitly warns that adaptation to a different robot may fail. That warning is valuable evidence rather than a weakness: embodiment transfer is not guaranteed by checkpoint availability.

### 4. GR00T N1.7 has the broadest documented deployment surface in this set

GR00T N1.7 documents data conversion, inference, fine-tuning, policy serving, TensorRT deployment, and benchmark-specific workflows for LIBERO, SimplerEnv, and SO100. Its code is Apache-2.0, while weights use the NVIDIA Open Model License. The stack is comprehensive, but the environment, gated backbone access, submodules, GPU dependencies, and platform-specific paths raise the entry cost.

### 5. Benchmark results must not be collapsed into one leaderboard

LIBERO results can differ through task suite, observation history, image views, action representation, fine-tuning recipe, rollout horizon, seed count, and aggregation. Real-robot SO100/SO101 results introduce another set of hardware and data-collection variables. This landscape therefore records results with their protocol rather than ranking isolated headline numbers. See [benchmark-notes.md](benchmark-notes.md).

## Recommendations by Goal

- **First VLA experiment or modest hardware:** start with SmolVLA and LeRobot.
- **Study the canonical open VLA architecture and OXE lineage:** start with OpenVLA, then compare the OFT recipe.
- **Study flow matching, FAST tokenization, or DROID/ALOHA adaptation:** use openpi.
- **Build around a documented cross-embodiment deployment stack:** evaluate GR00T N1.7.
- **Compare paper results:** first normalize the benchmark protocol; do not compare model names alone.

## Evidence Status

| Project | Level | What OpenEmbodied verified | Not yet verified |
| --- | --- | --- | --- |
| OpenVLA | L0 | Official repository, project page, checkpoints, license notes, documented workflows | Local installation, inference, benchmark results |
| SmolVLA | L0 | Official LeRobot docs, model card, license, model inputs/outputs, workflow | Local installation, inference, fine-tuning |
| openpi | L0 | Official repository, model family, checkpoints, requirements, license, serving docs | Local installation, checkpoint inference, LIBERO run |
| GR00T N1.7 | L0 | Official repository, model/weight licenses, workflows, supported benchmark guides | Gated-model access, local installation, inference, deployment |

## Watchlist

- **GR00T 2** was announced in November 2026 as a world-action model that predicts video and actions. The official research page states that code is scheduled for December, so it is not included in the current reproducibility matrix.
- This page will add new models only after primary-source review and a clear reason for comparison; popularity alone is not sufficient.

## Next Verification Steps

1. Install the current LeRobot release in a clean environment.
2. Load `lerobot/smolvla_base` and run one documented batch inference.
3. Record the exact OS, Python, package lock, device, memory use, latency, and output shape.
4. Promote the SmolVLA profile to L1 or L2 only after preserving the evidence.
5. Select one shared simulation protocol before attempting cross-model comparisons.

## Scope and Limitations

This is a source review, not an independent performance evaluation. Claims about model quality remain attributed to their official sources until OpenEmbodied reproduces them. Repository interfaces, checkpoints, and licenses can change; use the verification date and follow the linked primary sources before making deployment or licensing decisions.

