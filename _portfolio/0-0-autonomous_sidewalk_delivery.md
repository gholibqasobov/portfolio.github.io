---
title: "Toward Reasoning-Based Autonomous Navigation for Last-Mile Delivery Robots"
excerpt: "Learned locomotion, navigation and safety for wheeled quadruped delivery robots, deployed in real deliveries in Almaty, and the path toward a vision-language-action policy that reasons about urban sidewalks. <br/> ![delivery_robot](/portfolio.github.io/images/delivery/robot_platform.jpg)

"
collection: portfolio
---

<style>
  .fig { margin: 1.6em 0; text-align: center; }
  .fig img, .fig video { width: 100%; height: auto; border-radius: 6px; }
  .fig figcaption { font-size: 0.78em; color: #6a6a6a; margin-top: 0.5em; text-align: left; line-height: 1.45; }
  .fig-row { display: flex; gap: 10px; flex-wrap: wrap; }
  .fig-row > * { flex: 1 1 260px; min-width: 0; }
  .fig-row.portrait > video { flex: 1 1 200px; max-width: 49%; }
  .abstract { border-left: 3px solid #8fbf5a; padding: 0.4em 1em; background: rgba(143,191,90,0.07); font-size: 0.95em; }
</style>

<p class="abstract">
<b>Abstract.</b> Last-mile delivery in dense cities requires robots that can travel on sidewalks shared with pedestrians, cyclists and parked vehicles, through environments that are unstructured, changing and governed largely by implicit social rules. At Freedom X we develop the autonomy stack for wheeled quadruped delivery robots, and in November 2026 our team launched the first robot-dog deliveries in Almaty. This page describes the work in three stages. First, a hierarchy of reinforcement-learning policies for locomotion, goal-directed navigation and obstacle avoidance, trained entirely in simulation and transferred to the real robot. Second, the limits of purely reactive policies in urban scenes, and the photorealistic closed-loop simulation we are building to go beyond them. Third, our study of video world foundation models as tools for data generation, scene understanding and data quality control. Together these form the path toward our goal: <b>a reasoning-based vision-language-action (VLA) policy for autonomous sidewalk navigation</b>.
</p>

<figure class="fig">
  <img src="{{ '/images/delivery/robot_platform.jpg' | relative_url }}" alt="Wheeled quadruped delivery robot in simulation">
  <figcaption><b>Figure 1.</b> The delivery platform: a wheeled quadruped carrying a delivery compartment. Wheels give efficient motion on flat pavement, and legs let the robot handle curbs, ramps and uneven ground.</figcaption>
</figure>

## 1. Introduction

Autonomous driving has moved from modular pipelines toward end-to-end models that perceive, reason and act within a single network. Sidewalk robots face a harder version of the same problem. They share space directly with people, follow no lane markings, and must decide continuously whether to slow down, yield, pass, or step onto another surface. A purely geometric navigation stack can avoid obstacles, but it cannot tell a pedestrian who is about to step aside from one who is not, or recognize that a parked car's door is about to open.

Our approach is incremental. We first built a robust *reactive* autonomy layer that can be trained at scale in simulation and deployed safely on hardware. On top of it we are now developing a *deliberative* layer: a policy that understands the scene semantically and explains its decisions. The sections below follow that progression.

## 2. Learned Locomotion and Navigation

### 2.1 A hierarchical curriculum

The control stack is a hierarchy of policies trained with reinforcement learning (PPO) in GPU-parallel simulation, with 4,096 to 8,192 robots learning simultaneously. Each level is trained, frozen, and then used as the action space of the next:

1. **Locomotion:** full-body control of legs and wheels from velocity commands, first on flat ground and then on rough terrain with slopes, steps and stairs.
2. **Goal-directed navigation:** a policy that outputs velocity commands to reach goal poses, first in empty worlds and then among static obstacles.
3. **Obstacle avoidance and urban navigation:** navigation in procedurally generated urban scenes with dense clutter and moving obstacles, using onboard perception.

<figure class="fig">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/training_curriculum.mp4' | relative_url }}" type="video/mp4">
  </video>
  <figcaption><b>Figure 2.</b> The training curriculum: massively parallel locomotion learning, rough-terrain traversal, goal reaching (arrows show the commanded and achieved motion), obstacle fields, and finally urban scenes.</figcaption>
</figure>

<figure class="fig">
  <div class="fig-row">
  <img src="{{ '/images/delivery/urban_training_tiles.jpg' | relative_url }}" alt="Urban training tiles">
  <img src="{{ '/images/delivery/urban_training_obstacles.jpg' | relative_url }}" alt="Urban training tiles with obstacles">
</div>
  <figcaption><b>Figure 3.</b> Urban training worlds. Left: parallel urban terrain tiles built from city-block geometry. Right: the same tiles with randomized static obstacles, re-sampled every episode so the policy cannot memorize layouts.</figcaption>
</figure>

### 2.2 Perception and the learned safety shield

Navigation runs on two complementary representations of the environment. A GPU **elevation map** built from LiDAR captures traversability (curbs, steps, ramps) for terrain-aware planning. A 360° **ray observation** of 180 bearings within 3 m feeds a dedicated safety layer.

The **safety shield** is a recurrent (LSTM) policy that sits between the navigation command and the locomotion controller at 50 Hz. It passes safe commands through unchanged and minimally corrects unsafe ones. Training in simulation exposed the shield to ideal ray observations. On the real robot, a separately trained **ray predictor network** converts raw LiDAR point clouds into the same representation, which closes the gap between simulated and real perception. In closed-loop simulation with static clutter, the shield reduces collisions by **93%** compared with the same robot driven without it.

<figure class="fig">
  <img src="{{ '/images/delivery/perception_elevation_rays.jpg' | relative_url }}" alt="Elevation map and safety rays">
  <figcaption><b>Figure 4.</b> Onboard perception on the robot: the LiDAR elevation map (color = height) and the safety shield's 360° ray observation (magenta ring), computed in real time.</figcaption>
</figure>

A practical sim-to-real problem was high-frequency oscillation in the shield's corrections on hardware, caused by sensor noise that the simulator did not reproduce. We solved it by passing only the shield's *correction* (not the user command) through a critically damped second-order low-pass filter, with per-axis cutoffs selected by replaying recorded robot data offline.

<figure class="fig">
  <img src="{{ '/images/delivery/shield_command_filter.jpg' | relative_url }}" alt="Shield command filtering analysis">
  <figcaption><b>Figure 5.</b> Offline replay of a real-robot recording. Raw shield outputs (yellow) against filtered commands (blue) for forward, lateral and yaw velocity, with the resulting correction magnitude (red). The filter removes high-frequency jitter while keeping fast reactions to real obstacles.</figcaption>
</figure>

### 2.3 Real-world deployment

The policies run onboard the robot as exported neural networks. Every change is validated in a high-fidelity digital twin before it reaches hardware.

<figure class="fig">
  <div class="fig-row portrait">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/real_outdoor_safety_shield.mp4' | relative_url }}" type="video/mp4">
  </video>
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/real_indoor_navigation.mp4' | relative_url }}" type="video/mp4">
  </video>
</div>
  <figcaption><b>Figure 6.</b> Sim-to-real results. Left: the learned safety shield outdoors, on paving, grass and curbs. Right: terrain-aware navigation with the shield indoors, reacting to static obstacles and to people stepping into its path. Faces are blurred.</figcaption>
</figure>

These components now support the robot dogs in real deliveries in Almaty.

## 3. Beyond Reactive Control: A Photorealistic Closed-Loop Simulator

The policies above act on geometry. They know *where* free space is, but not *what* surrounds the robot. Better sidewalk behavior needs semantic understanding: a person waiting to cross, a scooter lying on the pavement, the right door to wait at. Learning this requires visual training data at scale, and rigorous evaluation requires **closed-loop** testing, where the policy's own actions change what it sees next.

We are therefore building a simulator around three ideas:

- **Diverse urban scenes.** A library of photorealistic sidewalk environments with varied architecture, street furniture, vehicles and vegetation, so that policies generalize beyond a single city.
- **Multi-modal ground truth.** Every rendered frame comes with depth, semantic segmentation and surface normals, giving direct supervision for perception.
- **Reconstruction of real streets.** Recordings from the robot's own camera are reconstructed as neural 3D scenes in which the real pedestrians and vehicles become separate, replayable agents. A policy can then be evaluated against what the robot would actually see on its route.

<figure class="fig">
  <div class="fig-row">
  <img src="{{ '/images/delivery/scene_japan_overview.jpg' | relative_url }}" alt="Urban scene">
  <img src="{{ '/images/delivery/scene_korea_overview.jpg' | relative_url }}" alt="Urban scene">
  <img src="{{ '/images/delivery/scene_overview_china.jpg' | relative_url }}" alt="Urban scene">
</div>
  <div class="fig-row" style="margin-top:10px">
  <img src="{{ '/images/delivery/scene_japan_1.jpg' | relative_url }}" alt="Robot-eye view">
  <img src="{{ '/images/delivery/scene_custom_2.jpg' | relative_url }}" alt="Robot-eye view">
  <img src="{{ '/images/delivery/scene_china_1.jpg' | relative_url }}" alt="Robot-eye view">
</div>
  <figcaption><b>Figure 7.</b> Urban scene diversity. Top: overviews of simulated city blocks. Bottom: views from the robot's camera height.</figcaption>
</figure>

<figure class="fig">
  <img src="{{ '/images/delivery/sim_modalities.jpg' | relative_url }}" alt="RGB, depth and segmentation outputs">
  <figcaption><b>Figure 8.</b> Multi-modal outputs per frame: RGB, depth, semantic segmentation and normals.</figcaption>
</figure>

<figure class="fig">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/urban_sim_navigation.mp4' | relative_url }}" type="video/mp4">
  </video>
  <figcaption><b>Figure 9.</b> Closed-loop navigation of the delivery robot through photorealistic urban scenes, with the planned trajectory (green) and the robot's internal view (3× speed).</figcaption>
</figure>

<figure class="fig">
  <img src="{{ '/images/delivery/neural_reconstruction.jpg' | relative_url }}" alt="Neural reconstruction of a real street">
  <figcaption><b>Figure 10.</b> Early result: our delivery yard, reconstructed as a neural 3D scene from a single camera recording. Artifacts remain in areas the camera barely observed. Improving reconstruction coverage is ongoing work.</figcaption>
</figure>

## 4. World Foundation Models for Sidewalk Autonomy

Video world foundation models are trained on large amounts of real-world video. They can generate physically plausible futures, re-render a scene under new conditions, and answer questions about video with explicit reasoning. We evaluated one such model on **recordings from our own delivery robot's front camera** to see how it could support each part of the VLA pipeline: data, edge cases, understanding, and quality control. All recordings were anonymized before processing.

### 4.1 Scaling real data across conditions

From a single real ride, the model generates the same trajectory under new weather and lighting, while the scene's structure and the robot's motion stay fixed through edge-based control. One recording becomes many training examples, including conditions such as snow and darkness that are expensive to wait for and record.

<figure class="fig">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_transfer_conditions.mp4' | relative_url }}" type="video/mp4">
  </video>
  <figcaption><b>Figure 11.</b> Condition transfer. Top left: a real ride re-rendered from its own structure (fidelity check). The other panels are generated variants: fresh snow, rainy dusk with street lights, the delivery depot at night under floodlights, and a winter evening at a delivery address.</figcaption>
</figure>

### 4.2 Generating safety-critical edge cases

The rarest events are often the most dangerous, and they cannot be staged safely with a real robot. Conditioned on the last frames of a real recording, the model imagines how the scene could continue. In the example below, recorded at our delivery depot, a courier steps out from behind a parked van carrying a crate and walks directly into the robot's path. This occlusion-driven hazard appears suddenly, leaves little time to react, and is exactly the kind of event a sidewalk robot must anticipate.

<figure class="fig">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_predict_courier.mp4' | relative_url }}" type="video/mp4">
  </video>
  <figcaption><b>Figure 12.</b> A generated future from a real moment at the delivery depot: a courier emerges from behind a van into the robot's path. The model keeps the scene, the lighting and the parked vehicles consistent while introducing a plausible new agent. Faces are blurred.</figcaption>
</figure>

The same approach produces other urban hazards: a car door swinging open into the sidewalk, or a cyclist riding fast toward the robot on a narrow path.

<figure class="fig">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_predict_edge_cases.mp4' | relative_url }}" type="video/mp4">
  </video>
  <figcaption><b>Figure 13.</b> Generated futures from real moments: a parked car's door opens into the robot's path (left), and an oncoming cyclist on a narrow sidewalk (right). Faces and licence plates are blurred.</figcaption>
</figure>

### 4.3 Reasoning about the scene and the next action

Asked to act as the navigation module of a small delivery robot, the model describes the scene, identifies hazards, and selects the next maneuver with an explicit chain of reasoning. This is the behavior we want the final policy to have.

<figure class="fig">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_reason_next_action.mp4' | relative_url }}" type="video/mp4">
  </video>
  <figcaption><b>Figure 14.</b> Next-action reasoning. Two pedestrians approach on a narrow sidewalk. Of four options, the model chooses to <i>slow down and keep to the right edge, stopping if needed</i>, and rejects leaving the sidewalk because of the nearby pedestrians.</figcaption>
</figure>

<figure class="fig">
  <div class="fig-row">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_reason_narrow_sidewalk.mp4' | relative_url }}" type="video/mp4">
  </video>
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_reason_hazard.mp4' | relative_url }}" type="video/mp4">
  </video>
</div>
  <figcaption><b>Figure 15.</b> Left: free-space reasoning around a parked SUV that blocks part of the sidewalk. Right: hazard identification, where the model spots a scooter lying on the road.</figcaption>
</figure>

The model can also **ground** its understanding spatially. It returns bounding boxes for pedestrians and vehicles and makes task-level decisions, such as which building entrance a delivery robot should wait at.

<figure class="fig">
  <div class="fig-row">
  <img src="{{ '/images/delivery/wfm_grounding_people.jpg' | relative_url }}" alt="Grounding pedestrians and vehicles">
  <img src="{{ '/images/delivery/wfm_grounding_free_space.jpg' | relative_url }}" alt="Grounding vehicles and free space">
  <img src="{{ '/images/delivery/wfm_grounding_door.jpg' | relative_url }}" alt="Grounding entrance doors">
</div>
  <figcaption><b>Figure 16.</b> Spatial grounding: pedestrians and parked vehicles on a sidewalk (left), vehicles and drivable free space at the delivery depot (center), and the choice of entrance door at a delivery address (right). Boxes are drawn exactly as the model returned them.</figcaption>
</figure>

### 4.4 Automatic quality control of synthetic data

Generated data is only useful if it is physically plausible. We used the model's reasoning ability to judge its own generated videos. **Every video it rejected was also rejected or flagged in our manual review**: a car that never moves while the vans around it change shape, a scooter sliding without cause, and the robot appearing in its own camera view. Reasoning can therefore pre-screen synthetic data before it enters training.

<figure class="fig">
  <img src="{{ '/images/delivery/wfm_quality_filter.jpg' | relative_url }}" alt="Quality filter summary">
  <figcaption><b>Figure 17.</b> Plausibility verdicts for nine generated scenarios compared with our manual review.</figcaption>
</figure>

<figure class="fig">
  <div class="fig-row">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_qc_accepted_courier.mp4' | relative_url }}" type="video/mp4">
  </video>
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_qc_rejected.mp4' | relative_url }}" type="video/mp4">
  </video>
</div>
  <figcaption><b>Figure 18.</b> Left: an accepted generation. The model identifies the courier walking into the robot's path as the main hazard and confirms that stopping is the right reaction. Right: a rejected generation, where a scooter moves with no visible cause, violating object permanence.</figcaption>
</figure>

### 4.5 Limitations

The model's weakest skill is judging the robot's **own** behavior. In one case it stated that the robot stayed on the sidewalk and gave the route a perfect score, while the robot was in fact driving on the roadway. In another it rated a very close pass with a pedestrian 4 out of 5. These failures show that general-purpose video reasoning is not yet reliable enough for safety-critical self-assessment, and they motivate post-training on domain-specific, robot-centric data.

<figure class="fig">
  <div class="fig-row">
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_limit_route.mp4' | relative_url }}" type="video/mp4">
  </video>
  <video autoplay loop muted playsinline controls preload="metadata">
    <source src="{{ '/videos/delivery/wfm_limit_close_pass.mp4' | relative_url }}" type="video/mp4">
  </video>
</div>
  <figcaption><b>Figure 19.</b> Failure cases in self-assessment: misjudging the driving surface (left) and underestimating the risk of a close pass (right).</figcaption>
</figure>

## 5. Toward a Reasoning VLA Policy

The pieces above fit into one pipeline:

- **Data.** Real robot recordings, multiplied across conditions by condition transfer and enriched with generated edge cases, then filtered automatically for physical plausibility.
- **Supervision.** Scene descriptions, spatial grounding and reasoning traces provide language-level labels alongside the robot's actions, so the policy learns *why* an action is chosen, not only *what* it is.
- **Evaluation.** Closed-loop testing in photorealistic and reconstructed scenes, where the policy's decisions change what it observes next.
- **Safety.** The learned safety shield and locomotion stack stay underneath the VLA policy as a verified low-level layer, so high-level reasoning never acts on the robot directly without a reactive safeguard.

Our next steps are to scale real-world data collection from the delivery fleet, to post-train the reasoning model on robot-centric sidewalk data so that it handles exactly the failure cases above, and to train and evaluate the VLA policy in closed loop before deploying it on the robots.

## 6. Conclusion

We have built and deployed a learned autonomy stack that lets wheeled quadruped robots perform real deliveries in Almaty, trained entirely in simulation and transferred to hardware. The next frontier is reasoning: robots that understand urban sidewalks the way people do and can explain their decisions. Photorealistic closed-loop simulation and world foundation models are giving us the data, the supervision and the evaluation tools to get there.
