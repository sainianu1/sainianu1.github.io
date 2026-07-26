---
layout: project
title: UBC UAS 60V → 5V Buck Converter
heading: 60V → 5V Buck Converter
permalink: /UasBuckConvertor/
cover: /docs/assets/UASBuck.png
eyebrow: UBC Uncrewed Aircraft Systems · Electrical
role: Electrical Engineer · UBC UAS
timeline: Team project · Altium + power electronics
summary: Central buck converter for UBC UAS aircraft power distribution — TPS54560-based Altium design stepping 60V down to a 5V / 5A rail.
tags:
  - Altium
  - Buck Converter
  - TPS54560
  - Power
metrics:
  - value: "60V → 5V"
    label: "Conversion"
  - value: "5A"
    label: "Output capability"
  - value: "TPS54560"
    label: "Regulator IC"
---

<p class="section-label">Context</p>
## The problem

UBC Uncrewed Aircraft Systems needed a **central power stage** that could take a high-voltage aircraft bus and deliver a clean **5 V / 5 A** rail for avionics and payloads. I redesigned that distribution step-down in Altium around a proven buck IC.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/UASBuck.png' | relative_url }}" alt="Assembled UAS buck converter board">
    <figcaption>Assembled buck stage</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/1Buck Circuit.png' | relative_url }}" alt="Buck converter PCB">
    <figcaption>PCB realization</figcaption>
  </figure>
</div>

<p class="section-label">Design</p>
## What I built

- **TPS54560DDA** — 60 V, 5 A step-down regulator with integrated high-side MOSFET
- Full schematic + PCB in **Altium**, sized for team manufacturing constraints
- Component selection biased toward **JLCPCB**-friendly, all-SMT parts with correct temp / current ratings

<figure>
  <img src="{{ '/docs/assets/1Buck Schematic.png' | relative_url }}" alt="Buck converter schematic">
  <figcaption>Buck schematic (TPS54560)</figcaption>
</figure>

<p class="section-label">Layout</p>
## PCB decisions that matter for bucks

- **Bootstrap capacitor** routed with the shortest practical trace to keep loop inductance down
- Surface-mount BOM for cost and assembly yield
- Operating-condition checks (temperature, current) enforced during part selection — not as an afterthought

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/1Buck Converter Circuit.png' | relative_url }}" alt="Buck converter circuit detail">
    <figcaption>Circuit detail</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/1Buck Converter Simulation.png' | relative_url }}" alt="Buck converter simulation">
    <figcaption>Simulation / validation view</figcaption>
  </figure>
</div>

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Power | Buck topology, 60 V input design, 5 V / 5 A rail |
| CAD | Altium schematic + PCB |
| DFM | SMT BOM, JLCPCB-oriented part choices, thermal / current derating |
