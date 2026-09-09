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

  <div class="container hero__layout">
    <div class="hero__intro">
      <p class="eyebrow reveal">5th Year Engineering Physics · UBC · Hardware</p>
      <h1 class="reveal reveal-delay-1">Anubhav Saini</h1>
      <p class="lede reveal reveal-delay-2">
        Electronics Hardware Intern at Kardium. I take systems from architecture and schematic
        through layout, bring-up, and measured validation — medical PCBs, power, sensing, and test.
      </p>
      <div class="btn-row reveal reveal-delay-3">
        <a class="btn btn--primary" href="#work">View work</a>
        <a class="btn btn--ghost" href="{{ '/docs/assets/AnubhavSaini_Resume.pdf' | relative_url }}" target="_blank" rel="noopener">Resume</a>
      </div>
    </div>

    <aside class="hero-timeline reveal reveal-delay-3" aria-label="Internship timeline">
      <p class="hero-timeline__label">Path</p>
      <ol>
        <li class="is-now">
          <a href="#kardium">
            <span class="hero-timeline__when">2026</span>
            <span class="hero-timeline__who">Kardium</span>
            <span class="hero-timeline__what">Electronics Hardware Engineering Intern</span>
          </a>
        </li>
        <li>
          <a href="#arlo">
            <span class="hero-timeline__when">2025</span>
            <span class="hero-timeline__who">Arlo Technologies</span>
            <span class="hero-timeline__what">Hardware Engineering Intern</span>
          </a>
        </li>
        <li>
          <a href="#sarcomere">
            <span class="hero-timeline__when">2024</span>
            <span class="hero-timeline__who">Sarcomere Dynamics</span>
            <span class="hero-timeline__what">Electrical Engineering Intern</span>
          </a>
        </li>
        <li>
          <a href="#microchip">
            <span class="hero-timeline__when">2024</span>
            <span class="hero-timeline__who">Microchip</span>
            <span class="hero-timeline__what">Product Engineering Intern</span>
          </a>
        </li>
      </ol>
    </aside>
  </div>
</section>

<section class="section section--ink" id="work">
  <div class="container">
    <div class="section__head reveal">
      <p class="eyebrow">Highlighted</p>
      <h2>Three boards that define the loop</h2>
      <p class="lede">Production medical PCB, consumer camera power, and a robot-arm motor controller — the work I want a recruiter to open first.</p>
    </div>

    <div class="highlight-stack">
      <a class="project-tile project-tile--featured reveal" href="{{ '/Kardium/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/Kardium3D_Top.png' | relative_url }}" alt="3D render of the Kardium Cronus Handle Board Gen 2">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">01 / Kardium</span>
          <h3>Medical-Grade PCB Design</h3>
          <p>2nd-gen 6-layer production board — DFM vendor transition, 16HV + 16LV across 8 channels plus flash, HIPOT, and a matched-impedance flash/SPI test jig.</p>
          <ul class="tag-row">
            <li>Medical PCB</li>
            <li>HIPOT</li>
            <li>IPC Class 3</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile project-tile--flip reveal" href="{{ '/ArloCamera/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/arlo-power-oring-bringup.jpg' | relative_url }}" alt="Arlo Power-ORing switch live test bench">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">02 / Arlo</span>
          <h3>Power-ORing Switch</h3>
          <p>Firmware plus fallback hardware so the camera picks supply, external solar, or embedded solar — MOSFET/diode analog control at &gt;98% efficiency.</p>
          <ul class="tag-row">
            <li>Power-ORing</li>
            <li>MOSFET</li>
            <li>&gt;98% eff.</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile project-tile--featured reveal" href="{{ '/SarcoPCB/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/MotorControlPCB.png' | relative_url }}" alt="BLDC motor control PCB">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">03 / Sarcomere</span>
          <h3>BLDC Motor Control PCB</h3>
          <p>Altium multi-layer ECU — STM32F412, motor driver, magnetometer, and CAN for a scalable robot-arm network.</p>
          <ul class="tag-row">
            <li>Altium</li>
            <li>STM32</li>
            <li>CAN</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>
    </div>
  </div>
</section>

<section class="section section--ink section--tight" id="experience">
  <div class="container">
    <div class="section__head reveal">
      <p class="eyebrow">By internship</p>
      <h2>The rest of the bench work</h2>
      <p class="lede">Each company from the path, then the projects that sit beside the three highlights.</p>
    </div>

    <article class="work-group reveal" id="kardium">
      <header class="work-group__head">
        <div>
          <p class="work-group__co">Kardium Inc.</p>
          <p class="work-group__role">Electronics Hardware Engineering Intern</p>
        </div>
        <p class="work-group__when">Jan — Aug 2026</p>
      </header>
      <div class="work-group__grid">
        <a class="project-tile project-tile--flip reveal" href="{{ '/KardiumTesting/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/rfs-cardcage.jpg' | relative_url }}" alt="OneBox RF Switch in the card cage with SOM installed">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">Also / Kardium</span>
            <h3>RF Switch System Validation</h3>
            <p>Owned the full test loop on the OneBox RF Switch — 17 tests across 8 suites — then left the framework the rest of the 11+ board ecosystem still uses.</p>
            <ul class="tag-row">
              <li>Power</li>
              <li>SI</li>
              <li>Relays</li>
            </ul>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>

        <a class="project-tile reveal" href="{{ '/Amplink/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/PMIC1.jpg' | relative_url }}" alt="PMIC programming bench">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">Also / Kardium</span>
            <h3>AmPLink · PMIC Programming System</h3>
            <p>USB production programmer for processor/SOM flash and a TPS65400 I2C bench — chip-type detect (FT4232H vs FT2232H), R2R board-ID via ADS7142, and fail-safe DS4520 hold so rails stay off until the mapped image programs.</p>
            <ul class="tag-row">
              <li>PMIC</li>
              <li>PMBus</li>
              <li>FTDI</li>
              <li>I2C / SPI</li>
            </ul>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>
      </div>
    </article>

    <article class="work-group reveal" id="arlo">
      <header class="work-group__head">
        <div>
          <p class="work-group__co">Arlo Technologies</p>
          <p class="work-group__role">Hardware Engineering Intern</p>
        </div>
        <p class="work-group__when">May — Dec 2025</p>
      </header>
      <div class="work-group__grid">
        <a class="project-tile reveal" href="{{ '/ArloCamera/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/arlo-power-oring-bringup.jpg' | relative_url }}" alt="Arlo Power-ORing switch live test bench">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">Also / Arlo</span>
            <h3>Power-ORing Switch</h3>
            <p>Firmware plus fallback hardware so the camera picks supply, external solar, or embedded solar — MOSFET/diode analog control at &gt;98% efficiency.</p>
            <ul class="tag-row">
              <li>Power-ORing</li>
              <li>MOSFET</li>
              <li>&gt;98% eff.</li>
            </ul>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>
      </div>
    </article>

    <article class="work-group reveal" id="sarcomere">
      <header class="work-group__head">
        <div>
          <p class="work-group__co">Sarcomere Dynamics</p>
          <p class="work-group__role">Electrical Engineering Intern</p>
        </div>
        <p class="work-group__when">Sep — Dec 2024</p>
      </header>
      <div class="work-group__grid">
        <a class="project-tile project-tile--flip reveal" href="{{ '/SarcoSensor/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/force sensor4.png' | relative_url }}" alt="Fingertip magnetic force sensor">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">Also / Sarcomere</span>
            <h3>Fingertip Magnetic Force Sensor</h3>
            <p>Magnet + MLX90393 — K-means-verified Bx/By/Bz mapping, pseudoinverse shear, &gt;90% accuracy, 5–10× cheaper than catalog.</p>
            <ul class="tag-row">
              <li>MLX90393</li>
              <li>Firmware</li>
              <li>Sensing</li>
            </ul>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>
      </div>
    </article>

    <article class="work-group reveal" id="microchip">
      <header class="work-group__head">
        <div>
          <p class="work-group__co">Microchip Technology</p>
          <p class="work-group__role">Product Engineering Intern</p>
        </div>
        <p class="work-group__when">May — Aug 2024</p>
      </header>
      <div class="work-group__grid">
        <a class="project-tile reveal" href="{{ '/MicrochipMultithread/' | relative_url }}">
          <div class="project-tile__media">
            <img src="{{ '/docs/assets/MicrochipLab.png' | relative_url }}" alt="Multithreaded SERDES test lab setup">
          </div>
          <div class="project-tile__body">
            <span class="project-tile__index">Also / Microchip</span>
            <h3>SERDES Multithreaded Test</h3>
            <p>Python + firmware characterization that cut SERDES I3C pad test time by &gt;40% and power by 15%.</p>
            <ul class="tag-row">
              <li>Python</li>
              <li>SERDES</li>
              <li>VT corners</li>
            </ul>
            <span class="project-tile__cta">Open project</span>
          </div>
        </a>
      </div>
    </article>
  </div>
</section>

<section class="section section--paper" id="personal">
  <div class="container">
    <div class="section__head reveal">
      <p class="eyebrow">Personal projects</p>
      <h2>Built outside a company badge</h2>
      <p class="lede">Power electronics and robotics I designed, simulated, or raced on my own time.</p>
    </div>

    <div class="project-grid-2">
      <a class="project-tile project-tile--diagram reveal" href="{{ '/SolarExpress/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/solar-express-system-diagram.png' | relative_url }}" alt="Solar Express panel-level DC power optimizer system diagram">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">Personal</span>
          <h3>Solar Express</h3>
          <p>600W panel-level DC optimizer — 4-switch GaN buck-boost, 99%+ pass-through, NEC 690.12 rapid shutdown.</p>
          <ul class="tag-row">
            <li>GaN</li>
            <li>Buck-Boost</li>
            <li>MPPT</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>

      <a class="project-tile reveal" href="{{ '/MetalMario/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/MarioKart.png' | relative_url }}" alt="Metal Mario autonomous robot car">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">Personal</span>
          <h3>Metal Mario</h3>
          <p>STM32 race car with IMU + encoder localization and PID path following — fastest lap by 4 seconds.</p>
          <ul class="tag-row">
            <li>STM32</li>
            <li>PID</li>
            <li>Localization</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>
    </div>

    <div class="personal-follow">
      <a class="project-tile project-tile--flip reveal" href="{{ '/MLrobot/' | relative_url }}">
        <div class="project-tile__media">
          <img src="{{ '/docs/assets/MLRobot.png' | relative_url }}" alt="Machine learning detective robot in simulation">
        </div>
        <div class="project-tile__body">
          <span class="project-tile__index">Personal</span>
          <h3>ML Detective Robot</h3>
          <p>ROS/Gazebo autonomous car that reads visual clues with a CNN — character recognition above 98%, wired into the robot through publisher/subscriber control.</p>
          <ul class="tag-row">
            <li>CNN</li>
            <li>ROS</li>
            <li>Gazebo</li>
          </ul>
          <span class="project-tile__cta">Open project</span>
        </div>
      </a>
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
        <a href="{{ '/docs/assets/AnubhavSaini_Resume.pdf' | relative_url }}" target="_blank" rel="noopener"><span>Resume PDF</span><span>→</span></a>
      </div>
    </div>
  </div>
</section>
