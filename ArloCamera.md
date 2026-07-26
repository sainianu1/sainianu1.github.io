---
layout: project
title: Arlo Solar Camera — Power Architecture & Hardware Validation
heading: Solar Camera Power & HW Validation
permalink: /ArloCamera/
cover: /docs/assets/USB_PowerCircuitry.png
eyebrow: Arlo Technologies · Hardware Engineering Intern
role: Hardware Engineering Intern · Arlo Technologies
timeline: May 2025 — Present · Vancouver, BC
summary: Led R&D for a new solar-powered security camera — power architecture, multi-source switching, RF coexistence debug, and hardware test coverage that moved yield and validation metrics in the right direction.
tags:
  - Power Architecture
  - MOSFET Switching
  - RF Debug
  - Validation
metrics:
  - value: "<1%"
    label: "PIR yield loss (from 30%)"
  - value: "100%"
    label: "ALS hardware test coverage"
  - value: "R&D lead"
    label: "Solar camera power system"
---

<p class="section-label">Context</p>
## The problem

Arlo was developing a new consumer security camera with an **embedded solar panel** alongside USB-C / external supply paths. The product needed a power architecture that could:

- Parallelize external power with the embedded solar panel without back-feeding the panel
- Charge the battery efficiently across dead-battery and normal operating corner cases
- Survive real RF environments (2.4 GHz Wi‑Fi) without breaking motion detection
- Be validated with enough hardware test coverage to catch coexistence issues early

<p class="section-label">Impact</p>
## Results that mattered

<div class="callout">
  <strong>PIR / RF coexistence:</strong> Investigated and eliminated PIR noise induced by 2.4 GHz Wi‑Fi radiation, cutting yield loss from <strong>30% to less than 1%</strong> and restoring reliable motion detection across idle, streaming, and recording states.
</div>

- **Led power-system R&D** for the solar camera: architecture definition, Boost / charger / fuel-gauge IC selection, competitive benchmarking, and voltage / power / battery charge–discharge validation.
- Expanded Ambient Light Sensor hardware test coverage from **70% → 100%** and built a coexistence test suite around it.
- Modified in-development hardware (separated PSUs on interconnected PCBs) to capture clean power-consumption and efficiency data across multiple ICs.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/USB_PowerCircuitry.png' | relative_url }}" alt="USB and solar power switching circuitry">
    <figcaption>Multi-source power switching</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/EmbedSPCircuitry.png' | relative_url }}" alt="Embedded solar panel power circuitry">
    <figcaption>Embedded solar panel path</figcaption>
  </figure>
</div>

<p class="section-label">Design</p>
## Power architecture

Built analog power-control circuitry for robust switching between multiple sources with minimal loss (validated in **LTSpice**), including:

- Parallelization of external adapter / external solar with the embedded solar panel
- Efficient battery charging with negligible reverse current into the embedded panel
- Hardware-controlled isolation of the embedded solar panel from the charging path when required

### Operating modes

- **Default (dead battery):** USB‑C switch (Q1+Q2) ON and embedded SP switch (Q4+Q5) ON — hardware controlled so a depleted pack can still recover.
- **USB‑C present:** USB‑C path ON, embedded SP path OFF — hardware controlled when USB‑C is plugged in.
- **Higher-input selection:** Firmware chooses the higher voltage between USB‑C and embedded solar when both are available.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/USB_PowerADCProtection.png' | relative_url }}" alt="GPIO and ADC protection circuitry">
    <figcaption>GPIO / ADC protection</figcaption>
  </figure>
</div>

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Power | Multi-input architecture, MOSFET switching, diode-ORing, battery charging |
| Debug | PIR / RF coexistence, Wi‑Fi aggressor analysis, yield root-cause |
| Validation | Voltage / power / charge–discharge sweeps, ALS coexistence suite, LTSpice |
| Product HW | PSU isolation mods for accurate IC efficiency measurement |
