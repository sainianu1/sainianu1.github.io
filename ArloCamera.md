---
layout: project
title: Arlo Power-ORing Switch
heading: Power-ORing Switch
permalink: /ArloCamera/
cover: /docs/assets/arlo-power-oring-bringup.jpg
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
- Utilized **diode-ORing on PMOS gate inputs** to allow a shutdown signal to arrive from one of multiple sources for robust control
- Validated switching behavior and charging efficiency first in **LTSpice**, then on the **actual PCB**

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/arlo-power-oring-bringup.jpg' | relative_url }}" alt="Bench bring-up of the Power-ORing path: N6705B, labeled Solar and Battery meters, and proto boards on the ESD mat">
    <figcaption>PCB bring-up — USB-C / solar / battery rails on the bench</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/arlo-power-oring-bench.jpg' | relative_url }}" alt="Wider lab shot of the Power-ORing fixture with scope, power analyzer, and labeled Solar meter">
    <figcaption>Corner-case validation on the live fixture</figcaption>
  </figure>
</div>

<p class="section-label">Design</p>
## How the Power-ORing works

Two parallel power branches feed the charger IC:

- **USB-C** — a wall adapter or an **external solar panel**
- **Embedded solar** — the panel built onto the camera itself

Each branch reaches `VIN_CHG` through a **back-to-back PMOS** pair. That topology blocks the body-diode path, so current cannot sneak the wrong way through a single FET. Bidirectional blocking is what makes the OR safe: no reverse current into a weaker source, no back-feed into the battery, and real **power multiplexing** without an ideal-diode or mux IC.

The embedded panel is, by design, the weaker charger. Hardware has to treat a USB-C plug-in as a preemption, not a negotiation.

### Plug-in detect, in hardware
External solar is recognized the instant it lands on the connector: **15 kΩ on CC1/CC2**. A wall adapter is recognized the same way, from the manufacturer’s CC band. A dedicated control leg then **opens the embedded-solar PMOS path** as soon as USB-C voltage crosses a threshold — because the embed rail charges at a lower voltage, it must drop out the moment a stronger source is present.

Firmware can still disconnect **either or both** inputs from the charger, using the MPPT algorithm and measured input power. That is the preferred-source loop when the MCU is alive.

### Dead-battery and analog source select
The hardware contract was plug-ins and **dead-battery recovery**: the pack has to come up even if firmware is not running. I went further and made the analog front-end **choose the higher-power input by itself**, with no firmware, from the voltages sitting on the two source rails.

That only works if the control graph is right first — which node is allowed to shut which switch, and where each MOSFET’s gate, source, and drain actually sit. The gate map is the design. Once that was explicit, the FETs could be wired for clean handoff instead of fight-or-float.

Where several sources needed to pull a PMOS into cutoff, I **diode-ORed the gate inputs**. Those were logic-level shutdowns, not load current, so the diode drop did not show up as a power loss — it just guaranteed the gate could be held above threshold from more than one place.

<figure class="figure-diagram">
  <img src="{{ '/docs/assets/arlo-power-oring-ltspice.png' | relative_url }}" alt="LTSpice simulation of the front-end power-path: dual PMOS back-to-back switches from embedded solar and USB into VIN_CHG">
  <figcaption>LTSpice — both PMOS branches into VIN_CHG, with multi-source gate shutdown</figcaption>
</figure>

After the Spice model, I brought up the **actual PCB**, walked the same edge and corner cases the sim predicted, and shipped an application-specific alternative to a PMIC or power multiplexer.

<p class="section-label">Also on this internship</p>
## Broader Arlo impact (resume-level wins)

These are called out on the resume; the Power-ORing switch above is the featured deep dive.

**Led R&D** of a new solar-powered security camera with an embedded solar panel. This started with research on solar panels and testing the capabilities of Arlo’s existing solar tech. I also conducted competitive benchmarking by taking apart solar-embedded cameras designed by competitors, and building up their charging tree from the bare PCB.

With this research and other tests, I defined the **system architecture** — configuration of multiple power inputs, finding boost / charger / fuel-gauge ICs — as well as outlining the required firmware, including the **MPPT** algorithm.

I validated the design through comprehensive **voltage, power, efficiency, and battery charge/discharge cycle** testing.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/arlo-rd-outdoor-cart.jpg' | relative_url }}" alt="Outdoor solar-camera R&D: laptop on a cart next to a white utility cart with panels, cameras, and power stations">
    <figcaption>Outdoor validation — existing Arlo solar tech on the cart</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/arlo-rd-solar-rig.jpg' | relative_url }}" alt="Custom wooden solar-panel test rig on a white cart with multiple panels and Arlo cameras">
    <figcaption>Panel / camera test rig used for competitive and embed-solar work</figcaption>
  </figure>
</div>

<figure class="figure-diagram">
  <img src="{{ '/docs/assets/arlo-solana-block-diagram.png' | relative_url }}" alt="System diagram: external solar and wall adapter ORed at USB-C, embedded solar through a boost, both switched into VIN_CHG, charger, system, and 4-cell pack">
  <figcaption>System-level architecture from that R&amp;D — sources, switches, charger, and pack</figcaption>
</figure>

- Root-caused Wi-Fi / motion-sensor interference, cutting related **yield loss from 30% to under 1%**
- Grew key sensor hardware test coverage **from 60% to 100%** for wireless coexistence

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Power | Back-to-back PMOS Power-ORing, reverse-current block, discrete mux vs. PMIC |
| Control | CC plug-in detect, analog higher-source select, FW MPPT disconnect, dead-battery recovery |
| Analog | Diode-ORed PMOS gate shutdowns; gate / source / drain map before layout |
| Validation | LTSpice, then PCB bring-up across edge and corner cases |
| Debug | RF coexistence / PIR yield root-cause |
