---
layout: default
title: Metal Mario
permalink: /MetalMario/
---

# Metal Mario Autonomous Robot Car

## Project Overview
<div style="text-align: center; margin-bottom: 20px;">
  <img src="docs/assets/MarioKart.png" alt="Metal Mario" style="width: 400px; border-radius: 10px; margin-bottom: 10px;">
</div>

An **autonomous robotic car** built from scratch to **speedily navigate** a Mario Kart-themed obstacle course.

---

## Key Features
- multi-sensor input
- a global location tracking scheme
- internal PID control

---

## Skills Applied

| **Category**    | **Skills**                                                                 |
|------------------|---------------------------------------------------------------------------|
| **Design**       | Analog Circuit Design, Sensor Systems Design                            |
| **Software**     | C/C++, PID Control, Embedded Systems (PlatformIO), Real-Time Data Acquisition |
| **Electrical**   | Rotary Encoder Design, Noise Reduction Techniques, RC Filtering, Compartmentalization |

---

## Project Workings
- Coupled an inertial measurement unit (accelerometer and gyroscope) with a magnetometer to obtain real-time directional orientation of the car. 

- Built a rotary encoder to count wheel spins in known directions, allowing continuous mapping of the car’s global location.

- Employed STM32 to integrate all sensors and circuitry. Developed a path following PID algorithm.

- Coded the optimal path onto the STM32 microprocessor, and utilizing the car’s global position on this preset map, applied PID  to ensure that the path was followed. 

- Developed robust recalibration procedures (using a variety of sensor data) to constantly reposition onto optimized path, especially after jumps and obstacle enounters

- Built a mechanically robust chassis which was capable of jumping off of a 1.5-foot ramp onto a rocky surface

<div style="text-align: center; margin: 20px 0;">
  <img src="docs/assets/MarioKart.png" alt="Mario" style="width: 500px; border-radius: 10px;">
</div>

---

## Challenges Faced
- Minimizing noise interference in the circuit.
- Ensuring reliable recalibration for repeatable repositioning.

---

## Lessons Learned
- **System integration:** Combining hardware and software to achieve precision results.
- **Error mitigation:** Identifying and reducing sources of error in real-world measurements.

---

## More Details

---

