---
title: "Unitree G1 Robot Guide"
excerpt: "Autonomous humanoid guide combining conversational AI, RAG, and indoor navigation <br/> ![robot_guide](/portfolio.github.io/images/g1_guide_thumbnail.png)

"
collection: portfolio
---

This project presents the development of an autonomous Robot Guide for the Unitree G1 humanoid robot, capable of interacting naturally with visitors and autonomously guiding them through indoor environments.

The system combines a retrieval-augmented conversational AI pipeline with autonomous navigation, enabling the robot to answer questions using domain-specific knowledge and escort users to predefined destinations. A web-based management interface was also developed, allowing non-technical users to configure the robot without interacting directly with ROS.

### Statement of the Problem

Service robots operating in public spaces must be capable of both natural human interaction and reliable autonomous navigation. While conversational AI and mobile robotics have individually matured, integrating these capabilities into a unified system presents several challenges.

The robot must understand user requests, retrieve accurate information from a custom knowledge base, determine whether navigation is required, and safely escort users to their destination while maintaining a seamless interaction experience.

### System Architecture

The Robot Guide integrates multiple software components into a unified service robotics platform:

- **Conversational AI:** Supports natural language interaction using local or cloud-hosted Large Language Models (LLMs).
- **Retrieval-Augmented Generation (RAG):** Retrieves relevant information from custom knowledge bases to provide context-aware responses.
- **Autonomous Navigation:** Uses ROS 2 Humble, Nav2, and SLAM Toolbox for mapping, localization, path planning, and obstacle avoidance.
- **Robot Behavior Manager:** Coordinates dialogue, navigation requests, and user interactions.
- **Web Management Interface:** Allows operators to configure maps, guide destinations, and conversational knowledge through an intuitive browser-based interface.

### Conversational AI

The conversational system enables the robot to communicate naturally with visitors using Retrieval-Augmented Generation (RAG).

Instead of relying solely on a language model's internal knowledge, the system retrieves relevant information from a custom knowledge base before generating responses. This approach allows the robot to answer organization-specific questions while supporting both locally hosted and cloud-based LLMs.


### Autonomous Visitor Guidance

When a visitor requests assistance reaching a specific location, the Robot Guide transitions from conversation to autonomous navigation.

Using maps generated with SLAM Toolbox and the Nav2 navigation stack, the robot plans and executes collision-free paths while continuously avoiding static and dynamic obstacles. Upon reaching the destination, it resumes conversational interaction with the visitor.


### Web-Based Management Interface

To simplify deployment and maintenance, a web-based management interface was developed for operators without robotics expertise.

Through the interface, users can:

- Create and manage navigation maps
- Configure guide destinations and points of interest
- Upload and organize documents for the RAG knowledge base
- Configure robot behavior without directly interacting with ROS 2

This allows the system to be adapted to new environments with minimal technical knowledge.


### Highlights: <br/><br/>

- **Conversational AI:** Developed a natural language interaction system using Retrieval-Augmented Generation (RAG). <br/>
- **Flexible LLM Backend:** Supported both locally hosted and cloud-based Large Language Models. <br/>
- **Autonomous Navigation:** Integrated ROS 2, Nav2, and SLAM Toolbox for reliable indoor navigation and obstacle avoidance. <br/>
- **Human-Robot Interaction:** Combined conversation and navigation into a seamless visitor guidance workflow. <br/>
- **Web-Based Configuration:** Built an intuitive interface for managing maps, guide destinations, and conversational knowledge. <br/>
- **Real Robot Deployment:** Integrated and validated the complete system on the Unitree G1 humanoid robot. <br/>

<br/>

### Results

<iframe 
  width="315" 
  height="560" 
  src="https://youtube.com/shorts/Ka-Kt-AqR6Y?si=PGcvqRj3GG0GV6vM" 
  title="YouTube video player" 
  frameborder="0" 
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
  allowfullscreen>
</iframe>

<br/><br/>

The Robot Guide demonstrates how conversational AI, autonomous navigation, and intuitive system management can be combined into a practical service robotics application. By integrating language understanding, knowledge retrieval, and reliable navigation within a single platform, the system provides a foundation for next-generation humanoid assistants in public spaces such as offices, museums, universities, hospitals, and exhibition centers.