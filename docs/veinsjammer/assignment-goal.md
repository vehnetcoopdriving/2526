---
title: Assignment Goal
parent: Veins Jammer
nav_order: 1
---

# Assignment Goal

## Objectives

The main goal of this assignment is to implement a reactive jamming attack in a vehicular network simulation environment. Students will extend the baseline Veins scenario to introduce a malicious Road Side Unit (RSU) capable of disrupting vehicle-to-vehicle (V2V) communications.

### Starting Point

Begin with the basic Veins scenario as documented in the [official Veins tutorial](https://veins.car2x.org/tutorial/#finish). This provides the foundation for vehicular network simulation with SUMO traffic simulation and OMNeT++ network simulation.

### Core Tasks

1. **Model a Jamming RSU**: Design and implement a new Road Side Unit (RSU-jam) that acts as a malicious network entity capable of disrupting wireless communications in its vicinity.

2. **Develop Custom Application**: Create a new application layer protocol for the RSU-jam. This application must be developed from scratch by students and will implement the jamming behavior.

3. **Implement Reactive Jamming Strategy**: The jamming application should implement a triggered jamming approach rather than a naive constant noise generation. Specifically:
   - Subscribe to physical layer events to monitor the wireless channel
   - Detect ongoing transmissions in real-time
   - React immediately by transmitting interference signals to disrupt legitimate communications
   - This reactive approach is more sophisticated and realistic than continuous jamming, as it conserves energy and is harder to detect

### Implementation Guidance

The recommended approach is to design the RSU-jam application to listen for transmission events on the physical channel. When a transmission is detected, the jammer should immediately initiate its own transmission to interfere with the legitimate signal. This creates a triggered jammer that responds to network activity rather than blindly generating constant interference.

## Expected Outcomes

What are the expected outcomes and deliverables for this project?
