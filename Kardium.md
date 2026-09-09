---
layout: project
title: Kardium — Medical-Grade PCB Design & Validation
heading: Medical-Grade PCB Design
permalink: /Kardium/
cover: /docs/assets/Kardium3D_Top.png
eyebrow: Kardium Inc. · Electronics Hardware Intern
role: Electronics Hardware Intern · Kardium Inc.
timeline: Jan 2026 — Aug 2026 · Burnaby, BC
summary: Designed the 2nd generation of Kardium’s highest-volume 6-layer production PCB — HV RF/PF ablation plus LV sense/drive, DFM vendor transition, 16HV + 16LV across 8 channels and flash under IPC Class 3 — and owned a matched-impedance 4-layer flash/SPI test jig from component selection through bring-up.
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
    label: "End-to-end flash/SPI test jig"
---

<p class="section-label">Context</p>
## The problem

Kardium’s catheter handle board sits between the multi-use **RF/PF ablation generators** and disposable **electrode capsules**. It has to carry high-voltage ablation energy and low-voltage sense/drive safely, survive medical HV compliance, stay manufacturable at high volume under **IPC Class 3**, and fit an extreme mechanical envelope — then prove out on the bench before production.

At Kardium I designed the **2nd generation of their highest-volume production PCB**: a **6-layer** board carrying high-voltage **RF/PF ablation** signals plus low-voltage sense/drive paths for **resistance and temperature**. I owned the **vendor transition for DFM**, then laid out the full board under extreme size constraints. I also took a companion **4-layer flash/SPI test jig** from component selection, schematic capture, and layout through bare-board bring-up and functional verification.

<figure>
  <img src="{{ '/docs/assets/KardiumHandleBoardGen2_Top.png' | relative_url }}" alt="Top-side CAD view of the Cronus Handle Board Gen 2">
  <figcaption>Cronus Handle Board Gen 2 — top-side CAD view</figcaption>
</figure>

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
- Owned a companion **4-layer flash/SPI test jig end to end** — component selection, schematic, layout, bare-board bring-up, and functional verification — with an Arduino Nano Every, ADG3304, and a controlled-impedance pogo-pin interface
- Built the fixture to test the **handle PCB by itself** and to dock with the **fully assembled catheter system**, supporting both board-level development and final-assembly testing
- Also on the internship: next-gen **1500V+ medical flex**, a full **system-level RF Switch validation campaign** (see [that write-up]({{ '/KardiumTesting/' | relative_url }})), and multi-board debug in a **10+ board** system

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

### 4 · End-to-end ownership — 4-layer flash/SPI test jig
After the production layout, I developed a companion **4-layer flash/SPI test jig** so bring-up and communication tests would be representative of the real product. I owned the complete electrical design cycle:

- Selected the components and defined the electrical architecture
- Captured the **schematic** and completed the **4-layer PCB layout**
- Assembled and brought up the manufactured jig from a **bare-board state**, populating the pogo pins, ICs, and 0402 resistors and capacitors
- Verified that the completed fixture programmed and communicated with the handle board as intended

The fixture accommodates two test configurations: direct access to the **standalone handle PCB**, and insertion into the **fully assembled catheter system** for final-assembly testing.

#### Electrical design
The jig was more than a physical breakout:

- Routed the **SPI traces with controlled impedance** to match the production handle board and preserve representative signal integrity
- Used an **ADG3304** logic-level translator between the Arduino Nano Every and the flash I/O voltage domain
- Added **ESD protection diodes** at the external pogo-pin interface
- Implemented hardware **switch debouncing** for reliable operator input
- Added on-board **button and LED** control/status circuitry
- Matched the generator’s **pogo-pin interface** to the same gold-pad array on the handle board

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/KardiumTestJig_3D_Top.png' | relative_url }}" alt="Top-side Altium 3D view of the Kardium handle-board flash test jig">
    <figcaption>Top-side 3D view — Arduino host and pogo interface</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/KardiumTestJig_3D_Bottom.png' | relative_url }}" alt="Bottom-side Altium 3D view of the Kardium handle-board flash test jig">
    <figcaption>Bottom-side 3D view — operator interface circuitry</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/KardiumTestJig_Layout.png' | relative_url }}" alt="Altium PCB layout view of the four-layer Kardium handle-board flash test jig">
    <figcaption>4-layer PCB layout — SPI routing and board interfaces</figcaption>
  </figure>
</div>

Selected schematic pages show the protected pogo interface, bidirectional level translation, and controller/status circuitry:

<figure>
  <img src="{{ '/docs/assets/KardiumTestJig_Schematic_PogoESD.png' | relative_url }}" alt="Kardium test jig schematic showing the pogo-pin SPI interface and ESD protection">
  <figcaption>Pogo-pin SPI interface with ESD protection</figcaption>
</figure>

<figure>
  <img src="{{ '/docs/assets/KardiumTestJig_Schematic_LevelTranslator.png' | relative_url }}" alt="Kardium test jig schematic showing ADG3304 SPI logic-level translation">
  <figcaption>ADG3304 bidirectional SPI logic-level translation</figcaption>
</figure>

<figure>
  <img src="{{ '/docs/assets/KardiumTestJig_Schematic_Controller.png' | relative_url }}" alt="Kardium test jig schematic showing the Arduino controller, switch debounce, LEDs, and power circuitry">
  <figcaption>Arduino host, power, debounced switch, and status LEDs</figcaption>
</figure>

#### Assembly and bring-up
I then populated the manufactured bare PCB with the **pogo pins, ICs, and 0402 passives**, brought up each circuit block, and verified the complete programming and communication path before integrating the board into the fixture.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/KardiumTestJig_Controller.png' | relative_url }}" alt="Top side of the Kardium flash test jig with Arduino Nano Every and pogo-pin interface">
    <figcaption>Controller side — Arduino host and pogo-pin interface</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/KardiumTestJig_DUT.png' | relative_url }}" alt="Device-under-test side of the Kardium flash test jig PCB">
    <figcaption>DUT side — handle-board contact and operator control</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/KardiumTestJig_Fixture.png' | relative_url }}" alt="Completed Kardium test jig mounted in its mechanical fixture">
    <figcaption>Completed jig in the dual-configuration fixture</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/KardiumTestJig_Catheter.png' | relative_url }}" alt="Kardium test jig inserted into a fully assembled catheter handle">
    <figcaption>Fixture testing the handle board inside the assembled catheter</figcaption>
  </figure>
</div>

That closed the loop from component selection and PCB design through manufactured hardware, board bring-up, and representative testing at both the board and assembled-system levels.

<p class="section-label">Also on this internship</p>
## Broader Kardium impact

### Medical-grade flex
- Layout for next-generation **medical flex PCBs**
- Routed **1500V+ signals** within strict safety clearances
- Aimed at short-term cost reduction and rapid drop-in integration into the current production system

### System-level RF Switch validation
The OneBox RF Switch campaign is its own project: I owned **what to test, the plans, the bench work, the pass/fail, and the reports**. That framework is what later cards in the cage were tested against.

→ [System-Level RF Switch Validation]({{ '/KardiumTesting/' | relative_url }})

### AmPLink / PMIC programmer
USB production programmer for power boards — I2C PMIC images, analog board identity, and a hardware interlock so the rails stayed off until the right config was written.

→ [PMIC Programming System]({{ '/Amplink/' | relative_url }})

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
| Test hardware | Component selection, schematic, 4-layer layout, bare-board assembly/bring-up, controlled-impedance SPI, ESD protection, switch debouncing, Arduino Nano Every, ADG3304, dual-configuration fixture |
| Also | Medical flex (1500V+), RF Switch system validation, AmPLink PMIC programmer, multi-board SI debug |
