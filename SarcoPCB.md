---
layout: default
title: Sarcomere Dynamics Motor Control PCB
permalink: /SarcoPCB/
---

# Motor Control PCB

## Project Overview

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

I designed a **Motor Control PCB** on Altium Designer to allow for the control of a DC Brushless motor based on input data from a Magnetometer.

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
| **Communication** | I2C, SPI, CAN Hardware                            |
| **Electrical**    | Multi-Layer PCB Design, Sensor Integration |

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
