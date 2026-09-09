---
layout: project
title: Kardium — AmPLink PMIC Programming System
heading: PMIC Programming System
permalink: /Amplink/
cover: /docs/assets/PMIC1.jpg
eyebrow: Kardium Inc. · Electronics Hardware Intern
role: Electronics Hardware Engineering Intern · Kardium Inc.
timeline: 2026 · Burnaby, BC
summary: USB production programmer for power boards — I2C PMIC images, analog board identity, and a hardware interlock so the rails stayed off until the right config was written.
tags:
  - PMIC
  - PMBus
  - FTDI
  - I2C/SPI
  - Production test
metrics:
  - value: "2 fixtures"
    label: "SPI production + I2C bench"
  - value: "Hold → ID → burn"
    label: "Release only on success"
  - value: "HEX + XML"
    label: "One write path"
---

<p class="section-label">Context</p>
## What this was

I built a USB programming setup for boards that share the same four-rail PMIC but need different voltages and power-up sequences depending on board type and revision. The programmer had to identify the board, load the matching configuration, and keep the supplies off until that write succeeded.

Two USB adapters covered the two jobs: a four-port fixture for SPI flash and clock programming on processor and module boards, and a two-port adapter for I2C-only work on the PMIC bench. The software chose the pin map from the chip type, not from a product name.

<div class="figure-grid">
  <figure>
    <img src="{{ '/docs/assets/PMIC1.jpg' | relative_url }}" alt="PMIC programming bench with USB fixture and instrumentation">
    <figcaption>I2C / PMIC programming bench</figcaption>
  </figure>
  <figure>
    <img src="{{ '/docs/assets/PMIC2.jpg' | relative_url }}" alt="Second view of the PMIC programming bench and DUT">
    <figcaption>Bench bring-up and identity / interlock hardware</figcaption>
  </figure>
</div>

<p class="section-label">Hardware</p>
## Hardware I had to make talk

Three chips sat on one I2C bus: the PMIC, a 12-bit ADC, and an I/O expander used as the enable latch.

Board identity was analog. An R2R ladder produced a voltage for board type and another for revision. The ADC digitized both. I unpacked the 12-bit codes the way the datasheet specified, averaged samples, and matched them to a table with a few LSB of tolerance so converter noise did not miss a known board. Wrong byte order would have looked like a few volts instead of a few hundred millivolts; the datasheet unpack matched the ladder on the bench.

Enable was a hardware interlock, not a software hope. The expander output, through a pull-up and an NMOS, held the sequencer’s ON/OFF pin low so the PMIC stayed off. After a successful program, the expander pulled that line low, the FET released, and the sequencer could bring the rails up. The 3.3 V pull-up had to come from a rail that existed while the bucks were still off. If identification or programming failed, the expander was left in the hold state.

<figure class="figure-diagram">
  <img src="{{ '/docs/assets/amplink-system.svg' | relative_url }}" alt="Block diagram from host PC through FTDI chip-type detect to AmPLink SPI path or I2C bench with ADC, expander, and PMIC">
  <figcaption>USB → chip-type detect → SPI fixture or I2C bench</figcaption>
</figure>

<p class="section-label">Software</p>
## How I made the software work

I treated configuration as two layers. A short script chose the target and the sequence of operations. A separate image file held the register bytes. That let the same programmer stream Intel HEX or XML without mixing bring-up chatter into a production write.

Bring-up used register-level PMBus reads and writes: ping the PMIC, check identity and capability, step VREF per rail, set sequencing, then retrigger the rails with input still applied so a scope could catch TON stagger and rail order. Those writes lived in working registers. Cycling the 12 V input reloaded the factory EEPROM, so all four bucks came up together again. That was expected. A true non-volatile burn needed an explicit store command after unlocking write-protect. I left that off the default production images so demos and limited EEPROM cycles stayed safe, and used an in-session restart when I wanted to show sequencing without storing.

Production writes dropped the pings and reads. The same stagger and rail-order payloads went out as a linear image. HEX and XML both called the same write path; the format was detected from the file. Command-only PMBus operations, such as clearing faults, stayed in the script because an image record cannot send a command with no data.

The USB I2C path had to respect the PMIC’s clock-stretch timeout. Transfers were packed so the clock was not held across USB round-trips. After open, the bus was left at the PMIC address in a known idle state.

I collapsed the separate bring-up utilities into a debug mode on the main programmer, and kept a second binary for the one-button flow: hold enable, read the ADC, look up the image, program, then release only on success. A failed program returned a failing exit so the interlock never opened.

<p class="section-label">Results</p>
## What I shipped

A single programming stack that could flash SPI config and clocks on the production fixture, or write PMBus images on the I2C bench. Automatic SKU select from analog board ID and revision. Rails held off until the mapped image succeeded. Dual image formats through one write path. Teammate docs for the operator path, not a pile of one-off tools.

The result was a fail-safe, identity-driven programmer: identify the board, write the right power config, then allow the supplies to come up.
