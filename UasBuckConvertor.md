---
layout: default
title: UAS Buck Convertor
permalink: /UasBuckConvertor/
---

# UAS Buck Convertor: 60V -> 5V


## Project Overview

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/1Buck Circuit.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

I designed a **Buck Convertor** on Altium Designer to allow for the stepdown from 60V to 5V.

---

## Key Features
- implemented 

---

## Skills Applied

| **Category**    | **Skills**                                                                 |
|------------------|---------------------------------------------------------------------------|
| **Electrical**    | Multi-Layer PCB Design, Altium |

---

## Schematic
<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/1Buck Schematic.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

description
- for coherent inter-communication between multiple ecu's on the robot arm
- allowed for scalability in design


---
## PCB


<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/1Buck Circuit.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
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
