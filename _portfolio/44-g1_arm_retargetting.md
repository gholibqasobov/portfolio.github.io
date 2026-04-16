---
title: "Vision-Based Teleoperation of Unitree G1 Humanoid Robot"
excerpt: "Real-time human pose retargeting to Unitree G1 using MediaPipe and ROS2 <br/> ![g1_teleop](/portfolio.github.io/images/retargetting_real_robot.png)

"
collection: portfolio
---

This project presents the development of a vision-based teleoperation system for the Unitree G1 humanoid robot, enabling intuitive control of the robot’s upper body using human motion capture.

The system leverages MediaPipe for real-time human pose estimation, where detected arm and hand keypoints are mapped to the robot through a retargeting pipeline based on inverse kinematics (IK).

### Statement of the problem

Humanoid robots require precise and coordinated joint control to replicate human-like motion.

Direct mapping of human motion to robot joints is non-trivial due to kinematic differences, joint limits, and self-collision constraints.

A robust solution must ensure that generated motions are both feasible and safe for the robot, while maintaining responsiveness for real-time teleoperation.

### System Architecture

The developed system integrates multiple components into a unified pipeline:

- MediaPipe Pose Estimation: Extracts real-time human upper-body and hand keypoints from camera input.
- Inverse Kinematics Solver: Computes joint angles for both left and right arms of the Unitree G1.
- Collision-Aware Retargeting: Ensures safe motion by considering collisions with the robot body and between arms.
- ROS2 Humble Framework: Handles communication, control, and modular system integration.
- RViz Visualization: Provides real-time visualization of joint states and robot motion.


![rviz]({{ "/images/rviz.png" | relative_url }})

### NVIDIA Omniverse & Simulation

Before deployment on the physical robot, the system was validated in simulation using NVIDIA Isaac Sim, enabling safe and controlled testing.

Isaac Sim served as a digital twin of the Unitree G1, accurately modeling robot kinematics and environmental interactions. This allowed verification of:

IK solution stability
Motion smoothness and feasibility
Collision avoidance behavior

![isaacsim]({{ "/images/retargetting_isaacsim.jpg" | relative_url }})

### Deployment on Real Robot

After successful validation in simulation, the system was deployed on the real Unitree G1 humanoid robot.

The robot successfully replicated human arm motions in real time, demonstrating:

Accurate pose retargeting
Stable and smooth joint actuation
Safe operation with collision constraints

RViz was used alongside the hardware setup to monitor joint states and ensure consistency between commanded and executed motions.

![real_robot]({{ "/images/retargetting_real_robot_2.png" | relative_url }})

### Highlights: <br/><br/>
- **Vision-Based Teleoperation:** Controlled humanoid robot arms using real-time human pose estimation. <br/>
- **Inverse Kinematics Implementation:** Developed IK solvers for both arms with joint and workspace constraints. <br/>
- **Collision-Aware Motion Planning:** Incorporated self-collision and body collision avoidance. <br/>
- **Simulation-to-Real Pipeline:** Validated in Isaac Sim before deployment on physical hardware. <br/>
- **ROS2 Integration:** Built a modular and scalable control architecture using ROS2 Humble. <br/>
- **Real-Time Visualization:** Used RViz for monitoring and debugging robot joint states. <br/>
<br/>

### Results

<iframe width="560" height="315" src="https://www.youtube.com/embed/P-laYIH3FBA?si=8llYP0t90xRZSGs8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br/><br/>

This project demonstrates how computer vision and kinematic modeling can be combined to enable intuitive human-to-robot interaction, providing a foundation for future work in teleoperation, assistive robotics, and humanoid manipulation.