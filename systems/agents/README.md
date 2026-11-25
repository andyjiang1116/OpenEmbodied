# Agent-Based Manipulation

[简体中文](README_ZH.md) · [Embodied Systems](../README.md) · [Manipulation paradigms](../../analysis/manipulation-paradigms/README.md)

Agent-based manipulation places a multimodal model inside a closed-loop execution system. The model may choose robot commands, review another policy's proposal, or decide when to call a learned skill. A controller and tool interface convert decisions into bounded physical actions and return observations for the next decision.

| Control pattern | Representative work | Agent's role |
| --- | --- | --- |
| Direct and hybrid action control | [GPT-6 Astra as an Embodied Policy](gpt-as-policy.md) | Generate end-effector targets directly or review and correct π0.5 action candidates |
| Selective intervention | [π0.5 + Astra with Selective Intervention](pi05-call-astra.md) | Take over when a learned trigger detects a recovery need |
| In-context robot learning | [GPT-Policy](gpt-policy.md) | Use demonstrations and execution history to propose constrained robot-tool actions |

The distinction is the control interface, not the underlying model name. Evaluation should report the action authority of each component, observation frequency, latency, controller constraints, robot embodiment, and whether physical time continues during reasoning.
