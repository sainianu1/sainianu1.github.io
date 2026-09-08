---
layout: project
title: Kardium — AmPLink PMIC Programming System
heading: PMIC Programming System
permalink: /Amplink/
cover: /docs/assets/PMIC1.jpg
eyebrow: Kardium Inc. · Electronics Hardware Intern
role: Electronics Hardware Engineering Intern · Kardium Inc.
timeline: 2026 · Burnaby, BC
summary: Took an existing AmPLink SPI flash / clock-burn tool and turned it into a two-binary production programmer — same script language on two USB fixtures, automatic board identity, and a hardware interlock that keeps the PMIC disabled until the correct image is written.
tags:
  - PMIC
  - PMBus
  - FTDI
  - I2C / SPI
  - Production test
metrics:
  - value: "2 fixtures"
    label: "One script language"
  - value: "2 binaries"
    label: "Production + debug mode"
  - value: "Hold → ID → burn"
    label: "Release only on success"
---

<p class="section-label">Context</p>
## The problem

Production boards share a **TPS65400** four-buck PMIC but need **different power-up and VOUT images** by board type and revision. Identity is analog: an **R2R ladder** into an **ADS7142**. The rails must not come up on a factory EEPROM default — all bucks together — before the right sequence is loaded.

The inherited tool already programmed **processor and SOM** boards on an **FT4232H AmPLink** fixture (SPI config flash + VersaClock I2C). The bench I needed was different: an **FT2232H**, I2C only, talking to **three devices on one bus**.

I needed one stack that could:

- Keep talking to AmPLink (SPI + GPIO + clock)
- Program the TPS65400 over **PMBus** on the 2232 bench, including **HEX / XML** images — not only interactive register pokes
- Identify the board from the ADC and pick the image from an **editable map**
- **Hold the PMIC off** until that program succeeds, then release enable

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

<div class="callout">
  The honest parallel to the Microchip SERDES card is a fail-safe, identity-driven, dual-fixture programmer — not a fake time-cut KPI.
</div>

<p class="section-label">Impact</p>
## What a recruiter should know

- One **script language** on two fixtures: AmPLink SPI/GPIO/clock and an FT2232H PMBus bench
- **Two production binaries** instead of a folder of test exes — debug is a mode, not a product
- Dual image formats (**Intel HEX + XML**) through the same `I2C_SEND` / `SPI_FLASH_SEND` callbacks
- Automatic SKU select: 12-bit AIN0/AIN1, editable map, **±8 LSB** window
- Hardware interlock: **DS4520 + FET + sequencer** polarity — no release on a failed burn
- Datasheet-correct **TON stagger** and rail order proven in RAM, with an explicit path to EEPROM store when a true persist is wanted
- Handoff docs so a teammate can change a map row or add an I2C name without reverse-engineering the tree

<figure class="figure-diagram">
  <img src="{{ '/docs/assets/amplink-system.svg' | relative_url }}" alt="Block diagram from host PC through FTDI chip-type detect to AmPLink SPI path or I2C bench with ADC, DS4520, and TPS65400">
  <figcaption>USB → chip-type detect → AmPLink (4232) or I2C bench (2232)</figcaption>
</figure>

<p class="section-label">Hardware</p>
## Two USB targets, one detect path

The programmer does not look for an “AmPLink” string. It reads the first **D2XX chip type**.

| Dongle | Job | What opens |
|--------|-----|------------|
| **FT4232H** | AmPLink PROC / SOM | GPIO + SPI mux + I2C ch0 |
| **FT2232H** | I2C bench | I2C channel 1 (interface B) only |

Swapping a 2232 onto AmPLink wiring does not make SPI work. Swapping a 4232 onto the bench without an I2C-on-channel-1 init does not make the bench path.

### I2C bench bus

| Device | Address | Role |
|--------|---------|------|
| TPS65400 | 0x6A | Four-buck PMIC (PMBus) |
| DS4520E+ | 0x50 | EEPROM I/O expander — enable interlock |
| ADS7142 | 0x1F | 12-bit ADC — board ID (AIN0) and revision (AIN1) |

### Enable chain

DS4520 **I/O 2** has a **10 kΩ pull-up to 3.3 V** and drives an NMOS gate. FET on (I/O 2 high-Z) pulls **MAX16165 ON/OFF** low → PENs held off → TPS65400 stays off. I/O 2 low releases the FET so the sequencer can enable the PMIC. That 3.3 V pull-up has to exist **while bucks are off** (VDDD / VIN LDO) — not a buck rail.

On the breadboard I validated DS4520 I/O 2 and the ADC without the full MAX16165 loop; the scripts still implement the production polarity.

### Board ID

R2R voltage → ADS7142. Codes unpack as `(MSB << 4) | (LSB >> 4)` — swapped bytes decoded as ~2.7 V and were wrong. Bench averages landed around **0x120–0x12D** (~232–242 mV at AVDD = 3.3 V). The map uses **±8 LSB** so a few codes of converter noise still match. Default map row: `0x12D  0x12D  burn_seq_ton_stagger.txt`.

<p class="section-label">Software</p>
## Two executables, one language

Both live next to scripts, HEX/XML payloads, and the FTDI DLLs (`ftd2xx.dll`, `libmpsse.dll`).

| Binary | Job |
|--------|-----|
| `AmplinkFlashProgrammer.exe` | Run one `.txt`, or `debug <tool>` without going through full programmer init |
| `Board_id_programmer.exe` | No FTDI of its own — shells out to the programmer. Failed script exits non-zero, so **release never runs** if the burn fails |

Production path:

**hold → ads_read → map → script → release (only on success)**

Debug tools that used to be separate binaries (`ack_test`, `ads_read`, `tps65400_read`, `tps65400_id`) are now **functions on the same exe**. Explicit product decision: two hierarchical binaries, not a pile of utilities.

`i2c_xfer` packs write-then-read with `FAST_TRANSFER_BYTES` so SCL is not stretched across USB ACK round-trips past the TPS65400’s **25–35 ms** timeout. Idle ping to 0x6A after init; bus-clear on failure.

<p class="section-label">Deep dive</p>
## How it was built

### 1 · Prove the I2C bench with PMBus
`I2C_PING` / `I2C_WRITE` / `I2C_READ` on VREF, PAGE, **CAPABILITY (0xA0)**, **PMBUS_REVISION (0x22)**. That confirmed FT2232H channel B, address 0x6A, and that the part was the TPS65400 we thought it was.

### 2 · Production back on linear images
Interactive pings are for bring-up. `I2C_SEND(file.hex, TPS65400)` reuses the original Intel HEX parser: record address low byte = first byte on the wire (PMBus command), remaining bytes = payload. Same idea as `SPI_FLASH_SEND` on AmPLink — the script chooses the target; HEX/XML is the image.

### 3 · XML sister payloads
Hand-written XML parser, same callback as HEX. Auto-detect by extension or first non-space (`:` vs `<`). Command-only PMBus (e.g. CLEAR_FAULTS 0x03) stays in the `.txt` because a data record cannot emit a command-only transaction.

### 4 · Sequencing from the datasheet
TON stagger **0 / 25 / 100 / 500 ms**. Start order **SW1 → SW2 → SW3 → SW4**. `seq_restart.txt` — OPERATION off/on on PAGE 0xFF with VIN still up, so you can scope the rails without cycling 12 V.

### 5 · RAM vs EEPROM — measured, then designed around
A **12 V VIN cycle** put all rails back on together. Live writes hit working registers; EEPROM reloads on VIN. Persist with **STORE_DEFAULT_ALL (0x11)** after unlocking WRITE_PROTECT. Production `burn_seq_*` **omit 0x11** on purpose (limited EEPROM cycles, safer demos). `seq_restart` is how you show sequencing without a store.

### 6 · Board ID on the same bus
ADS7142 bring-up: ACK at 0x1F, manual mode, datasheet nibble unpack, then AIN0 + AIN1, then `board_id_map.txt`: `id  rev  script  [tolerance]`.

### 7 · Fail-safe enable
`Board_id_programmer` always:

1. `ds4520_hold_off.txt` — I/O 2 high-Z, PMIC held off
2. `debug ads_read` — parse AIN0 / AIN1 averages
3. Map lookup
4. Mapped PMIC script
5. `ds4520_release.txt` **only if step 4 exits 0**

DS4520 **0xF2** is SRAM-shadowed EEPROM — hold/release persist. That only gates enable; it is not a copy of the TPS65400 image.

### 8 · Operator surface
CMake / Ninja / MSYS2 build, DLLs beside the exes, teammate **PROGRAMMER_GUIDE** (channel maps, parsers, pitfalls), **ARCHITECTURE** (every `src/` file and script in two sentences), **README** as the operator path.

<p class="section-label">Operators</p>
## What actually gets run

**Bring-up (debug, no script parse)** — `debug ack_test`, `debug tps65400_id`, `debug ads_read`. Expect ACKs at **0x6A, 0x50, 0x1F**.

**Manual bench** — `comms.txt`, `burn_seq_ton_stagger.txt`, `seq_restart.txt`.

**One-button production** — `Board_id_programmer.exe`.

**AmPLink (unchanged language, different USB map)** — `PROC.txt`, `SOM.txt`. Those still need the vendor HEX images and an FT4232H.

<p class="section-label">Results</p>
## What we proved

- Default map hit on the bench codes (**0x120–0x12D**, ±8 LSB)
- TON stagger visible after `seq_restart` with VIN held up
- PMIC **stayed off** on a map miss or a failed script — release never ran
- Same `.txt` language still burns PROC / SOM flash on the 4232 AmPLink
- A teammate can add a map row or an I2C name from the handoff docs

<p class="section-label">Skills</p>
## Tools & techniques

| Area | What I used |
|------|-------------|
| Fixtures | FT4232H AmPLink vs FT2232H I2C bench, D2XX chip-type detect |
| PMIC | TPS65400 PMBus, HEX/XML images, TON stagger, RAM vs EEPROM store |
| Identity | R2R → ADS7142, nibble unpack, editable map + tolerance |
| Interlock | DS4520 I/O 2, FET, MAX16165 polarity, release only on success |
| Stack | script parser, libMPSSE + D2XX, packed I2C xfer, CMake/Ninja/MSYS2 |
