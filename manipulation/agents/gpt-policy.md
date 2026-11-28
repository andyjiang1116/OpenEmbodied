# GPT-Policy

[简体中文](gpt-policy_ZH.md) · [Agent-Based Manipulation](README.md)

> In-context robot learning with VLM agents · [Paper](https://arxiv.org/abs/2609.19138) · [Project page](https://cheng-haha.github.io/GPT-Policy/) · [Official repository](https://github.com/cheng-haha/GPT-Policy)

<p align="center"><img src="https://arxiv.org/html/2609.19138v1/overview.png" alt="GPT-Policy context, VLM tool requests, robot controller, and feedback loop" width="820" /></p>

<p align="center"><em>Context-to-action architecture and feedback loop. Figure: <a href="https://arxiv.org/abs/2609.19138">original paper</a>.</em></p>

## Technical Summary

GPT-Policy studies whether a fixed general-purpose vision-language model can adapt robot behavior from information supplied at deployment, without gradient updates or task-specific parameter changes. It places the model inside a closed-loop robot-tool system. Demonstrations, goal images, interaction history, and human feedback can change the model's next tool request. The method is a system for in-context adaptation rather than a newly pretrained low-level action policy.

## Context and Model Input

At each decision, the model receives the task instruction, current camera images and robot state, available task references, recent interaction history, and the previous tool result. The paper studies five context families:

- **Human video:** ordered visual keyframes show a procedure without robot action labels.
- **Robot demonstration:** video may be paired with time-aligned end-effector poses, gripper states, and actions.
- **Goal image:** one image specifies the desired final arrangement without a movement sequence.
- **Self-interaction history:** prior observations, actions, errors, and outcomes remain available for replanning.
- **Online human interaction:** feedback and pointing can clarify or change the target during execution.

A context compiler preserves task-relevant visual transitions and aligns available state and action records with video keyframes. Robot action references contain more information than video alone; experiments comparing them must keep the visual and text inputs aligned.

## Tool Execution and Feedback

The VLM selects a structured tool name and arguments rather than writing arbitrary motor commands. Embodiment-specific adapters interpret motion targets, sample a pose path, solve inverse kinematics, time joint references, and execute them through the robot backend. Gripper commands and Cartesian moves use defined interfaces. A rejected request or completed movement returns an updated observation and an explicit result for the next model decision.

The public implementation includes adapters for ARX X5 and I2RT/YAM hardware and an optional RoboDojo simulation backend. This controller and tool layer is part of the evaluated system: observed success cannot be attributed solely to the model's language or vision capability.

## Evaluation and Findings

The paper compares context conditions across real-robot tasks and RoboDojo simulation, measuring success, number of model decisions, and elapsed execution time. The project page reports that, over four real-robot demonstration tasks, mean success rises from 10% without demonstrations to 80% with human video or robot demonstrations with action references. It also reports 36/50 successes on ten selected RoboDojo tasks under its one-shot setting. These are separate experimental settings, not one aggregate benchmark result.

In the real-robot contact tasks, robot video plus aligned actions can clarify motion that is ambiguous between video keyframes. Goal images supply relative object locations; interaction history lets the agent revise a plan after observing the result of its own actions. The paper reports that extra context does not automatically solve precise contact, outcome verification, execution latency, or physical safety. Its experimental series are small and tied to selected platforms and model conditions.

## Reuse Conditions

The official repository supplies the framework and setup instructions, but physical deployment requires a compatible robot adapter, calibrated cameras and coordinate frames, validated tool limits, and the corresponding third-party SDKs. A comparison should identify the VLM, context type, demonstration content, decision budget, execution controller, task success criteria, and whether rejected tool calls consume time. Hardware-specific SDK and third-party terms must be checked separately.

## How Context Changes a Fixed Policy

GPT-Policy keeps the VLM parameters fixed. Adaptation occurs through the prompt and interaction loop: a demonstration shows an example transition, a goal image specifies a desired arrangement, and recent history tells the model which attempted moves succeeded or failed. These signals have different information content. Human video can show ordering and object interaction without revealing robot joint commands. A robot demonstration with aligned actions additionally shows how a particular platform moved. A goal image specifies an endpoint but leaves the motion sequence underdetermined.

At each decision, the model issues a structured tool request. The adapter checks and converts that request into robot motion, and the returned observation becomes evidence for the next request. This loop can recover from some planning errors, but its result depends on tool limits, camera calibration, controller implementation, and the number of decisions allowed. The approach is relevant when task-specific gradient training is unavailable but useful demonstrations or feedback can be supplied at execution time; precise contact and hard real-time control remain separate engineering requirements.

## References

- [Paper](https://arxiv.org/abs/2609.19138)
- [Project page](https://cheng-haha.github.io/GPT-Policy/)
- [Official repository](https://github.com/cheng-haha/GPT-Policy)
