---
title: "Go2 Locomotion by Reinforcement Learning"
excerpt: "Unitree Go2 Locomotion Policy Trained with PPO in Isaac Lab <br/>  ![go2_locomotion](images/go2_camera_isaaclab.png)"

collection: portfolio
---

This project presents the development of a **reinforcement learning-based locomotion policy** for the **Unitree Go2 quadruped robot**, trained using **Isaac Lab** and deployed in **Isaac Sim** for high-fidelity simulation.

The locomotion policy was trained using **Proximal Policy Optimization (PPO)** implemented through the **RSL-RL framework**. The objective of the policy was to achieve **robust velocity tracking**, enabling the robot to follow commanded linear and angular velocities while maintaining stable and natural gait patterns.

![go2_locomotion](images/start_of_training_isaaclab.png)

My main contribution focused on the **design of the reinforcement learning pipeline**. I formulated the **Markov Decision Process (MDP)**, including the definition of observation space, action space, and termination conditions. A key part of the work was the **design of reward functions**, carefully balancing multiple objectives such as velocity tracking accuracy, energy efficiency, and stability to achieve smooth and reliable locomotion.

The training process was conducted entirely in simulation using **Isaac Lab**, with deployment and validation performed in **Isaac Sim**, allowing for realistic physics and robot behavior.

Highlights: <br/><br/>
- **Reinforcement Learning Locomotion**: Trained a quadruped robot to achieve stable walking using PPO. <br/>
- **Velocity Tracking Control**: Learned to follow commanded linear and angular velocities. <br/>
- **MDP Design**: Defined observation space, action space, reward functions, and termination logic. <br/>
- **Custom Reward Engineering**: Designed reward terms for stability, tracking accuracy, and smooth motion. <br/>
- **Simulation Pipeline**: Trained in Isaac Lab and deployed in Isaac Sim for validation. <br/>

<br/>

### Training & Deployment Pipeline

![go2_pipeline](images/training_isaaclab.png)

<br/><br/>

![go2_pipeline](images/training_isaaclab_2.png)


### Results

<iframe width="560" height="315" src="https://www.youtube.com/embed/YcYta5fGbXY?si=zPlj9ihTBv1Sl64J" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br/><br/>

This project demonstrates how **reinforcement learning and simulation-driven training** can be used to develop **robust locomotion policies for legged robots**, forming a foundation for future work in **real-world deployment and autonomous navigation**.