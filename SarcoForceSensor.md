---
layout: default
title: Sarcomere Dynamics Magnetic Force Sensor
permalink: /SarcoSensor/
---

# Fingertip Magnetic Force Sensor
# Metal Mario Autonomous Robot Car

## Project Overview
<div style="text-align: center; margin-bottom: 20px;">
  <img src="docs/assets/MarioKart.png" alt="Metal Mario" style="width: 400px; border-radius: 10px; margin-bottom: 10px;">
</div>


Working recently at Sarcomere Dynamics, I was tasked with developing a **Fingertip Force Sensor**. The setup was a small permanent magnet being placed in a malleable rubber casing above a tri-axis Magnetic Field sensor (MLX90393). As the rubber was compressed, the magnet moved and shifted orientation resulting in a different Magnetic Field output. We required an accurate reading of the normal force being applied and needed to identify the direction of shearing, which we were unable to get.


---

## Key Features
- Data Collection/Repeatability
- Normal Force Mapping
- Shear Direction Mapping
- Calibration Scheme

---

## Skills Applied

| **Category**    | **Skills**                                                                 |
|------------------|---------------------------------------------------------------------------|
| **Mathematics**  | Linear Algebra, Pseudoinverse Matrices                            |
| **Software**     | Python, Embedded Systems (PlatformIO), Real-Time Data Acquisition, Sensor Firmware |

---

## Configuring Data Repeatability
My first steps were to ensure sensor output repeatability both in the Normal and Shear Directions. 

This involved collecting raw Magnetic field data in all three directions at:
- different applied forces (systematically increasing) 
- in 4 directions (+x,-x,+y,-y) and simply normal 
- essentially established different “states”  (ie 4N force in +x direction)

I followed this by ensuring running a clustering K-Means algorithm to see if the collected data really emerged as consistent different states.

---
## Normal Force Mapping

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/Normal Force Mapping1.png' | relative_url }}" alt="Normal Mapping 1" style="width: 500px; border-radius: 10px;">
</div>

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/Normal Force Mapping2.png' | relative_url }}" alt="Normal Mapping 2" style="width: 500px; border-radius: 10px;">
</div>


---
## Shear Force Mapping


<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/Shear Mapping.png' | relative_url }}" alt="Shear Mapping" style="width: 500px; border-radius: 10px;">
</div>

---

## Challenges Faced

---

## Lessons Learned

---
