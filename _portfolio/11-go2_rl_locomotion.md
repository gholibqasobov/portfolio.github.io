---
title: "Go2 Locomotion by Reinforcement Learning"
excerpt: "Unitree Go2 Locomotion Policy Trained with PPO in Isaac Lab <br/>  ![go2_locomotion](/portfolio.github.io/images/go2_camera_isaaclab.png)"

collection: portfolio
---

This project presents the development of a **reinforcement learning-based locomotion policy** for the **Unitree Go2 quadruped robot**, trained using **Isaac Lab** and deployed in **Isaac Sim** for high-fidelity simulation.

Reinforcement learning (RL) is a branch of machine learning in which an agent learns to make decisions through interactions with its environment.

![rl_overview]({{ "/images/rl_.png" | relative_url }})


### Statement of the problem
STATEMENT OF THE PROBLEM​
Quadrupedal robots like Unitree Go1 and Go2 require precise coordination of multiple joints to maintain balance and produce smooth movement.​


Traditional control methods, such as Model Predictive Control (MPC), rely on complex physics models and are computationally intensive for real-time operation.​


Reinforcement learning offers a faster, learning-based alternative by enabling the robot to map observed states directly to control actions through trial and error.​
![kinematics_vs_policy]({{ "/images/kinematic_to_policy.png" | relative_url }})
​

### NVIDIA Omniverse
NVIDIA Omniverse:​

Isaac Sim is a realistic robot simulator that models physics, sensors, and how the
robot interacts with its surroundings.​


Isaac Lab is a Reinforcement Learning Platform built on top of Isaac Sim.
It streamlines reinforcement learning pipelines by supporting vectorized
environments, parallel simulation, and structured RL interfaces.​

​![omniverse]({{ "/images/omniverse.png" | relative_url }})


### Training

The locomotion policy was trained using **Proximal Policy Optimization (PPO)** implemented through the **RSL-RL framework**. The objective of the policy was to achieve **robust velocity tracking**, enabling the robot to follow commanded linear and angular velocities while maintaining stable and natural gait patterns.

![pipeline]({{ "/images/pipline_go2_locomotion.png" | relative_url }})

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

Training the locomotin in vectorized environment
![training_1]({{ "/images/training_isaaclab.png" | relative_url }})

<br/><br/>

![training_2]({{ "/images/training_isaaclab_2.png" | relative_url }})

<br/><br/>

Deployed Policy in IsaacSim

![deployment]({{ "/images/deployed_policy_isaacsim.png" | relative_url }})


### Results

<iframe width="560" height="315" src="https://www.youtube.com/embed/YcYta5fGbXY?si=zPlj9ihTBv1Sl64J" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br/><br/>

This project demonstrates how **reinforcement learning and simulation-driven training** can be used to develop **robust locomotion policies for legged robots**, forming a foundation for future work in **real-world deployment and autonomous navigation**.
