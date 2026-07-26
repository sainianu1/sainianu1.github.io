---
layout: home
title: Hardware Engineer
body_class: is-home
description: Anubhav Saini — Engineering Physics at UBC. Hardware, PCB design, embedded systems, robotics, and power electronics.
---

<section class="hero" id="top">
  <div class="hero__media" aria-hidden="true">
    <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="">
  </div>
  <div class="hero__veil" aria-hidden="true"></div>
  <div class="hero__grid" aria-hidden="true"></div>

  <div class="container hero__content">
    <p class="eyebrow reveal">Engineering Physics · UBC · Hardware</p>
    <h1 class="reveal reveal-delay-1">Anubhav Saini</h1>
    <p class="lede reveal reveal-delay-2">
      I design and validate real hardware — power systems, motor control PCBs,
      sensors, and embedded firmware that ship from the bench to the product.
    </p>
    <div class="btn-row reveal reveal-delay-3">
      <a class="btn btn--primary" href="#work">View work</a>
      <a class="btn btn--ghost" href="{{ '/docs/assets/Resume%20-%20Anubhav%20Saini.pdf' | relative_url }}" target="_blank" rel="noopener">Resume</a>
    </div>
    <div class="hero__meta reveal reveal-delay-3">
      <div>
        Currently
        <strong>Hardware Eng Intern · Arlo</strong>
      </div>
      <div>
        Previously
        <strong>Sarcomere · Microchip</strong>
      </div>
      <div>
        Focus
        <strong>PCB · Power · Embedded</strong>
      </div>
    </div>
  </div>
</section>

<section class="section section--ink" id="work">
  <div class="container">
    <div class="section__head reveal">
      <p class="eyebrow">Selected work</p>
      <h2>Projects that prove I can build</h2>
      <p class="lede">From consumer camera power architecture to fingertip force sensing and autonomous robots — click through for schematics, boards, and results.</p>
    </div>

    <div class="project-mosaic">
      <a class="project-tile project-tile--featured reveal" href="{{ '/ArloCamera/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/USB_PowerCircuitry.png' | relative_url }}" alt="Arlo camera power circuitry">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">01 / Industry</span>
          <h3>Arlo Camera Power Circuitry</h3>
          <p>Power architecture for a solar-powered security camera — supply switching, battery charging, and validation under real load.</p>
          <ul class="tag-row">
            <li>Power</li>
            <li>MOSFETs</li>
            <li>Battery</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile project-tile--flip reveal" href="{{ '/SarcoSensor/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/force sensor4.png' | relative_url }}" alt="Fingertip magnetic force sensor">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">02 / Sensing</span>
          <h3>Fingertip Magnetic Force Sensor</h3>
          <p>Mapped normal force and shear from a tri-axis magnetometer inside a soft fingertip — high accuracy, low cost.</p>
          <ul class="tag-row">
            <li>Sensors</li>
            <li>Python</li>
            <li>Firmware</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile reveal" href="{{ '/SarcoPCB/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="Motor control PCB">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">03 / PCB</span>
          <h3>Motor Control PCB</h3>
          <p>Altium-designed BLDC motor driver board with STM32, SPI, I2C, and CAN — layout through bring-up.</p>
          <ul class="tag-row">
            <li>Altium</li>
            <li>STM32</li>
            <li>CAN</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <div class="project-grid-2">
        <a class="project-tile reveal" href="{{ '/MetalMario/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/MarioKart.png' | relative_url }}" alt="Metal Mario autonomous robot car">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">04 / Robotics</span>
            <h3>Metal Mario</h3>
            <p>Autonomous robot car with IMU fusion, rotary encoding, and PID control on a Mario Kart course.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>

        <a class="project-tile reveal" href="{{ '/MLrobot/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/MLRobot.png' | relative_url }}" alt="Machine learning robot detective">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">05 / ML + HW</span>
            <h3>ML Robot Detective</h3>
            <p>Vision-driven robot that classifies and acts on what it sees — embedded ML meets mechanical systems.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>
      </div>

      <div class="project-grid-2">
        <a class="project-tile reveal" href="{{ '/MicrochipMultithread/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/MicrochipLab.png' | relative_url }}" alt="Multithreaded test routine lab setup">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">06 / Test Eng</span>
            <h3>Multithreaded Test Routine</h3>
            <p>Python + firmware test flow that cut SERDES pad validation time by more than 40%.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>

        <a class="project-tile reveal" href="{{ '/UasBuckConvertor/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/UASBuck.png' | relative_url }}" alt="Buck converter circuit">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">07 / Power</span>
            <h3>Buck Converter Circuit</h3>
            <p>Designed, simulated, and built a buck converter — from schematic through measured regulation.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>
      </div>
    </div>
  </div>
</section>

<section class="section section--paper" id="about">
  <div class="container about-grid">
    <div class="about-portrait reveal">
      <img src="{{ '/docs/assets/ProfilePic1.png' | relative_url }}" alt="Portrait of Anubhav Saini">
    </div>
    <div class="about-copy reveal reveal-delay-1">
      <p class="eyebrow">About</p>
      <h2>Built for the hardware loop</h2>
      <p>
        I'm a 4th-year Engineering Physics student at UBC specializing in electrical engineering and robotics.
        I care about the full loop: schematic → layout → bring-up → measurement → iterate.
      </p>
      <p class="muted">
        Internships at Arlo, Sarcomere Dynamics, and Microchip taught me how to debug noisy sensors,
        ship motor-control boards, and write test firmware that actually saves time on the line.
      </p>
      <dl class="skill-bands">
        <div class="skill-band">
          <dt>Hardware</dt>
          <dd>PCB design (Altium), power management, sensor systems, STM32, ADC / UART / I2C / SPI / CAN</dd>
        </div>
        <div class="skill-band">
          <dt>Software</dt>
          <dd>C/C++, Python, embedded firmware, PlatformIO, MATLAB, ROS, OpenCV, TensorFlow</dd>
        </div>
        <div class="skill-band">
          <dt>Interests</dt>
          <dd>Robotics · Aerospace · Automotive · Consumer electronics · AI on the edge</dd>
        </div>
      </dl>
    </div>
  </div>
</section>

<section class="section section--ink" id="contact">
  <div class="container">
    <div class="contact-panel reveal">
      <div>
        <p class="eyebrow">Contact</p>
        <h2>Let's build something that works on the bench.</h2>
        <p class="lede">Open to hardware, firmware, and robotics roles — internship or full-time conversations welcome.</p>
      </div>
      <div class="contact-links">
        <a href="mailto:sainianubhav01@gmail.com"><span>Email</span><span>→</span></a>
        <a href="https://www.linkedin.com/in/anubhavsainiubc/" target="_blank" rel="noopener"><span>LinkedIn</span><span>→</span></a>
        <a href="https://github.com/sainianu1" target="_blank" rel="noopener"><span>GitHub</span><span>→</span></a>
        <a href="{{ '/docs/assets/Resume%20-%20Anubhav%20Saini.pdf' | relative_url }}" target="_blank" rel="noopener"><span>Resume PDF</span><span>→</span></a>
      </div>
    </div>
  </div>
</section>
