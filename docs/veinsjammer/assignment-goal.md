---
title: Assignment Goal
parent: Veins Jammer
nav_order: 1
---

# Assignment Goal

## Objectives

The goal of this project is to design and implement a **reactive jamming attack** in a Vehicular Ad Hoc Network (VANET) using **VEINS 5.3.1**, **OMNeT++**, and **SUMO**.

Starting from the standard VEINS example, the project adds a malicious Road Side Unit (RSU) that selectively interferes with IEEE 802.11p communications between vehicles.

Unlike a constant jammer, the reactive jammer remains silent until it detects activity on the wireless channel. It then transmits a short interference burst before returning to the idle state. This behavior makes the attacker more efficient and less detectable.

---

## Starting Point

![Simulation topology]({{ "/assets/images/sumo.png" | relative_url }})

*Figure 1. Standard VEINS scenario.*

The implementation is based on the standard VEINS example presented in the [official Veins tutorial](https://veins.car2x.org/tutorial/#finish).

The example already provides:

- vehicle mobility managed by SUMO;
- dynamic vehicle creation through TraCI;
- an IEEE 802.11p communication stack;
- Road Side Units (RSUs);
- example applications for vehicles and RSUs.

The reactive jammer is added by extending this scenario without modifying the VEINS framework.

---

## Core Tasks

### 1. Add a Malicious RSU

Extend the network by adding a new Road Side Unit that acts as a jammer. The node uses the standard IEEE 802.11p protocol stack and runs a custom jamming application.

---

### 2. Implement a Jammer Application

Develop a new application-layer module that:

- extends the VEINS application framework;
- loads configurable jamming parameters;
- interacts with the IEEE 802.11p MAC layer;
- manages timers and the jammer state;
- collects simulation statistics.

The implementation should remain modular so that other jamming strategies can be added easily.

---

### 3. Implement Reactive Jamming

The jammer should transmit only when wireless activity is detected.

The application should:

- monitor channel activity through MAC-layer busy notifications;
- detect ongoing transmissions;
- wait for a configurable reaction delay;
- transmit an interference packet for a configurable duration;
- return to the idle state and wait for the next transmission.

---

## Expected Outcomes

At the end of the project, the implementation should provide:

- a VEINS scenario including a malicious RSU;
- a custom `JammerApplication` implementing the reactive jamming logic;
- configurable attack parameters, including reaction delay, burst duration, transmission power, and an enable/disable option;
- full compatibility with the VEINS 5.3.1 framework;
- simulation statistics such as the number of detected transmissions and jammer activations.

The completed project enables experiments to evaluate the impact of reactive jamming on IEEE 802.11p vehicular communications while preserving the original VEINS architecture.