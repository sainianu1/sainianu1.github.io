---
layout: project
title: Kardium — System-Level RF Switch Validation
heading: System-Level RF Switch Validation
permalink: /KardiumTesting/
cover: /docs/assets/rfs-thermal-system.jpg
eyebrow: Kardium Inc. · Electronics Hardware Intern
role: Electronics Hardware Intern · Kardium Inc.
timeline: 3-month campaign · 2026 · Burnaby, BC
summary: Owned the system-level validation campaign for Kardium’s OneBox RF Switch card — decided what to test, wrote the plans, ran the bench work, set pass/fail, and wrote the conclusions. The framework became the template for the rest of the 11+ board PCB ecosystem.
tags:
  - System Validation
  - Power Integrity
  - Signal Integrity
  - Relays
  - Thermal
metrics:
  - value: "17 tests"
    label: "Signed-off across 8 suites"
  - value: "11+ boards"
    label: "Same framework reused after"
  - value: "End-to-end"
    label: "Plan → bench → P/F → report"
---

<p class="section-label">Context</p>
## The problem

Kardium’s **OneBox RF Switch** sits in a **card-cage** with a system-on-module, backplane, and 24 V system power. It is the card that steers **RF driver / stim** paths through banks of **HV disconnect** and **switch/stim reed relays**, under firmware control from daisy-chained **shift registers** and **line buffers**. Isolated domains (**system, RFS, AUX**) share the same assembly. If a rail sags, a relay chatters, a shift-register clock glitches, or a monitor ADC lies, the rest of the ablation stack cannot trust the card.

Nobody handed me a finished protocol. Over a **three-month** campaign I decided what “healthy” meant at system level, wrote the plans, built the fixtures and rework, collected the data, set the pass/fail limits from datasheets and worst-case use, and wrote the conclusions — for **every** test.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/rfs-thermal-system.jpg' | relative_url }}" alt="FLIR thermal capture of the RF Switch in the card cage with rows of closed relays warming">
    <figcaption>Worst-case thermal — card cage, max relays closed</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/rfs-thermal-board.jpg' | relative_url }}" alt="FLIR close-up of the RF Switch PCB showing power and SOM hotspots">
    <figcaption>Board-level IR — supplies, SOM, closed relays</figcaption>
  </figure>
</div>

<div class="callout">
  The <a href="{{ '/Kardium/' | relative_url }}">layout / DFM page</a> is the production-PCB story. This page is the validation engineer walkthrough: how the RF Switch was proven on the bench, and why that method stuck.
</div>

<p class="section-label">Impact</p>
## What a recruiter should know

- **Owned the full loop** on the OneBox RF Switch: what to test, written plans, execution, data reduction, pass/fail requirements, and signed conclusions — not just “ran someone else’s script”
- Closed **17 tests across 8 suites**: Power, shift-register / buffer SI, HV+AUX relays, switch/stim relays, ADC diagnostics, magnetic coupling, system thermal, plus isolator SI/CMTI plans written into the same framework
- Exercised the card the way the product actually fails: **62 HV disconnects + 20 AUX + 45 switch/stim** closed together, rails measured from DC-DC output through chokes to the farthest coils
- Found real system behavior, not just green checkmarks — latching coil rails, load-switch auto-retry **disabled by design**, ADC accuracy vs. analog-rail voltage, clamped inductive kick on open-drain relay drive
- That structure — same sheet layout, probing notes, FW mapping, P/F table, and report — became the **fundamental test framework** for the rest of the **11+ board** PCB ecosystem; other cards have since been tested to the same parameters, the same way

<p class="section-label">Method</p>
## How a test was built

Every workbook followed the same contract so another engineer could pick it up:

| Step | What I did |
|------|------------|
| Decide | Map the failure mode (sag, brownout, bounce, coupling, heat) to the rail, IC, or relay that would show it |
| Plan | Goal, equipment, definitions, probing reference, required rework, FW/commands, procedure |
| Limits | Pass/fail from datasheets, converter capacitive-load ratings, pull-in/dropout vs. temperature, and worst-case current |
| Bench | Card cage + SOM, DMM / LCR / programmable load / programmable PS, 4-ch scopes, IR camera, ground-spring probing so “ringing” was the board’s, not the fixture’s |
| Conclude | Observations first, then explicit Pass / Fail / Tentative — including when the right answer was “this mode is not in the design” |

<p class="section-label">Deep dive</p>
## 1 · Power — five rails, worst-case load

Rails under test: **RFS +12 V, +5 V, +3.3 V, coil +5 V, AUX +5 V**, each with its own converter, enable, and ground domain.

**1.1 Path integrity (R + C).** DMM shorts-to-ground, source-to-farthest-load resistance, and bulk C at ~100 Hz against each converter’s max capacitive load. No rail-to-ground shorts; source-to-load DCR **0.4–0.6 Ω**; bulk C inside converter limits (e.g. +12 V **250 µF / 430 µF** max). **Pass.**

**1.2 Rise / fall / enable delay.** Defined 10–90% rise/fall and enable-to-rail delay on isolated vs. common grounds. All rises **&lt; 10 ms** (worst +12 V **9.57 ms**); turn-on delays **&lt; 100 ms** (worst +12 V **89 ms**). Fall times are capacitance-limited (coil +5 V **~7.7 s**) — **tentative** against an 8 s bound I set, with a note that fall time did **not** track measured C 1:1. Coil and AUX +5 V **latch on** after the enable and only die when 24 V is removed — documented as system behavior, not a surprise fail.

<figure>
  <img src="{{ '/docs/assets/rfs-rail-turnon.png' | relative_url }}" alt="Oscilloscope capture of +12 V rail rise with enable and annotated turn-on delay">
  <figcaption>+12 V enable vs. rail — rise and turn-on delay, annotated on the scope</figcaption>
</figure>

**1.3 Load-switch trip + inductive clamp.** Fuse-out rework, electronic load on the switch output, current ramped in 50–100 mA steps.

| Switch | Set ILIM | Measured trip | Input spike |
|--------|----------|---------------|-------------|
| Card-function (+12 V path) | 1.00 A | **1.004 A** | ~0 V |
| RFS coil | 3.70 A | **3.705 A** | +2 V |
| AUX | 3.70 A | **3.794 A** | +2 V |

All **Pass**; 24 V sagged to ~23 V at 3.7 A and recovered cleanly.

**1.4 Overcurrent hiccup.** Same fixture, IR on the switch, looking for t_on / t_off and auto-recovery. Card-function **MODE** is tied such that auto-retry is **off**; coil/AUX **LATCH** is held so they **stay off** after a trip. I closed the test as “characterize the design as built,” not a failed hiccup plot.

**1.5 Brownout / supervisors.** External PS injection on the +12 V supervisor sense. Mapped PG → PF and PF → PG: trip **10.67 V** emulated / recover **10.74 V**, **~78 mV** hysteresis — the card tells the system when the rail is no longer honest.

**1.6 Voltage drop, product worst case.** Close **62 HV**, **20 AUX**, and the **switch/stim** bank; measure converter, choke, and coil voltage at many pads. Open: coil rails sit at **~5.01 V** with ~0 V across an open coil. Closed: the coil line stays consistent along the board and **above dropout** (min pull-in **3.75 V @ 25 °C**, derated to **4.5 V @ 70 °C**). Sag was power-budget, not a mystery trace.

<p class="section-label">Deep dive</p>
## 2 · Shift registers + buffers — logic side and power side

Relay control is **daisy-chained STPIC6C595-class shift registers** (serial in/out, open-drain drains into the coils) driven by **clock/data buffers**. Fastest clocks in the notes sit around **~833 kHz**; the product is well below the part’s rating, so the risk is **ground bounce, crosstalk, and inductive kick**, not bit rate.

**2.1 Shift-register SI**

- Setup / hold on SER: **160 ns / 15 ns** both edges — **Pass** (hold is the tight one; setup has lots of margin)
- Ground bounce with all 8 drains switching ~30 mA HV-relay loads: **±10 mV** vs. **−0.3 / +0.75 V** limits
- Clock stays clean while every HV relay slams; apparent **330 MHz** ring attributed to coax-probe C, not the IC
- Open→close drain/coil: smooth, **5.05 V** peak. Close→open: **38.1 V** inductive spike, clamped by the open-drain / zener path (typical clamp ~37 V). Called **Pass\*** with that mechanism written down — not waved away

**2.2 Buffer SI** — rise **4 ns**, slew well inside **20 ns/V**, propagation **3 ns** vs. **3.5 ns** typical, peak **&lt; 5.1 V** vs. **5.5 V**. Ground-spring at the **receiver** (SR input). **Pass.**

<p class="section-label">Deep dive</p>
## 3 · Relays — time, power, contact, and neighbors

Two families, same three questions: **how fast**, **how much power**, **is the coil waveform healthy**.

| Family | Part class | Operate / limit | Release / limit | Bounce o→c | Coil power |
|--------|------------|-----------------|-----------------|------------|------------|
| HV disconnect + AUX | Standex HV reed | **400 µs / 1100 µs** | **13.5 µs / 100 µs** | **75 µs** | **28 mA, 140 mW** |
| Switch / stim | Coto reed | **130 µs / 350 µs** | **46 µs / 100 µs** | **30 µs** | **10 mA, 50 mW** |

Contact work needed **rework I specified**: isolate the RF pins, inject a clean DC source on one side, **680 Ω** DC load so bounce is a current path, not a floating capacitor. Open→close matches a classic reed bounce; close→open is a clean break then RC discharge — **Pass**, and the “healthy waveform” definition went into the report so later boards could use it.

Coil SI: HV family DC **&lt; 5.1 V** vs. **7.5 V** max, **no ringing**, close→open kick **38 V** and **clamped**. Switch/stim kick **5.9 V** vs. **6.5 V** max. **Pass.**

**7.1 Magnetic coupling** (the test most plans skip). Two supplies: victim pull-in / dropout, then a neighbor aiding vs. opposing.

| Condition (HV / AUX) | Pull-in | Dropout |
|----------------------|---------|---------|
| Isolated | 3.37 V | 1.72 V |
| Opposing neighbor | 3.54 V | 1.84 V |
| Aiding neighbor | 3.18 V | 1.53 V |

Shifts are real and in the expected direction — and **not large enough to invert open/close logic at 5 V coil drive**. Same story on switch/stim. **Pass.**

<p class="section-label">Deep dive</p>
## 4 · ADC, thermal, and the isolation plans

**5.1 Monitor ADC.** Lifted the +3.3 V inductor and swept an external rail while polling the card-function monitors. That produced a **use map**, not a single number:

- **Vin ≥ 2.6 V** — readings track
- **0.9–2.5 V** — the part still speaks, but the numbers are **wrong**
- **Vin ≤ 0.8 V** — high-Z / max-code, looks like a valid full-scale rail if you are not careful

That is the kind of conclusion firmware and system-monitor owners can actually use.

**8.1 System thermal.** Same worst-case relay set as 1.6; IR at 5 and 10 minutes. Hottest areas are **converters, SOM, and closed relays**. **Peak &lt; 40 °C** on the card. **Pass.**

**Isolator SI / CMTI / default-state (ISO776x / ISO772x class).** Propagation delay, skew, CMTI between SOM and RFS grounds, and fail-safe default outputs were **written into the framework**. They were still waiting on firmware hooks and a CMTI source at the end of my campaign — the plans shipped with the rest of the suite so the next owner did not start from zero.

<p class="section-label">Legacy</p>
## Why this outlived the RF Switch

The RF Switch was the first card that got a **complete, opinionated** system-level campaign: numbered suites, shared summary tracker, identical workbook anatomy, probing diagrams, FW mapping, and a written “what does pass mean.” That is what got reused.

Other boards in the **11+ PCB** cage have since been run through **the same parameters, in the same ways** — power integrity, SI at the control ICs, relay/contact health, ADC honesty, magnetic neighbors, thermal at max load. I did not just validate one card. I left a **method**.

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Ownership | Test selection, plans, execution, data, P/F limits, conclusions, summary readout |
| Power | 5-rail R+C, rise/fall, load-switch ILIM + clamp, brownout supervisors, worst-case IR drop |
| SI | Daisy-chained SRs, buffers, setup/hold, ground bounce, crosstalk, inductive clamp |
| Electromechanical | Reed operate/release/bounce, coil SI, magnetic aiding/opposing, hold-in stability |
| System | Card-cage + SOM, isolated grounds, ADC mapping vs. Vin, IR at max relay load |
| Bench | DMM, LCR, electronic load, programmable PS, 4-ch scopes, ground springs, FLIR, precision rework |
