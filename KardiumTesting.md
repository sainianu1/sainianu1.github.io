---
layout: project
title: Kardium — System-Level RF Switch Validation
heading: System-Level RF Switch Validation
permalink: /KardiumTesting/
cover: /docs/assets/rfs-cardcage.jpg
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

Kardium’s **OneBox RF Switch** sits in a **card-cage** with a system-on-module, backplane, and 24 V system power. It steers **RF driver and stimulation paths** through banks of high-voltage disconnect and switching relays. Firmware controls those relays through daisy-chained shift registers and line buffers. Several isolated power and ground domains share the same assembly, so a power, timing, relay, or monitoring problem on this card can affect the rest of the ablation system.

Nobody handed me a finished protocol. Over a **three-month** campaign I decided what “healthy” meant at system level, wrote the plans, built the fixtures and rework, collected the data, set the pass/fail limits from datasheets and worst-case use, and wrote the conclusions — for **every** test.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/rfs-board-top.jpg' | relative_url }}" alt="Top-down photo of the OneBox RF Switch with the Kardium SOM installed over the relay field">
    <figcaption>RF Switch + OneBox SOM — relay field, test points, live rails</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/rfs-cardcage.jpg' | relative_url }}" alt="RF Switch card standing in the metal card cage with converters and adjacent boards visible">
    <figcaption>In the card cage — the system the tests were written against</figcaption>
  </figure>
</div>

<div class="callout">
  The <a href="{{ '/Kardium/' | relative_url }}">layout / DFM page</a> is the production-PCB story. This page is the validation engineer walkthrough: how the RF Switch was proven on the bench, and why that method stuck.
</div>

<p class="section-label">Impact</p>
## What a recruiter should know

- **Owned the full loop** on the OneBox RF Switch: what to test, written plans, execution, data reduction, pass/fail requirements, and signed conclusions — not just “ran someone else’s script”
- Completed **17 tests across 8 suites** covering power, digital signal integrity, high-voltage and auxiliary relays, switching relays, ADC diagnostics, magnetic coupling, and system thermal performance
- Exercised the card the way the product actually fails: 62 HV disconnects relays + 20 AUX power supply relays + 45 switching relays closed together, rails measured from DC-DC output through chokes to the farthest coils.
- Characterized system behavior that a simple functional check would miss, including power-rail latching and recovery, relay-drive protection, and the conditions under which onboard monitoring could be trusted
- That structure — same sheet layout, probing notes, FW mapping, P/F table, and report — became the **fundamental test framework** for the rest of the **11+ board** PCB ecosystem; other cards have since been tested to the same parameters, the same way

<p class="section-label">Method</p>
## How a test was built

Every workbook followed the same structure so another engineer could repeat the test:

| Step | What I did |
|------|------------|
| Decide | Identify a realistic failure, such as a rail dropping under load, a relay switching incorrectly, or one circuit disturbing another |
| Plan | Define the purpose, equipment, probe locations, board modifications, firmware commands, and step-by-step procedure |
| Limits | Set acceptance criteria from component datasheets, operating temperature, maximum expected load, and the way the product would be used |
| Bench | Test the complete card-cage assembly using meters, programmable supplies and loads, oscilloscopes, an IR camera, and microscope-assisted rework |
| Conclude | Record what happened, compare it with the acceptance criteria, and explain any behavior that needed follow-up |

<p class="section-label">Deep dive</p>
## 1 · Power — five rails, worst-case load

I validated five power rails ranging from **3.3 V to 24 V**. The tests covered the complete path from each supply to the circuits and relay coils it powered, including separate enable controls and isolated ground domains.

**1.1 Power-path inspection.** Before applying power, I checked each rail for shorts, measured resistance from the supply to its farthest load, and measured the total capacitance connected to the converter. This confirmed that the assembled board was safe to power and that long traces, connectors, chokes, and capacitors would not place an unintended load on the supply.

**1.2 Power-up and power-down timing.** I used an oscilloscope to compare each enable signal with the corresponding rail as it turned on and off. This established the board’s startup sequence, shutdown behavior, and delay between a command and usable power—important for preventing circuits from starting in an undefined state.

<figure>
  <img src="{{ '/docs/assets/rfs-rail-turnon.png' | relative_url }}" alt="Oscilloscope capture of a power rail rising after its enable signal">
  <figcaption>Comparing a rail with its enable signal during startup</figcaption>
</figure>

**1.3 Overcurrent protection.** I isolated each protected output, connected a programmable electronic load, and increased the current in controlled steps. I monitored both the point where protection activated and the voltage disturbance created when the load was disconnected. This verified that a fault would be contained without overstressing the upstream supply.

**1.4 Recovery after a fault.** I deliberately triggered the same protection circuits and observed whether each output retried automatically, latched off, or required the main supply to be cycled. I also checked the hardware configuration that selected this behavior. The resulting documentation gave firmware and system engineers a clear recovery sequence for each rail.

**1.5 Brownout detection.** I replaced the normal rail with a controllable bench supply and slowly swept its voltage through the supervisor’s operating range. By monitoring the power-good and power-fail signals, I verified that the card could warn the rest of the system when its supply was no longer reliable and could recognize when normal operation was restored.

**1.6 Voltage delivery under maximum relay load.** I closed every relay bank used in the worst-case product state, then measured each coil supply at the converter, across the filtering chokes, and at the farthest relays. This showed whether the complete power path—not just the converter output—could keep all relay coils energized at once, including at elevated operating temperature.

<p class="section-label">Deep dive</p>
## 2 · Shift registers + buffers — logic side and power side

Relay control uses daisy-chained shift registers driven by clock and data buffers. The clock rate itself was comfortably within the component rating; the practical risks were electrical noise, interference between nearby signals, and the voltage spike produced when a relay coil switched off.

**2.1 Shift-register signals.** I probed serial data, clock, and relay-drive outputs while firmware switched individual channels and entire banks. I checked data timing at the receiving device, measured ground movement when several outputs changed together, and inspected the coil turn-off waveform. This verified that commands could travel through the full chain without being corrupted by simultaneous relay activity.

**2.2 Clock and data buffers.** I measured signal level, edge speed, and propagation delay at the shift-register inputs rather than only at the source. Short ground-spring probes helped separate real board behavior from noise introduced by the measurement setup. This confirmed that the buffers delivered clean, correctly timed logic signals to the devices that consumed them.

<p class="section-label">Deep dive</p>
## 3 · Relays — time, power, contact, and neighbors

The card uses two relay families for high-voltage disconnect, auxiliary power, RF switching, and stimulation. I evaluated both families using the same questions: how quickly does the contact respond, how cleanly does it switch, how much power does the coil require, and can nearby relays affect it?

**3.1 Operate and release timing.** I captured the coil command and contact voltage together so I could measure the complete delay from an electrical command to a physical contact change. I compared those delays with the relay specifications to confirm that the system allowed enough time before using a newly selected path.

**3.2 Contact bounce.** I specified board rework that isolated the RF contacts, then applied a controlled DC source and resistive load. This turned each contact closure and release into a waveform that could be measured consistently. The test established a repeatable definition of a healthy contact transition for this card and future boards.

**3.3 Coil-drive behavior.** I monitored coil voltage and current during turn-on, steady operation, and turn-off. This checked that the driver supplied enough energy to move the relay without exceeding the coil rating, and that the built-in clamp safely controlled the turn-off voltage spike.

**3.4 Magnetic interaction between neighboring relays.** I measured one relay’s pull-in and dropout behavior by itself, then repeated the test with a neighboring relay energized in both magnetic orientations. This addressed a board-level risk that a component-only test would miss: tightly packed relay coils influencing one another.

<p class="section-label">Deep dive</p>
## 4 · ADC, thermal, and the isolation plans

**4.1 ADC monitoring.** I isolated the ADC’s analog supply, powered it from a controllable source, and swept that source while firmware continuously reported the monitored channels. Instead of checking accuracy at only one voltage, I mapped where the readings were reliable, where they became misleading, and how an unpowered monitor appeared to software. This gave firmware engineers practical rules for deciding when telemetry could be trusted.

**4.2 System thermal test.** I ran the card in its maximum relay-load state inside the production card cage and captured infrared images over time. I inspected the converters, system-on-module, relay banks, and local hot spots to verify that the assembled system could sustain the intended operating state without thermal stress.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/rfs-thermal-system.jpg' | relative_url }}" alt="FLIR thermal capture of the RF Switch in the card cage with rows of closed relays warming">
    <figcaption>Worst-case IR — card cage, max relays closed</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/rfs-thermal-board.jpg' | relative_url }}" alt="FLIR close-up of the RF Switch PCB showing power and SOM hotspots">
    <figcaption>Board-level IR — supplies, SOM, closed relays</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/rfs-inspect.jpg' | relative_url }}" alt="Microscope view of a surface-mount IC during board inspection">
    <figcaption>Component-level inspection during rework and bring-up</figcaption>
  </figure>
</div>

**4.3 Digital-isolator test plans.** I also wrote procedures for isolator timing, channel-to-channel skew, immunity to fast ground differences, and output behavior when an input lost power. These tests required firmware hooks and specialized equipment that were not available before the end of my term, so I delivered complete plans that the next engineer could execute rather than leaving the work undefined.

<p class="section-label">Legacy</p>
## Why this outlived the RF Switch

The RF Switch was the first card to receive a complete system-level campaign with numbered suites, a shared summary tracker, consistent workbooks, probing diagrams, firmware mapping, and written acceptance criteria. That is what got reused.

Other boards in the **11+ PCB** cage have since been run through **the same parameters, in the same ways** — power integrity, SI at the control ICs, relay/contact health, ADC honesty, magnetic neighbors, thermal at max load. I did not just validate one card. I left a **method**.

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Ownership | Test selection, plans, execution, data analysis, acceptance criteria, conclusions, and summary reports |
| Power | Five-rail validation, startup and shutdown timing, overcurrent protection, brownout detection, and worst-case voltage delivery |
| Digital signals | Daisy-chained shift registers, clock and data buffers, timing margins, electrical noise, interference, and relay turn-off protection |
| Electromechanical | Relay operate and release timing, contact bounce, coil drive, neighboring magnetic fields, and hold-in stability |
| System | Card cage and system-on-module, isolated grounds, ADC behavior across its supply range, and thermal imaging at maximum relay load |
| Bench | DMM, LCR, electronic load, programmable PS, 4-ch scopes, ground springs, FLIR, precision rework |
