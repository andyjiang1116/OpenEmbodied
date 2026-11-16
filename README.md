<div align="center">
  <img src="docs/assets/openembodied-wordmark.png" alt="OpenEmbodied" width="760" />

  <p><strong>An evidence-first atlas for Embodied AI.</strong></p>
  <p>Track the frontier · Compare methods · Reproduce what matters</p>
  <p>
    <a href="README_ZH.md">简体中文</a>
    ·
    <a href="#-why-openembodied">Why OpenEmbodied</a>
    ·
    <a href="#-evidence-levels">Evidence Levels</a>
    ·
    <a href="#-roadmap">Roadmap</a>
  </p>
</div>

---

## 🌐 About

Embodied AI moves quickly, but more information does not always produce better understanding. Papers use different datasets, evaluation protocols, hardware, and reporting conventions; repositories often show successful demos without documenting the conditions or failures behind them.

**OpenEmbodied turns scattered resources into structured, comparable, and verifiable knowledge.**

Instead of building another link collection, this project records what a method solves, how it works, what evidence supports it, what it costs to reproduce, and where it stops working.

> [!IMPORTANT]
> OpenEmbodied is in its foundation stage. The standards and first flagship collections are being designed before the repository expands in breadth.

## ✨ Why OpenEmbodied

| Common problem | OpenEmbodied approach |
| --- | --- |
| Long lists of papers with little context | Concise Research Profiles with a consistent schema |
| Results that are difficult to compare | Dataset, benchmark, metric, and evaluation-protocol context |
| “Open source” without reproducibility details | Explicit code, weights, data, license, compute, and environment status |
| Successful demos without failure analysis | Limitations, failure modes, and unresolved questions |
| Tutorials that become stale silently | Verification dates and evidence levels |

## 🧭 Core Tracks

```text
Track → Understand → Verify → Choose
```

### 🔭 Frontier Watch

A focused digest of important work across VLA models, world models, manipulation, navigation, humanoids, data, and evaluation. Every item must link to a primary source and explain why it matters.

### 🗂️ Research Profiles

Standardized technical profiles for papers, models, datasets, and systems:

- problem and motivation;
- method and key design choices;
- data, benchmarks, metrics, and compute;
- code, weights, license, and release status;
- results, limitations, and failure modes;
- related work and last verification date.

### 🧪 Reproduction Reports

Reproduction records that preserve the environment, commands, hardware, outputs, metric gaps, fixes, and failed attempts—not only the final successful screenshot.

### ⚖️ Comparison Guides

Living comparison pages that help answer practical questions such as:

- Which VLA model fits a given robot, dataset, or compute budget?
- Which benchmark measures the capability I care about?
- What is actually open and reproducible?
- Which results can be compared fairly?

## 🧾 Evidence Levels

Every technical entry can carry an evidence level. The level describes what has been verified by OpenEmbodied; it is not a quality score for the original work.

| Level | Meaning |
| --- | --- |
| **L0 — Reviewed** | Primary sources have been read and summarized |
| **L1 — Installable** | The documented environment can be installed |
| **L2 — Runnable** | An official or minimal demo runs successfully |
| **L3 — Reproduced** | A reported metric or experiment is reproduced with recorded conditions |
| **L4 — Validated** | The method is verified on real hardware or an additional platform/task |

## 🎯 Initial Focus

The first release cycle will concentrate on three connected areas:

1. **[VLA Landscape](comparisons/vla-landscape/README.md)** — architecture, training data, action representation, embodiment, compute, openness, and evaluation.
2. **Benchmark Map** — tasks, protocols, metrics, comparability, and common interpretation errors.
3. **Reproduction Reports** — transparent records of environments, results, deviations, and failures.

This narrow starting point is intentional. A small set of reliable reference pages is more useful than a large set of shallow entries.

## 🗺️ Coverage Map

| Area | Representative topics |
| --- | --- |
| Vision-Language-Action | Generalist policies, action tokenization, multimodal grounding |
| World Models & Planning | Predictive models, planning, long-horizon reasoning |
| Manipulation | Grasping, dexterity, bimanual and mobile manipulation |
| Navigation | Spatial reasoning, mapping, exploration, VLN |
| Locomotion & Humanoids | Whole-body control, loco-manipulation, motion learning |
| Data & Evaluation | Robot datasets, simulators, benchmarks, evaluation protocols |

## ✅ Curation Standard

An entry should:

- cite original papers, official repositories, project pages, and datasets;
- distinguish authors' claims from our interpretation and reproduced observations;
- record publication and verification dates;
- state whether code, weights, data, and licenses are actually available;
- explain evaluation conditions before comparing numbers;
- document limitations and negative results;
- remain concise enough to scan and detailed enough to verify.

## 🚧 Roadmap

- [ ] Publish the topic taxonomy and repository structure.
- [ ] Release Research Profile and Reproduction Report templates.
- [x] Publish the first [Open VLA Landscape](comparisons/vla-landscape/README.md) research release.
- [ ] Publish the first Benchmark Map.
- [ ] Curate the first 12 Research Profiles.
- [ ] Complete two reproducible experiments with recorded evidence.
- [ ] Start a focused weekly Frontier Watch.

## 🤝 Contributing

OpenEmbodied welcomes corrections, primary-source updates, Research Profiles, benchmark notes, and reproduction reports.

A useful contribution includes:

- the official source and release date;
- the relevant research area;
- a factual summary and reason for inclusion;
- availability of code, weights, data, and license;
- evaluation or reproduction evidence when available;
- known limitations or unresolved questions.

Contribution templates will be added with the first repository structure release. Until then, open an Issue to propose a resource or correction.

## 🙏 Acknowledgments

OpenEmbodied is inspired by the researchers, engineers, educators, and open-source contributors advancing embodied intelligence.

External papers, code, datasets, and other resources remain the property of their respective owners. Follow each source's license and citation requirements.
