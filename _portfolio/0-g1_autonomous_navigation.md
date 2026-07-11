---
title: "Autonomous Navigation for the Unitree G1 Humanoid Robot"
excerpt: "ROS 2 Humble autonomous navigation using Nav2, SLAM Toolbox, and omnidirectional locomotion <br/> ![g1_navigation](/portfolio.github.io/images/g1_navigation_thumbnail.png)

"
collection: portfolio
---

This project presents the development of a complete autonomous navigation system for the Unitree G1 humanoid robot using ROS 2 Humble. The navigation stack combines mapping, localization, path planning, and obstacle avoidance with the robot's omnidirectional locomotion controller, enabling reliable autonomous navigation in indoor environments.

The system was validated on the physical robot, with extensive parameter tuning and integration to ensure stable navigation performance despite the unique locomotion characteristics of a humanoid platform.

### Statement of the Problem

Unlike wheeled mobile robots, humanoid robots introduce additional challenges for autonomous navigation due to body oscillations during walking, omnidirectional locomotion, and continuously changing sensor viewpoints.

Developing a reliable navigation system therefore requires careful integration of the locomotion controller with the navigation stack, robust localization, accurate environment mapping, and stable obstacle avoidance while maintaining smooth trajectory execution.

### System Architecture

The navigation framework integrates multiple ROS 2 components into a unified autonomous navigation pipeline:

- **SLAM Toolbox:** Generates occupancy grid maps while simultaneously estimating the robot's pose.
- **Nav2 Navigation Stack:** Performs global path planning, local trajectory generation, recovery behaviors, and navigation task execution.
- **Omnidirectional Locomotion Controller:** Executes navigation commands while accounting for the walking dynamics of the Unitree G1.
- **Costmaps & Obstacle Avoidance:** Maintains local and global environment representations for safe navigation around static and dynamic obstacles.
- **ROS 2 Humble:** Provides modular communication between localization, planning, perception, and control components.

### Mapping and Localization

The robot uses SLAM Toolbox to construct maps of previously unknown indoor environments while continuously estimating its pose.

Once a map has been created, the system transitions to localization mode, allowing the robot to accurately determine its position and navigate toward user-defined goal locations.

This approach enables autonomous operation in both newly explored and previously mapped environments.


### Autonomous Navigation

The generated maps are used by Nav2 to compute collision-free paths toward navigation goals.

During execution, the local planner continuously updates the robot's trajectory based on sensor observations, allowing it to safely avoid both static and dynamic obstacles while maintaining smooth motion.

Significant effort was dedicated to system integration and parameter tuning to achieve reliable performance on the physical Unitree G1 platform.


### Highlights: <br/><br/>

- **Complete Autonomous Navigation Pipeline:** Developed an end-to-end navigation system using ROS 2 Humble, Nav2, and SLAM Toolbox. <br/>
- **Indoor Mapping & Localization:** Enabled autonomous map creation and localization in previously mapped environments. <br/>
- **Global Planning & Local Control:** Integrated global path planning with real-time trajectory execution. <br/>
- **Obstacle Avoidance:** Implemented safe navigation around static and dynamic obstacles using layered costmaps. <br/>
- **Humanoid Navigation Integration:** Combined Nav2 with the Unitree G1 omnidirectional locomotion controller for reliable autonomous movement. <br/>
- **Physical Robot Validation:** Performed extensive integration, parameter tuning, and testing on the real Unitree G1 humanoid robot. <br/>

<br/>

### Results

<iframe width="560" height="315" src="https://www.youtube.com/embed/3kplVYuTJsw?si=va_CiXs0oR76e3_c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br/><br/>

This project demonstrates the integration of ROS 2 navigation technologies with a humanoid robotic platform, providing a robust foundation for autonomous service robotics applications such as inspection, guidance, and human-robot interaction.