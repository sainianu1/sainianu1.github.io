---
layout: project
title: Arlo Power-ORing Switch
heading: Power-ORing Switch
permalink: /ArloCamera/
cover: /docs/assets/USB_PowerCircuitry.png
eyebrow: Arlo Technologies · Hardware Engineering Intern
role: Hardware Engineering Intern · Arlo Technologies
timeline: May 2025 — Dec 2025 · Vancouver, BC
summary: Cost-effective Power-ORing switch with firmware and fallback hardware control so a solar-capable camera charges from the best of a power supply, external solar panel, or embedded solar path — MOSFET/diode analog control, validated in LTSpice and on the PCB at >98% efficiency.
tags:
  - Power-ORing
  - MOSFET
  - Firmware + HW
  - LTSpice
metrics:
  - value: ">98%"
    label: "Power-ORing efficiency"
  - value: "FW + HW"
    label: "Firmware + fallback hardware"
  - value: "Analog OR"
    label: "MOSFET / diode-array control"
---

<p class="section-label">Context</p>
## The problem

At Arlo I designed a cost-effective **Power-ORing switch** with integrated firmware and **fallback hardware control** so a solar-capable camera could charge from the **best available source** among a **power supply**, an **external solar panel**, and the **embedded solar path**. All of this without expensive integrated ideal-diode or power-mux ICs, and without back-feeding or inefficient rail handoffs.

<p class="section-label">Impact</p>
## What I delivered

<div class="callout">
  MOSFET and diode-array analog control, validated in <strong>LTSpice</strong> and on the actual PCB, at <strong>&gt;98% Power-ORing efficiency</strong>. Hardware handled plug-in and dead-battery recovery; firmware chose the preferred input when multiple sources were present.
</div>

- Implemented **smart MOSFET and diode-array logic** as an analog control system instead of a costly integrated power-mux or ideal-diode IC
- Combined **firmware** source selection with **fallback hardware control** for plug-in and dead-battery recovery
- Validated switching behavior and charging efficiency first in **LTSpice**, then on the **actual PCB**

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
- **Hardware-controlled paths** handle plug-in and dead-battery recovery so the pack can always come up
- **Firmware** chooses the preferred input when multiple sources are present

### Sources
- Power supply
- External solar panel
- Embedded solar path

### Discrete analog OR
Used MOSFET and diode-array logic to build an **analog control system** that ORs sources safely — prioritizing efficiency, reverse-current blocking, and cost over an integrated ideal-diode or power-mux IC.

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
| Power | Power-ORing, MOSFET + diode-array analog control, discrete source OR |
| Control | Firmware preferred-input selection + fallback hardware (plug-in / dead-battery) |
| Validation | LTSpice, then PCB bring-up; switching behavior and charging efficiency |
| Debug | RF coexistence / PIR yield root-cause |
