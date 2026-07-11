---
title: "IsaacLegs: RL Policy Deployment Framework for Legged Robots"
excerpt: "Open-source framework for deploying NVIDIA Isaac Lab policies into Isaac Sim digital twins using ROS 2 <br/> ![isaaclegs](/portfolio.github.io/images/isaaclegs_thumbnail.png)

"
collection: portfolio
---

IsaacLegs is an open-source reinforcement learning deployment framework that enables policies trained in NVIDIA Isaac Lab to be deployed into NVIDIA Isaac Sim digital twins through ROS 2.

The framework provides ready-to-use digital twins, reusable ROS 2 interfaces, and a robot-agnostic policy controller, simplifying the deployment of locomotion policies across different legged robot platforms.

[IsaacLegs GitHub Repository](https://github.com/gholibqasobov/IsaacLegs)

### Overview

Reinforcement learning allows legged robots to learn complex locomotion behaviors in simulation. However, transferring trained policies into realistic robot environments often requires significant robot-specific integration.

IsaacLegs addresses this challenge by providing a unified workflow connecting Isaac Lab training environments, Isaac Sim digital twins, and ROS 2-based robot controllers.

### System Architecture

The framework consists of three main components:

- **Isaac Lab:** Used for reinforcement learning policy training and exporting deployable policies.
- **Isaac Sim Digital Twins:** Provide realistic robot simulation environments with integrated sensors and control interfaces.
- **ROS 2 Policy Controller:** Executes trained policies and communicates with the simulated robot through standard ROS 2 interfaces.

### Supported Robots

IsaacLegs currently supports:

- Unitree Go2 quadruped
- Unitree G1 humanoid
- Unitree G1 humanoid (29-DOF configuration)

Each platform includes a ready-to-run digital twin, sensor interfaces, and deployment configuration.

### Digital Twin Integration

The provided digital twins integrate robot state, control interfaces, and sensor streams including:

- Joint states and commands
- IMU
- Odometry
- RGB and depth cameras
- LiDAR and point clouds

The framework also supports custom robots and environments through NVIDIA Isaac Sim's USD-based workflow.

### Highlights: <br/><br/>

- **Reinforcement Learning Deployment:** Deploy locomotion policies trained in NVIDIA Isaac Lab into Isaac Sim environments. <br/>
- **Robot-Agnostic Architecture:** Support multiple robot platforms without implementing separate controllers. <br/>
- **ROS 2 Integration:** Provides standardized communication between simulation, controllers, and external robotics systems. <br/>
- **Digital Twin Workflow:** Enables rapid testing and development using configurable Isaac Sim environments. <br/>
- **Extensible Framework:** Designed for future applications including navigation, SLAM, manipulation, and sim-to-real research. <br/>

<br/>

### Results

<video width="560" height="315" controls>
  <source src="{{ '/videos/isaaclegs_overview_vid.mp4' | relative_url }}" type="video/mp4">
  Your browser does not support the video tag.
</video>

<br/><br/>

IsaacLegs provides a reusable foundation for developing and deploying reinforcement learning-based controllers for legged robots, reducing the engineering effort required to move from policy training to robotic simulation and experimentation.