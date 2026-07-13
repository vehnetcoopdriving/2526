---
title: Implementation
parent: Platoon splitting
nav_order: 3
---

# Implementation

The implementation is distributed across the application and scenario layers of the Plexe framework, while the simulation environment expose customizable variables and enable the recording of output vectors

## Code Structure

The GettingStartedScenario.cc module implementation is centered around two primary methods. The initialize() method establishes the initial kinematic states, assigns base cruising speeds, and schedules the maneuver triggers. The handleMessage() method serves as the central event dispatcher. It actively manages a continuous radar polling loop that monitors the spatial gap to the preceding vehicle in real time. Once the target safety distance is achieved and with the leader authorization, the vehicle's longitudinal controller changes from cooperative adaptive cruise control (CACC) to standard adaptive cruise control (ACC).

The network application handles the logical hierarchy of the platoon. Upon a separation event, it is responsible for dividing the original formation array into two independent matrices. It manages the hierarchical propagation of the new formation data to the sub-followers, ensuring that every vehicle safely reconfigure its controller parameters to point to the new sub-leader.

The simulation environment and physical constraints (such as deceleration severity, trigger timings, and spatial target gaps) are fully parameterized through the .ned file definitions and mapped in the omnetpp.ini runtime configuration. This architecture enables extensive simulation testing and scenario customization without the need to recompile the C++ source code.


## Key Features

Radar-Driven Controller Transition: A continuous feedback loop in the scenario layer that autonomously downgrades the vehicle's longitudinal controller from cooperative (CACC) to standard adaptive (ACC) based on real-time spatial gap measurements.

Dynamic Formation Splitting: On-the-fly division of the platoon matrix at the application layer, ensuring correct sub-leader election and safe radio parameter reconfiguration for the followers.

V2V Authorization Handshake: A request-response communication protocol ensuring that the splitting vehicle obtains explicit permission from the original platoon leader before altering kinematics or forming a new sub-platoon (GUI-only).

Active Safety Stress-Testing: Programmable fault injections (e.g., sudden emergency braking by the old leader) executed via scenario timers to evaluate the collision avoidance capabilities and kinematic stability of the newly formed sub-platoon.