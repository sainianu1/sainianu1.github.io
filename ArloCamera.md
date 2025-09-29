---
layout: default
title: Arlo Camera Power Circuitry Design
permalink: /ArloCamera/
---

# Arlo Camera Power Circuitry Design

## Project Overview


<div style="display: flex; justify-content: center; gap: 20px; margin-bottom: 20px;">
  <img src="{{ '/docs/assets/USB_PowerCircuitry.png' | relative_url }}" alt="Arlo 1" style="width: 500px; border-radius: 10px;">
  <img src="{{ '/docs/assets/USB_PowerADCProtection.png' | relative_url }}" alt="Arlo 2" style="width: 300px; border-radius: 10px;">
</div>




Designed Arlo’s brand-new consumer product: a security camera with an embedded solar panel. 

---

## Key Features
- Power Circuitry Design
- Power Supply Switching
- Hardware Design + Testing

---

## Skills Applied

| **Category**    | **Skills**                                                                 |
|------------------|---------------------------------------------------------------------------|
| **Hardware**  | Power Management, Power Supply Parallelization, Battery Charging                            |
| **EE**     | Switching Circuitry Design, MOSFETS, Diode-Oring |

---

## Key Steps
- undertook extensive power testing and competitive benchmarking to develop a simple, robust, and low-cost power system architecture, which allows for the parallelization of either an external power source (power adapter or external solar panels) with the embedded solar panel

- built analog power control circuitry for robust switching between multiple power sources for brand new camera system while incurring minimal losses (tested in LTSpice)

- ensured that the design provides efficient battery charging, negligible flow back current from external power sources into the embedded solar panel and includes augmented hardware control to isolate the embedded solar panel from the charging system 



---
## Embedded Solar Panel Power Circuitry Design

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/EmbedSPCircuitry.png' | relative_url }}" alt="Arlo 3" style="width: 500px; border-radius: 10px;">
</div>

---
## Operation Modes


- Default: USB_C switch (Q1+Q2) ON and Embed SP switch (Q4+Q5) ON for the corner case for charging dead battery. This is HW controlled.
- USB_C IN: Plug in “USB_C IN”, USB_C switch (Q1+Q2) ON and Embed SP switch (Q4+Q5) OFF. This is HW controlled.
- Higher Input Selection: Choosing higher voltage input between USB_C and Embed SP. This is FW controlled.

---

## GPIO Safety Circuitry


---
