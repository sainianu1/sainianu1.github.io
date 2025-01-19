---
layout: default
title: Sarcomere Dynamics Motor Control PCB
permalink: /SarcoPCB/
---

# Brushless DC Motor Control PCB


## Project Overview

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

I designed a **Brushless DC Motor Control PCB** on Altium Designer

---

## Key Features
- STM32F412 Microcontroller to control the motor driver via SPI
- communicating with a magnetometer for motor's linear positioning via I2C
- internal voltage regulation (with a Linear Voltage Regulator) to allow for single power input
- implemented CAN communication (via transceiver hardware) for hierarchical system communication between multiple Motor Control Circuits

---

## Skills Applied

| **Category**    | **Skills**                                                                 |
|------------------|---------------------------------------------------------------------------|
| **Design**       | Analog Circuit Design, Sensor Systems Design                            |
| **Software**     | C/C++, PID Control, Embedded Systems (PlatformIO), Real-Time Data Acquisition |
| **Electrical**   | Rotary Encoder Design, Noise Reduction Techniques, RC Filtering, Compartmentalization |

---

## Schematic
<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/Top Level.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/STM32.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>



---
## PCB


<div style="display: flex; justify-content: center; gap: 20px; margin-bottom: 20px;">
  <img src="{{ '/docs/assets/pcbFront.png' | relative_url }}" alt="Force Sensor 1" style="width: 300px; border-radius: 10px;">
  <img src="{{ '/docs/assets/pcbBack.png' | relative_url }}" alt="Force Sensor 2" style="width: 300px; border-radius: 10px;">
</div>

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/pcbBack2.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>



---

## Challenges Faced
- Minimizing noise interference in the circuit.
- Ensuring reliable recalibration for repeatable repositioning.

---
