# π0.5 + Astra with Selective Intervention

[简体中文](pi05-call-astra_ZH.md) · [Agent-Based Manipulation](README.md)

> Learned handoff from a robot policy to a reasoning model · [Paper](https://arxiv.org/abs/2610.14117) · [Project page](https://kykgeek.github.io/Pi05_CALL_Astra/)

<p align="center"><img src="https://arxiv.org/html/2610.14117v1/method_overview.png" alt="CALL detector, π0.5 policy, and Astra recovery handoff" width="820" /></p>

<p align="center"><em>Selective policy-to-agent handoff. Figure: <a href="https://arxiv.org/abs/2610.14117">original paper</a>.</em></p>

## Technical Summary

Continuous review of a robot policy by a large reasoning model can add latency and token cost even when the policy is acting correctly. This work keeps a frozen π0.5 policy as the ordinary controller and trains a lightweight CALL head to estimate when assistance is needed. GPT-6 Astra enters the loop only after a trigger and returns control to π0.5 after recovery. The research question is whether a learned local handoff can retain the benefit of reasoning assistance without querying Astra at every step.

## Detector Inputs and Training

The frozen OpenPI `pi05_libero` policy proposes a 10-step, seven-dimensional action chunk. CALL reads a pooled vision-language representation, pooled action-token features, robot state, and statistics of that action chunk from the existing policy pass. A small three-branch network combines these features into a calibrated probability that help is needed; it does not call an external model to make this prediction.

Training examples combine normally progressing policy states with failure states from LIBERO-Recovery. For each saved state, repeated π0.5-only continuations estimate how often the base policy can finish the task. The detector's soft target is higher when that continuation success rate is lower. The paper reports 5,055 competence-state examples across task folds and uses task-specific detectors with suite-level fallbacks. This supervision labels a need for assistance from policy competence rather than from an arbitrary visual anomaly.

## Handoff and Recovery Loop

During normal execution, the system consumes five actions from each policy chunk before querying π0.5 and CALL again. A sustained trigger requires four of the latest five help scores above a calibrated threshold; a separate hard threshold can trigger immediately. A cooldown limits repeated consultations. When handoff occurs, queued π0.5 actions are discarded.

Astra then receives external and wrist RGB views, task instruction, measured robot state, the policy proposal, and execution history. It may issue a short sequence of end-effector corrections or return control without acting. The host validates and converts accepted corrections into LIBERO's action interface, executes them, and obtains a fresh π0.5 proposal before resuming. This makes consultation, actual Astra action, and successful recovery distinct events.

## Evaluation and Reported Results

The paper evaluates LIBERO-10, Object, Goal, and Spatial: ten tasks and five test episodes per suite, for 200 episodes in total. The hybrid succeeds in 195/200 episodes (97.5%) against 191/200 (95.5%) for π0.5 alone. Most of the four-episode difference arises in LIBERO-10; Object, Goal, and Spatial have the same reported success counts under both methods.

The system consults Astra in 61/200 episodes but executes Astra actions in 13/200. Across all four suites, Astra executes 12.44% of environment steps; the 5.49% figure in the abstract applies specifically to Object, Goal, and Spatial. These denominators matter when interpreting “selective” intervention. The paper also reports token use and environment-action throughput, which should accompany success when reasoning-model latency or cost is relevant.

## Interpretation and Reuse

The system depends on the frozen π0.5 checkpoint, competence-labeled recovery states, calibrated detector thresholds, a specific action interface, and Astra access. Its LIBERO results cannot be directly combined with selected RoboDojo results from continuously reviewing hybrid agents. Reproduction must specify what triggers consultation, what counts as an executed intervention, how long the agent retains control, and when the policy resumes.

## What the Handoff Detector Actually Predicts

CALL does not recognize a generic visual anomaly or ask Astra whether a scene is difficult. It estimates the frozen policy's chance of completing the task from the current state, using features already produced by that policy and continuation outcomes collected during training. A low estimated chance indicates that an external intervention may be useful. The threshold and persistence rule trade unnecessary calls against missed failures; the cooldown prevents rapid repeated handoffs. Once Astra acts, the system obtains a new observation and a fresh π0.5 proposal before returning control.

The distinction between a consultation and an executed correction is essential. An Astra call may inspect a state and hand control back without issuing an action; only some calls become robot steps. When reproducing the system, report all three rates: episodes with consultation, episodes with an Astra action, and the proportion of executed steps controlled by Astra. This method is relevant when a strong base policy already handles most states and external reasoning is reserved for recovery, rather than when every action requires agent planning.

## References

- [Paper](https://arxiv.org/abs/2610.14117)
- [Project page](https://kykgeek.github.io/Pi05_CALL_Astra/)
