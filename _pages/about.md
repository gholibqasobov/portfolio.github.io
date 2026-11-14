---
permalink: /
title: "👋 Hi, I'm Gholib!"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---
I am a **Robotics & Physical AI Engineer at Freedom X**, the R&D lab of Freedom Holding, where I work on **embodied autonomy for last-mile delivery in urban environments**. In **November 2026 our team launched the first robot-dog deliveries in Almaty, Kazakhstan**.
### 🧭 Research Direction

Urban sidewalks are among the hardest settings for a mobile robot. They are unstructured and crowded, and the rules governing them are mostly implicit. Pedestrians, cyclists, curbs, ramps, doors and changing terrain all have to be understood rather than merely avoided. Classical pipelines, which split perception, mapping, planning and control into hand-tuned modules, struggle to scale to this long tail of situations.

Our goal is to teach **a reasoning-based vision-language-action (VLA) policy for autonomous sidewalk navigation**: a single model that perceives the scene, reasons about it the way a person would, and acts on it. The robot should not only reach its goal safely, but also understand *why* a given action is right in context. This mirrors how end-to-end reasoning models are reshaping autonomous driving, carried over to legged and wheeled-legged robots in pedestrian space.

### ✅ What We Have Achieved So Far

- **Learned whole-body control.** A hierarchy of reinforcement-learning policies, trained entirely in simulation: robust locomotion over rough terrain, goal-directed navigation, and a learned safety layer that avoids obstacles in real time. Each level builds on the frozen level beneath it.
- **Sim-to-real transfer.** These policies have been deployed on the physical robot, with the full chain validated in high-fidelity digital twins before every real-world run.
- **Real-world operation.** The autonomy stack now supports the robot dogs in real deliveries on the streets of Almaty in Kazakhstan.
- **Photorealistic closed-loop simulation.** A simulator that reconstructs real recorded sidewalks as neural 3D scenes, preserving the real pedestrians and vehicles as replayable agents. A policy can therefore be trained and evaluated against what the robot would actually see.

### 🔭 What Comes Next

The next stage is to move from reactive control to **reasoning**. We are collecting real-world sidewalk data, scaling the reconstructed-scene simulator into a closed-loop training and evaluation environment, and training a VLA policy that unifies perception, reasoning and action for urban navigation. In the long run, I am working toward robots that learn robust, interpretable behavior in simulation and carry it reliably into the complexity of the real world.

<br/>

### 📜 Publications

* ### A Vision-Based Safety System for Human–Robot Collaboration Using a Real-Time Digital Twin in RoboDK
  *[Journal of Mechanical Science and Technology (2026)](https://link.springer.com/article/10.1007/s12206-026-2213-6).*
  A low-cost, vision-based safety monitoring system for human–robot collaboration in industrial environments. The robot's real-time digital twin defines dynamic safety zones around the human operator.

* ### Autonomous Multi-Floor Inspection Mobile Legged-Robot with Elevator Integration
  *Under review*
  An autonomous legged inspection robot that navigates between floors using elevators, with 95% inspection precision and 90% reliability on floor transitions.

* ### Development of a Mobile Robot Platform for Smart Warehouse Management
  *[Herald of Kazakh-British Technical University (2024)](https://gholibqasobov.github.io/portfolio.github.io/publication/2024-07-01-development-mobile-robot-smart-warehouse).*
  LiDAR-based navigation and grid positioning for an autonomous warehouse mobile robot, integrated with industrial control systems over OPC UA.

<br/>

# 🎉 Activities and Achievements

🥈 **National Competition of Students' Research Works (NIRS), 2026.** Automation and Control section. Awarded a Ministry diploma of the II degree; 35 works from 20 universities competed.

🥇 **1st Place, Digital Bridge 2025 Robotics Hackathon (Humanoid Robots track), Astana, 2025.** Built autonomous patrol navigation for a quadruped robot in maze-like environments, with a web interface for setting routes and watching the live camera.

🏆 **The Best Tech Talent, KBTU Awards 2026.**

🎤 **Invited Speaker, "Robotics Meets AI" workshop, KBTU (2025).** Delivered a lecture on the Robot Operating System (ROS) as the software foundation of modern robotic systems.

🤖 **Judge, Robo-Football Competition, ITFest 2024 & 2025.** Also presented KBTU's robotics research and projects to visitors and industry representatives.

🏅 **Finalist**, KAZENERGY Student Energy Challenge (2024) and the Open Olympiad in Electrical Engineering, Satbayev University (2023).

<br/>

# Projects
💼 See my [portfolio](https://gholibqasobov.github.io/portfolio.github.io/portfolio/) for details on each project.
