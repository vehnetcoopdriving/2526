---
title: Assignment Goal
parent: Veins Jammer
nav_order: 1
---

# Assignment Goal

## Objectives

The objective of this assignment is to design and implement a **reactive jamming attack** within a Vehicular Ad Hoc Network (VANET) simulated using **VEINS 5.3.1**, **OMNeT++**, and **SUMO**. The project extends the standard VEINS example by introducing a malicious Road Side Unit (RSU) capable of selectively interfering with IEEE 802.11p communications between legitimate vehicles.

Unlike a constant jammer, which continuously transmits interference, the implemented attacker should remain silent until wireless activity is detected. This models a more realistic adversary that consumes less energy and is more difficult to identify.

---

## Starting Point

![Simulation topology]({{ "/assets/images/sumo.png" | relative_url }})

*Figure 1. Sumo standard example*

The implementation should begin from the standard VEINS example described in the [official Veins tutorial](https://veins.car2x.org/tutorial/#finish).

This example provides the baseline vehicular network scenario, including:

* vehicle mobility managed by SUMO;
* dynamic node creation through TraCI;
* IEEE 802.11p communication stack;
* Road Side Unit (RSU) infrastructure;
* application-layer examples for vehicles and RSUs.

The reactive jammer should be developed by extending this baseline scenario without modifying the VEINS framework itself.

---

## Core Tasks

### 1. Create a Malicious RSU

Extend the original network by adding a dedicated Road Side Unit that behaves as a malicious node. This **RSU-jam** should use the standard VEINS IEEE 802.11p communication stack while executing a custom jamming application.

---

### 2. Develop a Custom Jammer Application

Implement a new application-layer module responsible for the jammer behaviour.

The application should:

* inherit from the VEINS application framework;
* initialize configurable jamming parameters;
* interact with the IEEE 802.11p MAC layer;
* manage timers and internal jammer state;
* collect statistics during the simulation.

The implementation should remain modular so that different jamming strategies can easily be added in the future.

---

### 3. Implement a Reactive Jamming Strategy

The jammer should implement a **reactive** attack rather than continuously transmitting interference.

The application is expected to:

* monitor wireless channel activity by subscribing to MAC-layer channel busy notifications;
* detect transmissions in real time;
* wait for a configurable reaction delay;
* generate an interference packet;
* transmit the interference burst for a configurable duration;
* return to the idle state and wait for the next transmission.

---

## Expected Outcomes

At the end of the assignment, the implementation should provide:

* a new network scenario including a malicious RSU;
* a custom `JammerApplication` module implementing the reactive jamming logic;
* configurable attack parameters (reaction delay, burst duration, transmission power, and enable/disable flag);
* successful integration with the existing VEINS 5.3.1 framework;
* simulation statistics describing the jammer behaviour, including the number of detected transmissions and jamming activations.

The completed project should allow experiments to evaluate how a reactive jammer affects IEEE 802.11p vehicular communications while preserving compatibility with the original VEINS architecture.
