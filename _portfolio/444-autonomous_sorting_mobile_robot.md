---
title: "Vision-Based Teleoperation of Unitree G1 Humanoid Robot"
excerpt: "Autonomous warehouse robot for logistics using ROS2, Nav2, and Isaac Sim <br/> ![g1_teleop](/portfolio.github.io/images/diploma_title.png)

"
collection: portfolio
---

### Project being implemented:
- Qasobov Gholibjon
- Abzhal Aybergen
- Ryaguzova Polina
- Kaziyev Nurtay


### Statement of the problem

Additive manufacturing has significantly improved production efficiency; however, post-processing tasks such as part handling and transportation remain largely manual, leading to increased costs and potential errors. This challenge is further amplified by the growing number of 3D printing facilities and limited automation in warehouse environments.

This project focuses on the development of an autonomous mobile robot designed to streamline logistics in additive manufacturing. The robot operates within an industrial warehouse, autonomously navigating between multiple 3D printers, exchanging filled and empty containers, and maintaining a continuous production cycle while avoiding dynamic obstacles.

<!-- process block diagram  -->
![rviz]({{ "/images/pbd_isaacsim.png" | relative_url }} 

<br/><br/>

![rviz]({{ "/images/fbd.jpg" | relative_url }} 


### System Architecture
A complete simulation-to-real pipeline was implemented. The system was first developed and validated in NVIDIA Isaac Sim, where a digital twin of the robot and warehouse environment was created. The robot model, designed in Fusion 360 and converted to URDF, enabled accurate simulation of kinematics, sensors, and physical interactions.

<!-- isaac sim digital twin -->
![rviz]({{ "/images/isaacsim_dd.png" | relative_url }} 


### Simulation and Digital Twin
Autonomous navigation was achieved using ROS2 and the Nav2 stack, incorporating SLAM-based mapping, real-time localization, and dynamic path planning. RViz was used to monitor sensor data and validate the TF tree, ensuring correct alignment of LiDAR, camera, and IMU frames.

<!-- slam and nav -->
![rviz]({{ "/images/slam.png" | relative_url }}
<br/><br/>

![rviz]({{ "/images/nav.png" | relative_url }}


### Robot Assembly
The physical robot was built using a modular aluminum frame, integrating an NVIDIA Jetson Orin Nano, LiDAR, and onboard sensors. To coordinate operations, the system utilizes ROS2 Action Servers, enabling communication with a PLC for task execution and feedback.
<!-- robot setup and architectural scheme -->

![isaacsim]({{ "/images/architecture_sys.png" | relative_url }})

<br/><br/>
![isaacsim]({{ "/images/robot_assembly.png" | relative_url }})

### Key functionalities
- Autonomous Navigation with dynamic obstacle avoidance
- Precision Docking using AprilTag-based localization
- Automated Loading/Unloading of 3D-printed parts



### Results

<iframe width="560" height="315" src="https://www.youtube.com/embed/OQcwlTI0U-g?si=npltdz1_k7ry2NQX" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br/><br/>

This project demonstrates a scalable robotic solution for automating logistics in additive manufacturing, bridging the gap between simulation and real-world industrial deployment.