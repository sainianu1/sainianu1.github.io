---
layout: project
title: Arlo Power-ORing Switch
heading: Power-ORing Switch
permalink: /ArloCamera/
cover: /docs/assets/USB_PowerCircuitry.png
eyebrow: Arlo Technologies · Hardware Engineering Intern
role: Hardware Engineering Intern · Arlo Technologies
timeline: May 2025 — Dec 2025 · Vancouver, BC
summary: Cost-effective Power-ORing switch with integrated firmware and auxiliary hardware control — 98% efficient charging from the best available source for Arlo’s solar-capable camera.
tags:
  - Power-ORing
  - MOSFET
  - Firmware + HW
  - HV Input
metrics:
  - value: "98%"
    label: "Power-ORing efficiency"
  - value: "FW + HW"
    label: "Integrated control"
  - value: "Discrete HV"
    label: "Transistor / diode array"
---

<p class="section-label">Context</p>
## The problem

Arlo’s camera needed to charge from the **best available power source** among USB-C, external supply, and an embedded solar path — without expensive integrated ideal-diode controllers, and without back-feeding or inefficient handoffs between rails.

<p class="section-label">Impact</p>
## What I delivered

<div class="callout">
  Designed a cost-effective <strong>Power-ORing Switch</strong> (integrated FW + auxiliary HW control) with <strong>98% efficiency</strong> to charge Arlo’s camera from the best available power source; applied transistor/diode array logic to create a discrete HV input system.
</div>

- Selected a discrete MOSFET / diode-array approach instead of a costly integrated power-mux, keeping the BOM lean while meeting efficiency targets
- Combined **firmware selection** of the preferred input with **auxiliary hardware control** for safe defaults and dead-battery recovery paths
- Validated switching behavior and charging efficiency across the multi-input architecture used on the solar-capable camera program

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/USB_PowerCircuitry.png' | relative_url }}" alt="Power-ORing and multi-source switching circuitry">
    <figcaption>Power-ORing / multi-source switch</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/EmbedSPCircuitry.png' | relative_url }}" alt="Embedded solar panel power path">
    <figcaption>Embedded solar path context</figcaption>
  </figure>
</div>

<p class="section-label">Design</p>
## How the Power-ORing works

### Control split
- **Hardware-controlled paths** handle plug-in and dead-battery corner cases so the pack can always recover
- **Firmware** chooses the higher / preferred input when multiple sources are present

### Operating modes
- **Default (dead battery):** USB‑C switch (Q1+Q2) ON and embedded SP switch (Q4+Q5) ON — hardware controlled
- **USB‑C present:** USB‑C path ON, embedded SP path OFF — hardware controlled on plug-in
- **Best-source selection:** firmware picks between USB‑C and embedded solar when both are available

### Discrete HV input
Used transistor/diode array logic to build a **discrete high-voltage input system** that ORs sources safely — prioritizing efficiency, reverse-current blocking, and cost over an integrated ideal-diode IC.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/USB_PowerADCProtection.png' | relative_url }}" alt="GPIO and ADC protection around the power path">
    <figcaption>Protection around the power / sense path</figcaption>
  </figure>
</div>

<p class="section-label">Also on this internship</p>
## Broader Arlo impact (resume-level wins)

These are called out on the resume; the Power-ORing switch above is the featured deep dive.

- **Led R&D** for a new solar-powered security camera — power architecture, competitive benchmarking, and battery/power validation
- Root-caused Wi-Fi / motion-sensor interference, cutting related **yield loss from 30% to under 1%**
- Grew key sensor hardware test coverage **from 60% to 100%** for wireless coexistence

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Power | Power-ORing, MOSFET switching, diode-array logic, discrete HV input |
| Control | Firmware source selection + auxiliary hardware fail-safes |
| Validation | Efficiency measurement, multi-source charge-path bring-up, LTSpice |
| Debug | RF coexistence / PIR yield root-cause |
