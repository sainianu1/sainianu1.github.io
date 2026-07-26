---
layout: project
title: Machine Learning Detective Robot
heading: ML Detective Robot
permalink: /MLrobot/
cover: /docs/assets/MLRobot.png
eyebrow: Personal / Course Project · ML + Robotics
role: Perception · ROS · simulation
timeline: UBC Engineering Physics
summary: ROS/Gazebo autonomous car that reads visual clues with a CNN — character recognition above 98% accuracy, wired into the robot through publisher/subscriber control.
tags:
  - CNN
  - ROS
  - OpenCV
  - Gazebo
metrics:
  - value: ">98%"
    label: "Character recognition"
  - value: "ROS"
    label: "Pub/sub robot bridge"
  - value: "Gazebo"
    label: "Full sim stack"
---

<p class="section-label">Context</p>
## The problem

Train an autonomous “detective” robot car in simulation that can **see clues, read characters, and act on rules** — not just follow a painted line. The stack had to connect a vision model to a live Gazebo robot through ROS.

<figure>
  <img src="{{ '/docs/assets/MLRobot.png' | relative_url }}" alt="Machine learning detective robot in simulation">
  <figcaption>Detective robot in the Gazebo environment</figcaption>
</figure>

<p class="section-label">System</p>
## What I built

- **CNN character recognition** trained and tuned to **>98% accuracy** for reading on-course clues
- **Computer vision pipeline** (OpenCV + TensorFlow) feeding decisions to the autonomy stack
- **ROS publisher/subscriber** interfaces so Gazebo sensor streams and AI outputs stayed synchronized
- **Rule-abiding autonomy** in sim: detect → classify → act, rather than open-loop motion

<div class="callout">
  <strong>Why recruiters care:</strong> this is the perception + systems glue — dataset realism, model accuracy, and a clean ROS bridge into robot control — not just a notebook model.
</div>

<p class="section-label">Hard parts</p>
## Challenges

- Collecting / synthesizing training data that matched what the robot actually saw in real time in Gazebo
- Keeping latency and topic timing sane so recognition results arrived while they were still actionable

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| ML | CNNs, TensorFlow, OpenCV |
| Robotics | ROS pub/sub, Gazebo simulation |
| Software | Python, Linux |
