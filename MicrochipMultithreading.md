---
layout: default
title: Multithreaded Test Routine
permalink: /MicrochipMultithread/
---

# Multithreaded Test Routine

## Project Overview

<div style="text-align: center; margin: 20px 0;">
    <img src="{{ '/docs/assets/MicrochipLab.png' | relative_url }}" alt="MarioKart1" style="width: 500px; border-radius: 10px;">
</div>


I formulated and deployed a **Multi-threaded testing procedure** to reduce testing time of SERDES Chips at Microchip Technology by **more than 40%**

**Reduced power consumption by 15%** via systematic voltage/temperature regularization scheme

---

## Skills Applied

| **Category**    | **Skills**                                                                 |
|------------------|---------------------------------------------------------------------------|
| **Design**       | Validation Systems Design                            |
| **Software**     | Python, Multithreading                                 |

---

## Project Workings
chips being tested for different levels of serialization/deserialization accuracy while being operated at 5 VT corners

- High Volt, Low Temp
- High Volt, High Temp
- Low Volt, Low Temp
- Low Volt, High Temp
- Nominal Volt, Nominal Temp

We had 8 different AC Tests and 5 different DC tests for each chip

- had to initialize chip at different characterization modes
- modes also depended on AC/DC tests

each of these tests required the chip being run at each of the 5 VT corners

things to configure for each test:
- initializing temp control
- initializing voltage control
- initializing bert input
    - frequency
    - bit length
- dcsu inputs
- some other params

i realized that configuring the bert input and other params for each of the 8 AC and DC tests respectively 

was possible if i took master control of the temp and voltage settings (most important was temp)
- as chip was set to run at (low, nom, high) voltage modes respectively while i could operate it at whatever voltage i initialized it at 
therefore, i would run all 8 AC tests and 5 DC tests while maintaining a single VT corner

then i would loop through the tests at each VT corner rather than looping through the VT corners at each test 

multithreading:
- running all required tests (with all the required inputs) while maintaining the voltage/temp corners simultaneously
- problem was that there were specific voltage trimming and temp regularization procedures which would need to happen regularly and without interruption 
- so i ran threaded python code which would (at required times during the tests) maintain the “master” voltage and temp control
    - i would feed in global variables for required temp/voltage/bert params etc which were protected so that they could not be altered during the voltage trimming or temp regularization 

procedures:
    - but these global variables could otherwise be changed during the tests as required by each test
        - global variables included the inputs for the bert/dcsu alongside the temperature and voltage

- also just to keep in mind, the tests were run with a loopback excel call where they would write raw results from the tests in excel files
- then they would compare these raw results with the required ranges/yields for the test to pass
- if this was met, the test would be labelled pass/fail


---

## Challenges Faced
- Ensuring reliable recalibration for repeatable repositioning.

---

## Lessons Learned
- **System integration:** Combining multiple different devices to emulate a real-life data transmission 

---
