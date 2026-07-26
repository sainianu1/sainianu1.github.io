---
layout: project
title: Fingertip Magnetic Force Sensor
heading: Fingertip Magnetic Force Sensor
permalink: /SarcoSensor/
cover: /docs/assets/force sensor4.png
eyebrow: Sarcomere Dynamics · Electrical Engineering Intern
role: Electrical Engineering Intern · Sarcomere Dynamics
timeline: Sep 2024 — Dec 2024 · Vancouver, BC
summary: In-house magnet-based fingertip force sensor — normal force and shear direction from a tri-axis magnetometer, more than 90% accurate and 5–10× cheaper than catalog alternatives.
tags:
  - MLX90393
  - Firmware
  - Python
  - Linear Algebra
metrics:
  - value: ">90%"
    label: "Force / shear accuracy"
  - value: "5–10×"
    label: "Cheaper than off-the-shelf"
  - value: "O(1)"
    label: "Matrix multiply at runtime"
---

<p class="section-label">Context</p>
## The problem

At Sarcomere Dynamics I owned firmware and signal mapping for a **fingertip force sensor**: a permanent magnet seated in a soft rubber tip above a tri-axis magnetic sensor (**MLX90393**). Compression moves and tilts the magnet, changing the field vector.

The product needed:

- Accurate **normal force**
- Reliable **shear direction** (+x / −x / +y / −y)
- Something cheap enough to scale — commercial force sensors were **5–10×** more expensive
- A runtime mapping light enough for embedded use

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/force sensor4.png' | relative_url }}" alt="Assembled fingertip force sensor">
    <figcaption>Sensor assembly</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/force sensor5.png' | relative_url }}" alt="Force sensor soft tip">
    <figcaption>Soft tip + magnet</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/force sensor3.png' | relative_url }}" alt="Force sensor internals">
    <figcaption>Sensing stack</figcaption>
  </figure>
</div>

<p class="section-label">Approach</p>
## What I built

### 1. Prove the data is repeatable
Collected raw Bx/By/Bz across systematically increasing forces and four shear directions (plus pure normal). Treated each condition as a state (e.g. 4 N in +x) and validated separability with **k-means clustering** before trusting any mapping.

### 2. Normal force
Mapped force from **z-magnitude** or **xyz-magnitude**. Both tracked applied load cleanly once repeatability was established.

### 3. Shear direction
Averaged the 2D (x, y) field vectors for each shear class, then used a **pseudoinverse** to learn a linear map from raw vectors → unit direction vectors. Runtime cost collapses to a single matrix multiply — ideal for firmware.

<div class="callout">
  <strong>Why this design won:</strong> &gt;90% accuracy on normal force and shear direction, computationally cheap on-device, and dramatically cheaper than buying a commercial fingertip force unit.
</div>

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/Normal Force Mapping1.png' | relative_url }}" alt="Normal force mapping plot 1">
    <figcaption>Normal force calibration</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/Normal Force Mapping2.png' | relative_url }}" alt="Normal force mapping plot 2">
    <figcaption>Normal force fit</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/Shear Mapping.png' | relative_url }}" alt="Shear direction mapping">
    <figcaption>Shear direction mapping</figcaption>
  </figure>
</div>

<p class="section-label">Stack</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Sensing | MLX90393 tri-axis magnetometer, magnet-in-elastomer fingertip |
| Math | Linear algebra, pseudoinverse mapping, k-means repeatability checks |
| Software | Python analysis, PlatformIO embedded firmware, real-time acquisition |
