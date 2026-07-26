---
layout: home
title: Hardware Engineer
body_class: is-home
description: Anubhav Saini — 5th-year Engineering Physics at UBC. Hardware Engineering Intern at Arlo. PCB design, embedded systems, robotics, and power electronics.
---

<section class="hero" id="top">
  <div class="hero__media" aria-hidden="true">
    <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="">
  </div>
  <div class="hero__veil" aria-hidden="true"></div>
  <div class="hero__grid" aria-hidden="true"></div>

  <div class="container hero__content">
    <p class="eyebrow reveal">5th Year Engineering Physics · UBC · Hardware</p>
    <h1 class="reveal reveal-delay-1">Anubhav Saini</h1>
    <p class="lede reveal reveal-delay-2">
      Hardware Engineering Intern at Arlo. I take systems from architecture and schematic
      through layout, bring-up, and measured validation — power, sensing, motor control, and test.
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
        <strong>Sarcomere · Microchip · Cloverdale</strong>
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
      <p class="lede">Consumer camera power systems, force sensing, motor-control PCBs, and mixed-signal test — click through for architecture, boards, and results.</p>
    </div>

    <div class="project-mosaic">
      <a class="project-tile project-tile--featured reveal" href="{{ '/ArloCamera/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/USB_PowerCircuitry.png' | relative_url }}" alt="Arlo camera power circuitry">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">01 / Arlo Technologies</span>
          <h3>Solar Camera Power &amp; HW Validation</h3>
          <p>Led power architecture for a new solar-powered camera, cut PIR yield loss from 30% to &lt;1%, and expanded ALS test coverage to 100%.</p>
          <ul class="tag-row">
            <li>Power</li>
            <li>RF Debug</li>
            <li>Validation</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile project-tile--flip reveal" href="{{ '/SarcoSensor/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/force sensor4.png' | relative_url }}" alt="Fingertip magnetic force sensor">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">02 / Sarcomere Dynamics</span>
          <h3>Fingertip Magnetic Force Sensor</h3>
          <p>Built a magnet + MLX90393 force pipeline that outputs normal force and shear direction at &gt;90% accuracy — 5–10× cheaper than off-the-shelf.</p>
          <ul class="tag-row">
            <li>Sensors</li>
            <li>Firmware</li>
            <li>Python</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile reveal" href="{{ '/SarcoPCB/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="Motor control PCB">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">03 / Sarcomere Dynamics</span>
          <h3>BLDC Motor Control PCB</h3>
          <p>Altium multi-layer board with STM32F412, motor driver, magnetometer, and CAN — designed for a scalable robot-arm ECU network.</p>
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
            <p>STM32 autonomous race car with IMU + encoder localization (&gt;85% accuracy) and PID path following — fastest lap by 4 seconds.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>

        <a class="project-tile reveal" href="{{ '/MLrobot/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/MLRobot.png' | relative_url }}" alt="Machine learning robot detective">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">05 / ML + Robotics</span>
            <h3>ML Detective Robot</h3>
            <p>ROS/Gazebo autonomous car with CNN character recognition at &gt;98% accuracy and publisher/subscriber control loops.</p>
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
            <span class="project-tile__index">06 / Microchip</span>
            <h3>SERDES Multithreaded Test</h3>
            <p>Python + firmware characterization flow that cut SERDES I3C pad test time by &gt;40% and power by 15% across VT corners.</p>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>

        <a class="project-tile reveal" href="{{ '/UasBuckConvertor/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/UASBuck.png' | relative_url }}" alt="Buck converter circuit">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">07 / UBC UAS</span>
            <h3>60V → 5V Buck Converter</h3>
            <p>Central power stage for uncrewed aircraft — TPS54560-based Altium design stepping 60V down to 5V / 5A.</p>
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
        Right now I'm a Hardware Engineering Intern at Arlo Technologies in Vancouver.
      </p>
      <p class="muted">
        Across Arlo, Sarcomere Dynamics, Microchip, and Cloverdale Robotics I've owned power architecture,
        sensor firmware, motor-control PCBs, and mixed-signal characterization — always with hard numbers attached.
      </p>
      <dl class="skill-bands">
        <div class="skill-band">
          <dt>Hardware</dt>
          <dd>PCB design (Altium), power management, sensor systems, STM32, ADC / UART / I2C / SPI / CAN</dd>
        </div>
        <div class="skill-band">
          <dt>Software</dt>
          <dd>C/C++, Python, embedded firmware, PlatformIO, MATLAB, ROS, OpenCV, TensorFlow, Linux</dd>
        </div>
        <div class="skill-band">
          <dt>Interests</dt>
          <dd>Robotics · Aerospace · Automotive · Consumer electronics · Edge AI</dd>
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
