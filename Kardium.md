---
layout: project
title: Kardium — Medical-Grade PCB Design & Validation
heading: Medical-Grade PCB Design
permalink: /Kardium/
cover: /docs/assets/Kardium3D_Top.png
eyebrow: Kardium Inc. · Electronics Hardware Intern
role: Electronics Hardware Intern · Kardium Inc.
timeline: Jan 2026 — Aug 2026 · Burnaby, BC
summary: Designed the 2nd generation of Kardium’s highest-volume 6-layer production PCB — HV RF/PF ablation plus LV sense/drive, DFM vendor transition, 16HV + 16LV across 8 channels and flash under IPC Class 3 — and a matched-impedance 4-layer flash/SPI test jig.
tags:
  - Medical PCB
  - HIPOT
  - IPC Class 3
  - Test Jig
metrics:
  - value: "6-layer"
    label: "Highest-volume production PCB"
  - value: "16HV + 16LV"
    label: "8 channels + flash, IPC Class 3"
  - value: "4-layer"
    label: "Matched-Z flash/SPI test jig"
---

<p class="section-label">Context</p>
## The problem

Kardium’s catheter handle board sits between the multi-use **RF/PF ablation generators** and disposable **electrode capsules**. It has to carry high-voltage ablation energy and low-voltage sense/drive safely, survive medical HV compliance, stay manufacturable at high volume under **IPC Class 3**, and fit an extreme mechanical envelope — then prove out on the bench before production.

At Kardium I designed the **2nd generation of their highest-volume production PCB**: a **6-layer** board carrying high-voltage **RF/PF ablation** signals plus low-voltage sense/drive paths for **resistance and temperature**. I owned the **vendor transition for DFM**, then laid out the full board under extreme size constraints, and designed a companion **4-layer flash/SPI test jig** so bring-up would be representative of the real product.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/Kardium3D_Top.png' | relative_url }}" alt="3D render of the Cronus Handle Board Gen 2, top side">
    <figcaption>Cronus Handle Board Gen 2 — top</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/Kardium3D_Bottom.png' | relative_url }}" alt="3D render of the Cronus Handle Board Gen 2, bottom side with Kardium silkscreen">
    <figcaption>Cronus Handle Board Gen 2 — bottom</figcaption>
  </figure>
</div>

<div class="callout">
  Resume bullets stay at impact (HIPOT strength, new vendor, cost). This page is the hardware-engineer walkthrough of how that board was shipped.
</div>

<p class="section-label">Impact</p>
## What a recruiter should know

- Designed the **2nd generation of Kardium’s highest-volume production PCB** — a **6-layer** board carrying **HV RF/PF ablation** plus **LV sense/drive** for resistance and temperature
- Owned the **vendor transition for DFM**: compared both fab houses’ capability and fabrication documents (spacings, clearances, expansions, hole tolerances), then laid out the full board under extreme size constraints
- Routed **16HV + 16LV signals each for 8 channels** as well as **flash**, holding **IPC Class 3** — increasing **HIPOT withstand** for medical HV safety compliance and cutting production cost on this safety-critical board
- Designed a companion **4-layer flash/SPI test jig** (Arduino Nano Every, ADG3304, pogo-pin interface) that preserved the same **controlled impedance** as the production board so bring-up and comms tests matched the real product
- Also on the internship: next-gen **1500V+ medical flex**, **100%** coverage validation on a **12-layer** board, and multi-board debug in a **10+ board** system

<p class="section-label">Deep dive</p>
## Highest-volume 6-layer handle PCB

### System role
The board is the interconnect inside one-time-use electrode capsules that mate to Kardium’s multi-use RF/PF ablation system:

- Routes **RF and pulsed-field (PF) ablation** signals from the generators to the RF/PF electrodes
- Returns **resistance and temperature sense** signals for closed-loop / monitoring paths
- Hosts a **flash memory** so each disposable capsule can carry identity / configuration data for the reusable generator stack
- Channel count: **16HV + 16LV signals each for 8 channels**, plus dedicated flash (SPI) — dense mixed-signal fanout under a hard size constraint

High-voltage ablation energy and low-voltage sense/drive share the same small board, so creepage/clearance, HIPOT strength, and layer assignment were first-class design drivers — not afterthoughts.

### 1 · Prework — vendor transition for DFM
Before touching the redesign layout, I owned the **vendor transition for DFM** (stackup was already approved). That meant comparing both **fab houses’ capability and fabrication documents** and locking every applicable rule into the CAD / fab package, including:

- Track-to-pad and related **spacings**
- Hole-to-hole and other **clearances**
- **NPTH solder-mask expansions** and mask openings
- **Hole-size tolerances** and related drill specs
- Broader fab drawing updates so the board stayed **IPC Class 3** while matching the new house’s process window

That prework is what made the vendor move a cost win instead of a quality risk: rules, drawings, and layout all pointed at the same manufacturable envelope.

### 2 · Layout — 6-layer mixed HV / LV under hard constraints
I then laid out the **entire 6-layer board**. Constraints that shaped the design:

- **No signal copper on top/bottom** — outer layers reserved (mechanical / contact / keep-out driven), so the ablation, sense, and flash nets had to be solved on the inner layers
- Extreme **physical sizing** from the capsule / handle mechanical envelope
- Coexistence of **high-voltage ablation** paths with **low-voltage sense and drive** on the same stackup, with HIPOT withstand strength as an explicit outcome of the 2nd-gen redesign
- Dense breakout for **16HV + 16LV signals each for 8 channels** plus flash, without violating Class 3 / vendor rules set in prework

<figure>
  <img src="{{ '/docs/assets/Kardium2D.png' | relative_url }}" alt="6-layer CAD layout of the Cronus handle PCB showing dense mixed-signal routing">
  <figcaption>6-layer CAD — mixed HV/LV inner-layer routing</figcaption>
</figure>

### 3 · Integration interfaces
Two mechanical-electrical interfaces define how the board sits in the product:

| Side | Connection | Role |
|------|------------|------|
| Generator / handle | **Pogo pins → exposed gold pads** | Multi-use RF/PF generators mate to the capsule board for powering ablation + sense + flash access |
| Electrode | **Solder-bond pads → ribbon cables** | Ablation and sense nets leave the board toward the RF/PF electrodes |

The flash device on the board is what makes the disposable capsule model work: many one-time capsules (board + electrode wiring) against one multi-use generator system, each capsule identifiable over SPI when docked on the pogo interface.

### 4 · Bring-up — 4-layer flash/SPI test jig
After the production layout, I designed a companion **4-layer flash/SPI test jig** so bring-up and communication tests would be representative of the real product:

- **Controlled-impedance SPI** path preserved to the same impedance as the production board
- **Arduino Nano Every** as the host controller
- **ADG3304** logic-level translator between MCU and flash I/O levels
- On-board **button + LEDs** for operator control and status
- **Pogo-pin interface** mating to the same gold-pad array used by the generators — so the jig plugs into the 6-layer board the same way the system does

That closed the loop: DFM vendor transition → production layout → system interfaces → a purpose-built fixture for flash bring-up and SPI confidence before capsules move with the ablation system.

<p class="section-label">Also on this internship</p>
## Broader Kardium impact

### Medical-grade flex
- Layout for next-generation **medical flex PCBs**
- Routed **1500V+ signals** within strict safety clearances
- Aimed at short-term cost reduction and rapid drop-in integration into the current production system

### 12-layer validation campaign
- End-to-end validation of a **12-layer medical-grade PCB**
- Authored and executed **25+ tests across 5 diagnostic suites**: Power, Signal Integrity, Thermal, ADC, Isolation
- **100% test coverage** across the planned suite
- Built custom **10× / 100× coaxial probes** for high-fidelity SI and isolation measurements

### Multi-board debug
- Debugged multiple **14-layer boards** inside a **10+ board system**
- Methods: high-speed signal analysis and precision rework

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| PCB prework | DFM vendor transition, fab capability/docs comparison, spacings / clearances / expansions / hole tolerances, IPC Class 3 |
| Production layout | 6-layer mixed HV/LV, 16HV + 16LV × 8 channels + flash, extreme size constraints |
| Integration | Pogo / gold-pad generator interface, solder-bond ribbon to electrodes, capsule flash |
| Test hardware | 4-layer flash jig, controlled-impedance SPI, Arduino Nano Every, ADG3304 |
| Also | Medical flex (1500V+), 12-layer validation suites, multi-board SI debug |
