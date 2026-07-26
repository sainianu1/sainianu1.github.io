---
layout: project
title: SERDES Multithreaded Characterization at Microchip
heading: SERDES Multithreaded Test
permalink: /MicrochipMultithread/
cover: /docs/assets/MicrochipLab.png
eyebrow: Microchip Technology · Product Engineering Intern
role: Product Engineering Intern · Microchip Technology
timeline: May 2024 — Aug 2024 · Burnaby, BC
summary: Python + firmware characterization flow for a SERDES I3C pad — multithreaded VT-corner testing that cut validation time by more than 40% and power by 15%.
tags:
  - Python
  - Multithreading
  - SERDES
  - Mixed-Signal
metrics:
  - value: "40%+"
    label: "Faster test time"
  - value: "15% less"
    label: "Power via VT regularization"
  - value: "5 VT"
    label: "Corners fully swept"
---

<p class="section-label">Context</p>
## The problem

At Microchip I characterized a **SERDES I3C pad** against performance requirements. Each device needed a battery of AC and DC tests across **five voltage/temperature corners** — and the naive loop (every test × every corner, with heavy setup each time) was burning lab time and power.

<figure>
  <img src="{{ '/docs/assets/MicrochipLab.png' | relative_url }}" alt="Microchip SERDES test lab setup">
  <figcaption>Characterization bench / lab setup</figcaption>
</figure>

<p class="section-label">Approach</p>
## What I changed

### Test matrix
- **5 VT corners:** HV/LT, HV/HT, LV/LT, LV/HT, nominal
- **8 AC + 5 DC tests** per chip, each with its own init mode
- Per-test knobs: temperature control, voltage control, BERT (frequency, bit length), DCSU inputs, and related params

### Smarter looping
Instead of sweeping VT inside every test, I took **master control of temp/voltage**, ran the full AC/DC suite at a fixed corner, then advanced corners. That collapsed redundant thermal/electrical settles.

### Multithreaded “master” regulation
Voltage trimming and temperature regularization had to run on time, uninterrupted. I wrote **threaded Python** that owned master VT control while tests progressed, using protected globals for temp / voltage / BERT params so regularization couldn’t be stomped mid-settle — while still allowing per-test updates when safe.

### Results pipeline
Tests wrote raw results through a loopback Excel path, compared them to pass/fail windows, and labeled outcomes automatically.

<div class="callout">
  <strong>Outcome:</strong> deployed a multithreaded procedure that cut SERDES pad testing time by <strong>&gt;40%</strong>, reduced power consumption by <strong>15%</strong> via systematic VT regularization, and fully characterized the I3C pad against mixed-signal requirements.
</div>

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Software | Python, multithreading, protected shared state |
| Firmware | Custom device init / mode control for AC & DC suites |
| Characterization | SERDES / I3C pad, BERT, DCSU, 5-corner VT sweeps |
| Analysis | Automated pass/fail vs yield windows |
