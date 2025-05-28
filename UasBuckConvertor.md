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
- designed a Buck Convertor Circuit to meet the power needs of UBC UAS's drone 

---

## Skills Applied

| **Category**    | **Skills**                                                                 |
|------------------|---------------------------------------------------------------------------|
| **Electrical**    | Multi-Layer PCB Design, Altium, Buck Convertor |

---

## Schematic
<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/1Buck Schematic.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>

description
- used the TPS54560DDA IC (60V, 5A step down regulator with an integrated high side MOSFET)

---
## PCB


<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/1Buck Circuit.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>


---

## PCB Choices and Why

routing:
- routed bootstrap capacitor so that its trace was as short as possible for minimal inductance

general:
- maximized components from JLC PCB
- ensured operating conditions for components (ie temp, max current ratings)
- chose all surface mount components for cheaper pcb manufacturing

---
