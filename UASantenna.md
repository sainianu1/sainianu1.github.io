---
layout: project
title: UAS Antenna Tracking System
heading: UAS Antenna Tracker
permalink: /UASantenna/
cover: /docs/assets/UasAntenna.png
eyebrow: UBC Uncrewed Aircraft Systems · RF / Systems
role: Electrical · UBC UAS
timeline: Team project
summary: Antenna tracking system for high-bandwidth video downlink from an unmanned aircraft — up to 200 Mbps at a nominal 750 m link.
tags:
  - RF
  - Tracking
  - Systems
metrics:
  - value: "200 Mbps"
    label: "Video downlink target"
  - value: "750 m"
    label: "Nominal range"
---

<p class="section-label">Context</p>
## The problem

UBC UAS needed a ground-side **antenna tracking system** that could maintain a high-rate video link with an airborne platform — targeting up to **200 Mbps** at a nominal distance of **750 m**.

<figure>
  <img src="{{ '/docs/assets/UasAntenna.png' | relative_url }}" alt="UAS antenna tracking system">
  <figcaption>Antenna tracker hardware</figcaption>
</figure>

<p class="section-label">Scope</p>
## Role in the stack

This project sits alongside the UAS buck converter as part of the team's electrical / RF system. The tracker keeps the air-to-ground video pipe locked while the aircraft moves through its mission envelope — pointing, RF chain, and link reliability under motion.
