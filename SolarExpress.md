---
layout: project
title: Solar Express — DC Power Optimizer
heading: Solar Express
permalink: /SolarExpress/
cover: /docs/assets/UASBuck.png
eyebrow: Personal Project · Power Electronics
role: Power architecture · controls · simulation
timeline: Personal project
summary: 600W panel-level DC-DC power optimizer — 4-switch buck-boost with GaN FETs, SPICE validation at 99%+ efficiency, and a Type-II compensator with strong stability margins.
tags:
  - Buck-Boost
  - GaN
  - SPICE
  - Controls
metrics:
  - value: "600W"
    label: "Panel-level optimizer"
  - value: "99%+"
    label: "Simulated efficiency"
  - value: "1.1s"
    label: "Rapid shutdown (under 1V)"
---

<p class="section-label">Context</p>
## The problem

Solar strings need panel-level power electronics that can track the best operating point, survive wide voltage ranges, and shut down safely. Solar Express is a **panel-level DC-DC power optimizer** designed around real PV-panel and string-inverter constraints.

<p class="section-label">Architecture</p>
## What I designed

- **600W** panel-level DC-DC optimizer
- **4-switch buck-boost** power stage with **100V GaN FETs at 250 kHz**
- Wide envelope: **10–80V** input / **5–80V** output at up to **15A**
- Full product-level power spec derived from panel and inverter constraints (not a textbook toy topology)

<div class="callout">
  Resume version stays high-level (600W, 99%+ efficiency, safety timing). This page is the engineer deep-dive.
</div>

<p class="section-label">Validation</p>
## Simulation & results

- Automated **NGSpice** switching simulations across a **24-point** Vin × Vout grid
- Achieved **99.5% pass-through** and **99.2% boost efficiency**
- Verified **NEC 690.12** rapid shutdown to **under 1V in 1.1s** (2s requirement)

<p class="section-label">Controls</p>
## Compensator design

- Small-signal plant identification on cycle-averaged SPICE models
- Characterized boost-mode **RHP zero at 3.9 kHz**
- Built a **Type-II compensator** with **≥94° phase margin**, **≥10 dB gain margin**, and **0.12%** step deviation

<p class="section-label">Optimization</p>
## Component selection

- Parametric loss-budget sweeps: RDS(on) 3–22 mΩ, fsw 100 kHz–1 MHz, L 3.3–22 µH
- Locked design point: **6.8 µH / 3.2 mΩ / 250 kHz**
- **Python + NGSpice** pipeline validated within **±0.5%** of an analytic loss model

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Power | 4-switch buck-boost, GaN FETs, MPPT-oriented optimizer spec |
| Simulation | NGSpice switching sims, loss-budget sweeps |
| Controls | Small-signal ID, Type-II compensation, RHP-zero awareness |
| Software | Python automation around SPICE |
