---
layout: home
title: Hardware Engineer
body_class: is-home
description: Anubhav Saini — 5th-year Engineering Physics at UBC. Electronics Hardware Intern at Kardium. PCB design, embedded systems, robotics, and power electronics.
---

<section class="hero" id="top">
  <div class="hero__media" aria-hidden="true">
    <img src="{{ '/docs/assets/TopLayer.png' | relative_url }}" alt="">
  </div>
  <div class="hero__veil" aria-hidden="true"></div>
  <div class="hero__grid" aria-hidden="true"></div>

  <div class="container hero__content">
    <p class="eyebrow reveal">5th Year Engineering Physics · UBC · Hardware</p>
    <h1 class="reveal reveal-delay-1">Anubhav Saini</h1>
    <p class="lede reveal reveal-delay-2">
      Electronics Hardware Intern at Kardium. I take systems from architecture and schematic
      through layout, bring-up, and measured validation — medical PCBs, power, sensing, and test.
    </p>
    <div class="btn-row reveal reveal-delay-3">
      <a class="btn btn--primary" href="#work">View work</a>
      <a class="btn btn--ghost" href="{{ '/docs/assets/Resume%20-%20Anubhav%20Saini.pdf' | relative_url }}" target="_blank" rel="noopener">Resume</a>
    </div>
    <div class="hero__meta reveal reveal-delay-3">
      <div>
        Currently
        <strong>Electronics HW Intern · Kardium</strong>
      </div>
      <div>
        Previously
        <strong>Arlo · Sarcomere</strong>
      </div>
      <div>
        Graduating
        <strong>May 2027</strong>
      </div>
    </div>
  </div>
</section>

<section class="section section--ink" id="work">
  <div class="container">
    <div class="section__head reveal">
      <p class="eyebrow">Selected work</p>
      <h2>Projects with measurable impact</h2>
      <p class="lede">Medical-grade PCBs, panel-level power electronics, consumer camera power-ORing, and sensing — click through for architecture, boards, and results.</p>
    </div>

    <div class="project-mosaic">
      <a class="project-tile project-tile--featured reveal" href="{{ '/Kardium/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/Kardium3D_Top.png' | relative_url }}" alt="3D render of the Kardium Cronus Handle Board Gen 2">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">01 / Kardium Inc.</span>
          <h3>Medical-Grade PCB Design</h3>
          <p>End-to-end 2nd-gen 6-layer production PCB — fab rules, mixed HV/LV layout, system interfaces, and flash test jig — plus flex and 12-layer validation.</p>
          <ul class="tag-row">
            <li>Medical PCB</li>
            <li>HIPOT</li>
            <li>IPC Class 3</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile project-tile--flip project-tile--diagram reveal" href="{{ '/SolarExpress/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/solar-express-system-diagram.png' | relative_url }}" alt="Solar Express panel-level DC power optimizer system diagram">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">02 / Personal</span>
          <h3>Solar Express</h3>
          <p>600W panel-level DC power optimizer — 4-switch GaN buck-boost, 99%+ pass-through efficiency, and NEC 690.12 rapid shutdown.</p>
          <ul class="tag-row">
            <li>GaN</li>
            <li>Buck-Boost</li>
            <li>MPPT</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile reveal" href="{{ '/ArloCamera/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/USB_PowerCircuitry.png' | relative_url }}" alt="Arlo Power-ORing switch circuitry">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">03 / Arlo Technologies</span>
          <h3>Power-ORing Switch</h3>
          <p>Discrete FW + HW Power-ORing switch at 98% efficiency — charges from the best available source with transistor/diode HV input logic.</p>
          <ul class="tag-row">
            <li>Power-ORing</li>
            <li>MOSFET</li>
            <li>98% eff.</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <div class="project-grid-2">
        <a class="project-tile reveal" href="{{ '/SarcoSensor/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/force sensor4.png' | relative_url }}" alt="Fingertip magnetic force sensor">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">04 / Sarcomere Dynamics</span>
            <h3>Fingertip Magnetic Force Sensor</h3>
            <p>Magnet + MLX90393 force pipeline for normal force and shear direction at &gt;90% accuracy — 5–10× cheaper than off-the-shelf.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>

        <a class="project-tile reveal" href="{{ '/SarcoPCB/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="Motor control PCB">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">05 / Sarcomere Dynamics</span>
            <h3>BLDC Motor Control PCB</h3>
            <p>Altium multi-layer board with STM32F412, motor driver, magnetometer, and CAN for a scalable robot-arm ECU network.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>
      </div>

      <div class="project-grid-2">
        <a class="project-tile reveal" href="{{ '/MetalMario/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/MarioKart.png' | relative_url }}" alt="Metal Mario autonomous robot car">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">06 / Robotics</span>
            <h3>Metal Mario</h3>
            <p>STM32 autonomous race car with IMU + encoder localization and PID path following — fastest lap by 4 seconds.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>

        <a class="project-tile reveal" href="{{ '/MicrochipMultithread/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/MicrochipLab.png' | relative_url }}" alt="Multithreaded test routine lab setup">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">07 / Microchip</span>
            <h3>SERDES Multithreaded Test</h3>
            <p>Python + firmware characterization flow that cut SERDES I3C pad test time by &gt;40% and power by 15%.</p>
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
        I'm a 5th-year Engineering Physics student at UBC (graduating May 2027), specializing in electrical engineering and robotics.
        Right now I'm an Electronics Hardware Intern at <strong>Kardium</strong> in Burnaby.
      </p>
      <p class="muted">
        Previously at Arlo and Sarcomere Dynamics (and earlier Microchip), I've owned power-ORing architectures,
        sensor firmware, motor-control PCBs, and mixed-signal characterization — always with hard numbers attached.
      </p>
      <dl class="skill-bands">
        <div class="skill-band">
          <dt>Hardware</dt>
          <dd>PCB design (Altium), medical / HV layout, power management, sensor systems, STM32, ADC / UART / I2C / SPI / CAN</dd>
        </div>
        <div class="skill-band">
          <dt>Software</dt>
          <dd>C/C++, Python, embedded firmware, PlatformIO, MATLAB, ROS, OpenCV, TensorFlow, Linux</dd>
        </div>
        <div class="skill-band">
          <dt>Interests</dt>
          <dd>Medical devices · Robotics · Aerospace · Automotive · Consumer electronics</dd>
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
        <p class="lede">Open to hardware, firmware, and robotics full-time roles and conversations for 2027.</p>
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
