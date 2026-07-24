---
title: Assignment Goal
parent: Veins Jammer
nav_order: 1
---

# Assignment Goal

## Overview

The objective of this project is to design and implement a **reactive jamming attack** against IEEE 802.11p communications in a Vehicular Ad Hoc Network (VANET) using **VEINS 5.3.1**, **OMNeT++**, and **SUMO**.

The implementation extends the standard VEINS example scenario by introducing a malicious Road Side Unit (RSU) capable of selectively interfering with wireless communications between vehicles.

Unlike a traditional constant jammer, which continuously occupies the wireless channel, the proposed jammer follows a **reactive strategy**:

1. It monitors wireless activity at the physical layer.
2. It detects the beginning of legitimate wireless transmissions.
3. It immediately generates a short interference burst.
4. It returns to an idle state until new activity is detected.

This approach reduces unnecessary channel occupation while maintaining an effective attack capability.

---

## Starting Point

![Simulation topology]({{ "/assets/images/sumo.png" | relative_url }})

*Figure 1. Standard VEINS scenario.*

The project is based on the official VEINS tutorial scenario, which already provides the main components required for VANET simulation:

* vehicle mobility controlled by SUMO through TraCI;
* IEEE 802.11p communication stack;
* Road Side Units (RSUs);
* example vehicle and RSU applications.

The existing architecture is extended with:

* a new malicious RSU node;
* a custom `JammerApplication`;
* additional PHY-layer mechanisms for detecting incoming transmissions and generating interference signals.

The original VEINS communication stack is preserved, with modifications limited to the components required to support reactive jamming.

---

## Project Objectives

The implementation has four main objectives.

### 1. Deploy a Malicious RSU

A new stationary RSU is added to the simulation scenario. The node uses the standard IEEE 802.11p stack but runs a custom application responsible for controlling the jamming behaviour.

The jammer operates as a network participant while generating interference at the physical layer rather than transmitting normal application packets.

---

### 2. Extend the IEEE 802.11p PHY Layer

The standard VEINS physical layer is extended with additional functionality required for reactive detection.

The PHY layer is modified to:

* generate a notification when a new wireless frame starts reception;
* distinguish legitimate transmissions from jammer-generated signals;
* provide an interface for creating artificial interference signals.

These extensions allow the jammer application to react directly to wireless channel activity without modifying the MAC layer.

---

### 3. Implement the Jammer Application

A dedicated `JammerApplication` module is developed to manage the attack logic.

The application is responsible for:

* subscribing to PHY-layer reception events;
* loading configurable attack parameters;
* maintaining the jammer state;
* scheduling jamming start and stop events;
* controlling the PHY-layer interference generation.

The application is designed to remain modular, allowing additional attack strategies to be added in the future.

---

### 4. Implement Reactive Jamming

The jammer follows an event-driven workflow:

1. A legitimate IEEE 802.11p transmission begins.
2. The PHY layer detects the incoming frame.
3. An `incomingFrame` notification is emitted.
4. `JammerApplication` receives the event.
5. If the jammer is enabled and inactive, a jamming burst is started.
6. The PHY layer injects an interference signal into the wireless channel.
7. After the configured duration, the jammer returns to the idle state.

Jammer-generated signals are excluded from the detection mechanism to prevent self-triggering and continuous activation.

---

## Expected Results

The completed implementation provides:

* a VEINS scenario containing a malicious RSU;
* a reactive `JammerApplication`;
* PHY-layer support for transmission detection and interference generation;
* configurable attack parameters:
  * enable/disable option;
  * jamming duration;
  * transmission power;
  * operating channel;
* compatibility with VEINS 5.3.1;
* simulation logs and statistics describing jammer activity and communication degradation.

The final system enables the evaluation of PHY-layer reactive jamming effects on IEEE 802.11p vehicular communications while maintaining compatibility with the existing VEINS simulation framework.