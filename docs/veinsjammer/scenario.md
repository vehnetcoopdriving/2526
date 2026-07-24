---
title: Scenario
parent: Veins Jammer
nav_order: 2
---

# Scenario

## Network Setup

The project extends the standard **VEINS 5.3.1 RSU example** to evaluate the impact of a reactive jammer in an IEEE 802.11p Vehicular Ad Hoc Network (VANET).

The simulation combines:

* **SUMO** for vehicle mobility management;
* **OMNeT++** for network simulation;
* **VEINS** for IEEE 802.11p communication.

The scenario includes:

* **Vehicles**, dynamically created through the TraCI interface and running the standard `TraCIDemo11p` application.
* **Legitimate RSU**, providing normal Road Side Unit communication through `TraCIDemoRSU11p`.
* **Jammer RSU**, a stationary node equipped with the custom `JammerApplication`.

The simulation area is **3200 m × 3200 m**.

![Simulation topology]({{ "/assets/images/simulation1.png" | relative_url }})

Node positions:

| Node | Position |
| ---- | -------- |
| Legitimate RSU | (2000 m, 2000 m, 3 m) |
| Jammer RSU | (2050 m, 2050 m, 3 m) |

---

## Simulation Parameters

Each simulation run lasts **200 seconds**.

During execution:

1. SUMO updates vehicle mobility.
2. TraCI manages dynamic vehicle creation.
3. OMNeT++ simulates wireless communication events.
4. Results are stored in the standard OMNeT++ output files.

The scenario is evaluated with different jammer configurations to measure the impact of interference on IEEE 802.11p communication performance.

---

## Jammer Configuration

The jammer parameters are defined in `omnetpp.ini`:

| Parameter | Default value | Description |
| --------- | ------------- | ----------- |
| `enabled` | `true` | Enables or disables the jammer. |
| `jammingDuration` | `0.02 s` | Duration of a jamming burst. |
| `jammingPower` | `0.1 W` | Transmission power of the jammer. |
| `jamChannel` | `178` | IEEE 802.11p channel used for jamming. |

These parameters allow different attack configurations to be tested without modifying the source code.