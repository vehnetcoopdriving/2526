---
title: Assignment Goal
parent: Platoon splitting
nav_order: 1
---

# Assignment Goal

## Objectives

The main goal of this assignment is to implement an advanced platoon splitting maneuver in a vehicular platoon simulation environment. Students will extend the baseline Plexe scenario to enable the separation of a contiguous sub-platoon from an existing platoon, rather than just a single vehicle.

### Starting Point

Begin with Plexe Tutorial 7 - [Leave Maneuver](https://plexe.car2x.org/tutorial/example7/), which demonstrates how a single vehicle at the rear of a platoon can perform a leave maneuver and separate from the platoon. This provides the foundational framework for platoon management and vehicle coordination.

### Core Tasks

1. **Extend Single-Vehicle Separation to Sub-Platoon Separation**: Enhance the existing leave maneuver implementation to support the departure of multiple consecutive follower vehicles as a coordinated group. Instead of a single vehicle leaving, a contiguous sub-platoon must be able to split from the main platoon while maintaining formation among the departing vehicles.

2. **Implement Coordinated Maneuver Logic**: Design and implement the coordination protocol required for multiple vehicles to execute a synchronized splitting maneuver. This includes:
   - Identifying the splitting point within the platoon
   - Coordinating communication between vehicles in the splitting sub-platoon
   - Managing the transition from main platoon control to independent sub-platoon operation
   - Ensuring safe spacing and speed adjustments during the maneuver

3. **Parametrization and Configuration**: Make the splitting behavior fully configurable through the `omnetpp.ini` configuration file. Students should implement parameters to specify:
   - The index of the vehicle initiating the split (the first vehicle of the departing sub-platoon)
   - The number of vehicles in the splitting sub-platoon
   - Timing and safety parameters for the maneuver

### Implementation Guidance

The recommended approach is to analyze the existing single-vehicle leave maneuver implementation and extend it to handle multiple consecutive vehicles. Key considerations include:
- How to propagate the split decision through the sub-platoon
- How to maintain cohesion among splitting vehicles while decoupling from the main platoon
- How to handle edge cases (e.g., splitting at different positions in the platoon)
- How to ensure the maneuver is safe and realistic under various traffic conditions

## Expected Outcomes

What are the expected outcomes and deliverables for this project?
