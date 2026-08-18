---
layout: project
title: Solar Express — Panel-Level DC Power Optimizer
heading: Solar Express
permalink: /SolarExpress/
cover: /docs/assets/solar-express-system-diagram.png
eyebrow: Personal Project · Power Electronics
role: Architecture · controls · simulation
timeline: Personal project
summary: 600W panel-level DC power optimizer — a 4-switch non-inverting buck-boost with 100V GaN FETs at 250 kHz, designed to track each PV panel’s maximum power point, integrate with mainstream string inverters, and meet NEC 690.12 rapid shutdown. Validated in NGSpice at 99%+ pass-through efficiency, with a Type-II compensator achieving ≥94° phase margin across the operating envelope.
tags:
  - GaN
  - Buck-Boost
  - MPPT
  - NEC 690.12
metrics:
  - value: "600W"
    label: "Panel-level optimizer"
  - value: "99.2%+"
    label: "Pass-through efficiency"
  - value: "≥94°"
    label: "Phase margin across envelope"
---

<p class="section-label">Context</p>
## The problem

Solar Express is a **panel-level DC power optimizer** — the electrical foundation of a broader integration platform for building-integrated and retrofit solar. It sits between one PV panel and the DC string, extracting maximum power from that panel regardless of what the rest of the string is doing.

String-level mismatch is the well-defined failure of “wire the panels in series and let the inverter handle it.” When modules see different irradiance — partial shading, mixed orientation, soiling, thermal gradients — a single global MPPT at the inverter cannot optimize every panel. Energy is left on the table. One converter per module decouples each panel’s operating point so every module can run at its own MPP while still feeding a common DC string bus.

The design is an **open, commodity-compatible** alternative to closed ecosystems. It works with standard **45–60 V-class PV panels** and mainstream string inverters (SMA, Sungrow, Fronius, Sol-Ark, and similar) that already perform string-level MPPT — not proprietary fixed-voltage architectures.

<figure class="figure-diagram">
  <img src="{{ '/docs/assets/solar-express-system-diagram.png' | relative_url }}" alt="Solar Express system diagram: PV panels into 600W 4-switch GaN optimizers, series DC string bus, string inverter, grid, with telemetry and NEC 690.12 rapid shutdown">
  <figcaption>System architecture — panel → optimizer → DC string → inverter, with telemetry and rapid shutdown</figcaption>
</figure>

<div class="callout">
  Resume version stays high-level (600W, 99%+ efficiency, safety timing). This page is the engineer walkthrough of topology, controls, and the simulation sign-off.
</div>

<p class="section-label">Impact</p>
## What a recruiter should know

- Designed a **600W panel-level DC optimizer** — **4-switch non-inverting buck-boost** with **100V GaN FETs at 250 kHz** — to track each panel’s MPP and feed a common string bus
- Validated **≥99.2% pass-through** and **99.18% nominal-boost** efficiency in NGSpice across a 24-point Vin × Vout grid
- Built a **Type-II compensator** with **≥94° phase margin** and **≥10 dB gain margin** across the operating envelope, including the dawn RHP-zero corner
- Closed **NEC 690.12** rapid shutdown to **≤1 V in ~1.1 s** (2 s spec) and specified staggered sunrise startup so a full string does not trip inverter OVP

<p class="section-label">Constraints</p>
## Why a naive string is not enough

- **Partial shading and mismatch.** One shaded panel current-limits the string. The inverter finds a compromise operating point; unshaded panels are pulled off their individual peaks.
- **Wide voltage envelope.** Panel voltage swings from ~**10 V at dawn** to ~**80 V cold Voc**. String bus voltage is set by inverter demand plus the series sum of optimizers. The converter must buck, boost, and pass through without mode chatter or efficiency cliffs.
- **Safety regulation.** **NEC 690.12** requires module-level rapid shutdown: within **2 s** of a command, each optimizer output must fall to **≤1 V**.
- **Inverter compatibility.** On the string side the optimizer must behave as a **regulated current source** — delivering MPP power into whatever load the inverter presents — without fighting the inverter’s own MPPT. Simultaneous sunrise boot of every unit in a string must not trip inverter overvoltage protection.
- **Efficiency at scale.** At 600 W continuous, 1–2% conversion loss is heat and lost revenue over a 25-year design life. GaN changes the loss budget relative to legacy silicon optimizers.

<p class="section-label">Architecture</p>
## Design decisions

### Topology — 4-switch non-inverting buck-boost
Four GaN FETs as two half-bridge legs around one inductor give non-inverting **buck**, **boost**, and **buck-boost**, plus a dedicated **pass-through** mode (Q1 + Q4 held ON — the topology becomes a wire). Pass-through is the efficiency play: when Vin ≈ Vout, switching losses vanish and efficiency exceeds **99%**.

### Switch technology — 100V-class GaN at 250 kHz
Low RDS(on) and fast edges allow higher frequency and a smaller inductor than silicon. Fixed **250 kHz** (crystal-derived, ±50 ppm) sits above PLC telemetry (**50–95 kHz**) and rapid-shutdown signaling (**100–150 kHz**), so the power stage does not land in the safety or communications bands.

### Terminal behavior — regulated current source
During MPPT, the optimizer regulates **output current** to push the panel’s MPP power into the string. Output voltage is set by the downstream load (other optimizers + inverter input). A fail-safe clamp (**VOUT_REG**) engages only if Vout would exceed **80 V** — protecting wiring on an open-string fault.

### Nested control + supervisor

| Loop | Rate | Job |
|------|------|-----|
| Inner | ~20 kHz | Peak current-mode on inductor current; slope compensation in boost / buck-boost; hardware OCP latch **&lt;1 µs**, independent of firmware |
| Outer | 100 Hz–1 kHz | Hybrid Perturb-and-Observe + Incremental Conductance MPPT with adaptive step; global MPP rescan on shading (**&gt;30%** power drop in **&lt;2 s**) |
| Supervisor | 1 Hz | Mode arbitration (BUCK / BOOST / BUCK-BOOST / PASS-THROUGH), fault classification, telemetry, rapid-shutdown state machine |

**Staggered startup:** a deterministic **0–500 ms** delay from the serial-number hash prevents every optimizer in a string from stepping voltage at once at sunrise.

### Safety — NEC 690.12 rapid shutdown
On RSD command, signal loss, or comms loss **&gt;7 s**, the state machine goes to active discharge: FETs latched off, **Q3** modulated as the discharger, output bleeder holds **Vout ≤1 V**. Simulated discharge: **~1.1 s** (spec ≤2 s).

<p class="section-label">Power stage</p>
## How the four switches convert

<pre>pv+ ── Q1 ──┬── sw_in ──[L]──[Rshunt]── sw_out ── Q4 ──┬── str+
            Q2│                                         Q3│
pv− ─────────┴───────────────────────────────────────────┴── str−</pre>

| Mode | Condition | Active switches | Conversion |
|------|-----------|-----------------|------------|
| Buck | Vin &gt; Vout | Q1/Q2 PWM, Q4 ON | Vout = d·Vin |
| Boost | Vin &lt; Vout | Q1 ON, Q3/Q4 PWM | Vout = Vin/(1−d) |
| Buck-boost | Vin ≈ Vout | All four PWM | Smooth transition, no mode chatter |
| Pass-through | Vin ≈ Vout (±2%) | Q1 + Q4 ON | M = 1 (near-lossless wire) |

**Dawn boost.** Panel at 18 V, string at 60 V. Q1 held ON; Q3/Q4 alternate at 250 kHz. Q3 charges the inductor from Vin; Q3 off + Q4 on delivers stored energy plus Vin to the output cap. MPPT sets duty so the panel sits at MPP as string voltage drifts.

**Midday buck.** Panel at 75 V, string pulled to 35 V by the inverter. Q3/Q4 static; Q1/Q2 chop at 250 kHz.

The **boost-mode RHP zero** is the binding control constraint. In boost, the small-signal plant has a right-half-plane zero at **f_RHPZ = (1−D)² · R / (2πL)**. At the nominal **45→60 V** point it sits at **~79 kHz** (harmless). At the dawn corner (**10→60 V**, D = 0.833) it collapses to **3.9 kHz**, capping inner-loop crossover at **~1.3 kHz**. That drove compensator design and MPPT rate selection (**100 Hz** full sun, **10 Hz** at low irradiance) so the optimizer stays cleanly separated from the inverter’s own MPPT loop.

<p class="section-label">Validation</p>
## Simulation campaigns

Three-layer pipeline: switching netlists for ground-truth efficiency, ripple, transients, and RSD timing; averaged plant `.ac` for a calibrated magnitude anchor at 1 kHz; Python (`plant_control.py`) for RHPZ, poles, Type-II compensator, and GM/PM.

### Campaign 1 — Power stage
NGSpice switching sims, **24-point** Vin × Vout grid @ **10 A**.

| Metric | Result |
|--------|--------|
| Pass-through efficiency | **≥99.2%** |
| Nominal boost (45→60 V) | **99.18%** |
| Soft-start Vout overshoot | **0.026%** (spec ≤5%) |
| Inductor peak current | **17.55 A** (OCP at 18 A) |
| RSD discharge to ≤1 V | **~1.1 s** (spec ≤2 s) |

### Campaign 2 — Controls
Small-signal plant ID + Type-II compensator (**K = 0.0015**, **fz = 600 Hz**, **fp = 40 kHz**). All anchors pass **GM ≥10 dB** and **PM ≥45°**.

| Anchor | Phase margin | Crossover | RHPZ |
|--------|--------------|-----------|------|
| Nominal boost (45→60 V) | **97°** | 122 Hz | 79 kHz |
| Low-Vin boost (10→60 V) | **127°** | 790 Hz | 3.9 kHz |
| Buck corner (80→45 V) | **94°** | 68 Hz | — |
| Inverter load step | **0.12%** Vout deviation | — | — |

### Component lock
Parametric sweeps over RDS(on) **3–22 mΩ**, fsw **100 kHz–1 MHz**, and L **3.3–22 µH** locked **6.8 µH / 3.2 mΩ / 250 kHz**. Python loss model agrees within **±0.5%** of NGSpice.

<p class="section-label">Specs</p>
## Design envelope

| Parameter | Value |
|-----------|--------|
| Rated power | 600 W |
| Input range | 10–80 V, 0–15 A |
| Output range | 5–80 V per unit (current-source behavior) |
| Peak efficiency | ≥99% (pass-through) |
| Switching frequency | 250 kHz fixed |
| Operating temp | −40 °C to +85 °C |
| Enclosure target | IP68 |
| MCU | STM32G474 (HRTIM, ADC12, CORDIC) |
| Compliance targets | NEC 690.12, UL 1741 SB, IEC 62109-1 |

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Power electronics | 4-switch buck-boost, GaN FET sizing, loss-budget optimization, EMI / PLC band planning |
| Controls | Small-signal plant ID, RHP-zero-aware Type-II compensator, nested loops, hybrid P&O + IncCond MPPT |
| Simulation | Python-driven NGSpice campaigns, 24-point efficiency grids, closed-loop stability sign-off |
| Systems | Requirements traceability, inverter-compatibility analysis, safety state machines, staggered string startup |
| Standards | NEC 690.12 rapid shutdown, UL 1741 SB, IEC 62109-1 creepage / clearance |
