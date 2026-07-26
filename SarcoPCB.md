---
layout: project
title: BLDC Motor Control PCB
heading: BLDC Motor Control PCB
permalink: /SarcoPCB/
cover: /docs/assets/MotorControlPCB.png
eyebrow: Sarcomere Dynamics · Electrical Engineering Intern
role: Electrical Engineering Intern · Sarcomere Dynamics
timeline: Sep 2024 — Dec 2024 · Vancouver, BC
summary: Multi-layer Altium motor-control PCB for a BLDC actuator — STM32F412, SPI motor driver, I2C magnetometer positioning, and CAN for a multi-ECU robot arm.
tags:
  - Altium
  - STM32F412
  - BLDC
  - CAN
metrics:
  - value: "STM32"
    label: "F412 MCU + USB prog"
  - value: "SPI / I2C / CAN"
    label: "On-board buses"
  - value: "~0.75A"
    label: "Motor trace capacity"
---

<p class="section-label">Context</p>
## The problem

Sarcomere needed a compact **motor-control ECU** that could drive a Maxon / Faulhaber **BLDC** from magnetometer-based position feedback, regulate power from a single 5 V input, and talk to sibling boards on a robot arm over **CAN**.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="Assembled motor control PCB">
    <figcaption>Assembled motor control board</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/pcbFront.png' | relative_url }}" alt="PCB front render">
    <figcaption>Front layout</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/pcbBack.png' | relative_url }}" alt="PCB back render">
    <figcaption>Back layout</figcaption>
  </figure>
</div>

<p class="section-label">Architecture</p>
## What I designed

- **STM32F412** — multiple SPI / I2C / CAN peripherals plus USB for programming
- **Motor driver (SPI)** — drives the BLDC coils; phase outputs and Hall inputs placed at the board edge for clean enclosure wiring
- **3D magnetometer (I2C)** — angle / rotor-position sensing as a complement (or alternative) to Hall inputs, depending on motor orientation relative to the board
- **CAN transceiver** — hierarchical communication between multiple motor ECUs on the arm
- **Linear regulator** — 5 V board input → 3.3 V @ up to 0.5 A for the MCU and logic rail / power plane

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/Top Level.png' | relative_url }}" alt="Top-level schematic block">
    <figcaption>Top-level schematic</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/STM32.png' | relative_url }}" alt="STM32 schematic block">
    <figcaption>STM32 block</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/Driver_Schematic.png' | relative_url }}" alt="Motor driver schematic">
    <figcaption>Motor driver</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/Mag_Schematic.png' | relative_url }}" alt="Magnetometer schematic">
    <figcaption>Magnetometer</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/CAN_Schematic.png' | relative_url }}" alt="CAN transceiver schematic">
    <figcaption>CAN interface</figcaption>
  </figure>
</div>

<p class="section-label">Layout</p>
## PCB decisions

- Board sized for a tight mechanical enclosure; connectors clustered so wiring exits cleanly from one edge
- Motor phase traces ~**0.7 mm** (~0.75 A) with matched STM32→driver control lengths
- CAN Tx/Rx length-matched where practical; dense routing with deliberate workarounds on a small outline

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/TopLayer.png' | relative_url }}" alt="PCB top copper layer">
    <figcaption>Top copper</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/Bottom Layer.png' | relative_url }}" alt="PCB bottom copper layer">
    <figcaption>Bottom copper</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/pcbBack2.png' | relative_url }}" alt="Alternate PCB back view">
    <figcaption>Assembly / back detail</figcaption>
  </figure>
</div>

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| CAD | Altium Designer, multi-layer PCB |
| MCU / buses | STM32F412, SPI, I2C, CAN, USB DFU/programming |
| Power | On-board LDO, power-plane strategy |
| Motion | BLDC driver integration, Hall + magnetometer sensing |
