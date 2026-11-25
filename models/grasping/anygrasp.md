# AnyGrasp

[简体中文](anygrasp_ZH.md) · [Grasping models](README.md)

> Parallel-gripper grasp detection and tracking from point clouds · [Project](https://graspnet.net/anygrasp.html) · [SDK](https://github.com/graspnet/anygrasp_sdk) · [Paper](https://arxiv.org/abs/2212.08333)

<p align="center">
  <img src="../../docs/assets/models/grasping/anygrasp-demo.gif" alt="AnyGrasp grasp perception demonstration" width="820" />
</p>

*Official project demonstration.*

## Technical Summary

- **Problem:** Detect stable 6-DoF grasp poses and track them over time in cluttered or dynamic scenes.
- **End effector:** Parallel gripper.
- **Observation:** Point clouds derived from depth sensing, optionally cropped or masked for a target region.
- **Output:** Grasp pose, width, score, and tracked candidates for downstream motion planning.

## Technical Contribution

Many grasp detectors treat each frame independently. AnyGrasp joins spatial grasp perception with temporal correspondence, so a robot can preserve stable candidates while the camera, objects, or robot move. The system targets practical throughput and has demonstrations spanning clutter removal, deformable objects, transparent objects, and moving targets.

## Technical Shape

The spatial component builds on dense graspability reasoning from the GraspNet and Graspness / GSNet line. Candidate generation is paired with objectness filtering and model-free collision checking. The temporal component associates grasps across consecutive observations, reducing pose jitter and avoiding a complete restart at every frame.

The released SDK exposes options for dense prediction, object-mask filtering, and collision detection. Dense mode trades additional memory and latency for more candidates and is intended for special cases rather than the default path.

## Deployment Boundary

AnyGrasp is a perception component, not a complete pick-and-place policy. A working robot system still needs calibrated RGB-D sensing, point-cloud preprocessing, robot–camera transforms, candidate selection, inverse kinematics, motion planning, gripper control, and failure recovery.

The current SDK documentation lists Python 3.6–3.14, PyTorch 1.7.1+, CUDA 11.x/12.x/13.x, and MinkowskiEngine 0.5.4. The supported combination still depends on the target GPU, operating system, and compiled extensions; the [official installation instructions](https://github.com/graspnet/anygrasp_sdk#installation) define the current setup.

## Availability and License Boundary

The official repository provides SDK wrappers and examples, while use of the core library requires license registration. The SDK replaced its previous license tool in July 2026; existing instructions based on the older `lib_cxx.so` or `license_checker` tools do not apply to the updated release. The [current registration guide](https://github.com/graspnet/anygrasp_sdk/tree/main/license_registration) should be consulted before installation or redistribution.

## References

- [Official project page](https://graspnet.net/anygrasp.html)
- [Official AnyGrasp SDK](https://github.com/graspnet/anygrasp_sdk)
- [AnyGrasp paper](https://arxiv.org/abs/2212.08333)
- [GraspNet project](https://graspnet.net/)
