# Benchmark Comparability Notes

[简体中文](benchmark-notes_ZH.md)

## Why This Page Exists

A model name and a benchmark score are not enough to support a fair comparison. VLA evaluation is highly sensitive to the policy checkpoint, task suite, observation pipeline, action representation, fine-tuning data, rollout settings, and success aggregation.

## LIBERO Checklist

Before placing two results in the same row, record:

- suite: Spatial, Object, Goal, Long, or aggregate;
- exact task count and task version;
- pretrained/base checkpoint and fine-tuning recipe;
- image views, resolution, observation history, and state inputs;
- action representation, action-chunk length, and execution horizon;
- demonstrations per task and any additional data;
- number of seeds, episodes per task, and checkpoint selection rule;
- success definition and whether the number is mean, final checkpoint, or best checkpoint;
- simulator and dependency versions;
- whether evaluation uses a local policy, remote server, or optimized runtime.

LIBERO results with different settings should be presented separately or accompanied by explicit protocol differences.

## SimplerEnv Checklist

Record at least:

- environment/task variant, including Google Robot or WidowX/Bridge route;
- visual matching or domain-randomization settings;
- policy checkpoint and action unnormalization key;
- control frequency and action horizon;
- evaluation episode count and seed policy;
- simulator, assets, and renderer versions.

## Real-Robot Checklist

SO100/SO101, DROID, ALOHA, humanoid, and other real-robot results should include:

- exact robot revision, cameras, calibration, controller, and control rate;
- training demonstrations and variation coverage;
- task reset and success criteria;
- number of trials, intervention policy, and excluded runs;
- inference hardware, communication path, and measured latency;
- safety controller or post-processing that changes policy outputs.

## Reporting Principles

1. Prefer official tables and scripts, but label all unverified numbers as author-reported.
2. Never infer equivalence from the benchmark name alone.
3. Keep simulation and real-robot evidence separate.
4. Report failed runs and protocol deviations alongside successful results when presenting a reproduction study.
5. A reproduced result requires the environment, checkpoint, and aggregation procedure to be specified.

