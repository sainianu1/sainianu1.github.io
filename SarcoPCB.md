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

choice of microcontroller
- due to communication reqs
- multiple SPI, I2C, and CAN for communication with external devices and sensors
- USB for programming of the stm32

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/Driver_Schematic.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

motor driver
- drove maxon/faulhaber bldc motor


<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/Mag_Schematic.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

magnetometer:
- opted for a 3d Magnetic sensor which was good for angle sensing
- complement to hall effect inputs: reduced wiring if wanted to use it singularly
- depending on the orientation of the motor to the board, we could get input signals for the motor rotor position from the sensor

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/CAN_Schematic.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

can communication:
- for coherent inter-communication between multiple ecu's on the robot arm
- allowed for scalability in design


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
## Layers

<div style="display: flex; justify-content: center; gap: 20px; margin-bottom: 20px;">
  <img src="{{ '/docs/assets/TopLayer.png' | relative_url }}" alt="Force Sensor 1" style="width: 300px; border-radius: 10px;">
  <img src="{{ '/docs/assets/Bottom Layer.png' | relative_url }}" alt="Force Sensor 2" style="width: 300px; border-radius: 10px;">
</div>


---

## PCB Choices and Why

incorporation of a linear regulation:
- allowed for 5V input into the board
- used lin reg to bring down 5V input to 3.3 w max 0.5A current draw
    - connected this to power plane and drew power for stm32 etc from that

placement of driver/stm32:
- components placed where they are mainly due to wiring constrains
- the entire PCB was to be inside an enclosing
- since i wanted minimal wiring coming out of the sides of the pcb  i placed the motor driver on the bottom
- where the driver’s a b c outputs into the coils could be wired easily out of the pcb
- also the hall inputs have been placed near the bottom where they can be wired in easily


trace widths:
- trace width for the motor outputs is around 0.7mm (good for about 0.75A)

routing:
- routing was pretty tight and done with some workarounds
- most traces were not too long because the pcb itself was quite small
- for the inputs from the stm32 to the driver, the traces were made to be of the same length
- also tried to make things like the can_Tx and can_Rx traces similar lengths



---
