---
layout: project
title: Metal Mario — Autonomous Robot Race Car
heading: Metal Mario
permalink: /MetalMario/
cover: /docs/assets/MarioKart.png
eyebrow: Personal / Course Project · Robotics & Controls
role: Embedded systems · sensor fusion · PID
timeline: UBC Engineering Physics
summary: Autonomous STM32 race car built from scratch — IMU + magnetometer orientation, custom rotary encoder localization (>85% accuracy), and PID path following that won fastest lap by 4 seconds.
tags:
  - STM32
  - PID
  - IMU
  - Analog Design
metrics:
  - value: "85%+"
    label: "Localization accuracy"
  - value: "4s faster"
    label: "Fastest lap margin"
  - value: "1.5 ft"
    label: "Ramp jump survived"
---

<p class="section-label">Context</p>
## The problem

Build an **autonomous robot car** that can blast a Mario Kart–style obstacle course: sense orientation and position in real time, stay on an optimal path through jumps and rough terrain, and do it faster than the field.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/MarioKart3.png' | relative_url }}" alt="Metal Mario robot car on course">
    <figcaption>On-course hardware</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/MarioKart.png' | relative_url }}" alt="Metal Mario chassis">
    <figcaption>Chassis + electronics</figcaption>
  </figure>
</div>

<p class="section-label">System</p>
## What I built

- **Orientation stack:** IMU (accel + gyro) fused with a magnetometer for real-time heading
- **Custom rotary encoder:** counted wheel rotations to continuously estimate global position on the track map
- **STM32 integration:** all sensors + control loops on one embedded target (PlatformIO / C/C++)
- **PID path follower:** optimal path programmed onto the MCU; PID kept the car on that trajectory using live pose
- **Recalibration:** multi-sensor re-lock after jumps and obstacle hits so pose errors didn’t compound
- **Mechanical robustness:** chassis survived a **1.5 ft** ramp jump onto a rocky surface

<div class="callout">
  <strong>Outcome:</strong> real-time orientation + global location with <strong>&gt;85% accuracy</strong>, and autonomous navigation that delivered the <strong>fastest lap by 4 seconds</strong>.
</div>

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/MarioKart4.png' | relative_url }}" alt="Metal Mario electronics detail">
    <figcaption>Sensor / control electronics</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/MarioKart2.png' | relative_url }}" alt="Metal Mario close-up">
    <figcaption>Close-up assembly</figcaption>
  </figure>
</div>

<p class="section-label">Hard parts</p>
## Challenges & how I handled them

- **Noise:** RC filtering, compartmentalized grounding / layout discipline, and careful analog front-end choices around the encoder and IMU
- **Pose drift after jumps:** scheduled recalibration using redundant sensor cues instead of trusting a single dead-reckoning stream
- **Debug speed:** separated electrical, firmware, and software failure modes so bring-up stayed systematic

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Embedded | C/C++, STM32, PlatformIO, real-time acquisition |
| Controls | PID path following, recalibration state logic |
| Sensing | IMU + magnetometer, custom rotary encoder |
| Circuits | Analog design, RC filtering, noise reduction |
