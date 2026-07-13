---
title: Implementation
parent: Veins Jammer
nav_order: 3
---

# Implementation

## Code Structure

The reactive jammer was implemented starting from **VEINS 5.3.1**, extending the existing IEEE 802.11p application framework instead of modifying the lower networking layers. This approach keeps the implementation modular and allows the jammer to be integrated into existing VEINS scenarios with minimal changes.

The implementation is composed of the following files:

| File                    | Purpose                                                                                                                                                  |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `JammerScenario.ned`    | Extends the standard `RSUExampleScenario` by adding a dedicated jammer node.                                                                             |
| `JammerApplication.ned` | Declares the jammer application module, its configurable parameters, emitted signals, and recorded statistics.                                           |
| `JammerApplication.h`   | Defines the application interface, timers, internal state variables, counters, and helper methods.                                                       |
| `JammerApplication.cc`  | Implements the reactive jamming logic, event handling, statistics collection, and interaction with the IEEE 802.11p MAC layer.                           |
| `omnetpp.ini`           | Configures the simulation scenario, network parameters, jammer position, transmission power, reaction delay, burst duration, and other runtime settings. |

The jammer is implemented as an application-layer module derived from `DemoBaseApplLayer`. Consequently, it can reuse the existing VEINS communication stack while introducing custom behaviour only where needed.

---

## Jammer Scenario

The network description extends the original VEINS RSU scenario by introducing a dedicated jammer node.

The jammer is instantiated as an `RSU`, allowing it to use the existing IEEE 802.11p protocol stack without requiring additional modifications. The only difference is the application layer, which is replaced by `JammerApplication`.

The scenario configuration (`omnetpp.ini`) specifies:

* jammer position;
* transmission power;
* reaction delay;
* jamming duration;
* enable/disable flag.

This makes different experiments possible without recompiling the simulator.

---

## Jammer Application

The jammer is implemented as a reactive application that monitors wireless channel activity and transmits an interference packet whenever a legitimate transmission is detected.

During initialization the module:

* loads all configurable parameters;
* creates self-messages used to schedule jamming events;
* locates the IEEE 802.11p MAC layer;
* subscribes to MAC channel busy notifications;
* configures the desired transmission power.

Once initialized, the jammer remains idle until the MAC layer reports that the channel has become busy.

---

## Reactive Jamming Logic

The behaviour follows a simple event-driven workflow.

1. The MAC layer reports that the wireless channel becomes busy.
2. The jammer records the detection event.
3. A timer is scheduled according to the configured reaction delay.
4. When the timer expires, the jammer starts transmitting an interference frame.
5. The transmission lasts for the configured burst duration.
6. A second timer stops the jamming activity and the jammer returns to the idle state.

This behaviour models a **reactive jammer**, which only transmits after detecting legitimate network activity rather than continuously occupying the channel.

---

## MAC Layer Interaction

Instead of continuously monitoring incoming packets, the implementation relies on the `Mac1609_4::sigChannelBusy` signal emitted by the VEINS MAC layer.

By subscribing to this signal, the jammer is notified whenever the medium changes from idle to busy.

This approach provides several advantages:

* low computational overhead;
* no modifications to the MAC implementation;
* immediate acknowledgement of channel activity;
* compatibility with existing VEINS components.

The jammer also configures its transmission power directly through the MAC layer using the configurable `jammingPower` parameter.

---

## Interference Transmission

When activated, the jammer generates a broadcast IEEE 1609.4 frame named **"jammer interference"**.

The generated frame is configured with:

* Control Channel (CCH);
* broadcast destination address;
* configurable transmission power;
* configurable frame length;
* custom PSID value (`9999`) used only to identify jammer packets.

The frame is transmitted through the standard VEINS communication stack using the inherited `sendDown()` function.

---

## Configuration Parameters

The jammer behaviour can be modified entirely through `omnetpp.ini`.

The main parameters are:

| Parameter         | Description                                                 |
| ----------------- | ----------------------------------------------------------- |
| `enabled`         | Enables or disables the jammer.                             |
| `reactionDelay`   | Delay between transmission detection and jammer activation. |
| `jammingDuration` | Duration of the interference burst.                         |
| `jammingPower`    | Transmission power used while jamming.                      |

Because these parameters are configurable at runtime, multiple experiments can be performed without changing the source code.

---

## Statistics Collection

The implementation records several metrics during simulation.

Signals emitted by the application include:

* transmission detected;
* jammer activated;
* jammer stopped;
* jammer-to-transmitter distance (when available).

At the end of each simulation, additional scalar statistics are recorded:

* number of detected legitimate transmissions;
* number of jammer activations;
* configured reaction delay;
* configured jamming duration;
* configured transmission power.

These statistics can be analysed using the standard OMNeT++ result analysis tools.

---

## Modifications to the Original VEINS Applications

In addition to implementing the reactive jammer, minor modifications were made to the original `TraCIDemo11p` and `TraCIDemoRSU11p` applications. These changes ensure compatibility with the additional jammer traffic while preserving the original application behaviour.

### Vehicle Application (`TraCIDemo11p`)

The original implementation assumed that every received IEEE 802.11p frame was a `TraCIDemo11pMessage`. Since the reactive jammer transmits custom interference frames based on `BaseFrame1609_4`, directly casting every received frame to `TraCIDemo11pMessage` could lead to runtime errors.

To avoid this issue, a type check was introduced before processing received frames. Only valid `TraCIDemo11pMessage` packets are processed by the application, while jammer-generated interference frames are ignored.

As a result, vehicles continue to process legitimate traffic normally without attempting to interpret interference packets as application messages.

### Roadside Unit Application (`TraCIDemoRSU11p`)

The same modification was applied to the roadside unit application.

The original implementation directly cast every received frame to `TraCIDemo11pMessage`. A type check was added so that only legitimate application messages are processed, while interference frames generated by the jammer are discarded.

Apart from this validation step, the forwarding behaviour of the RSU remains unchanged.

### Motivation

The reactive jammer transmits generic IEEE 1609.4 broadcast frames instead of application-specific `TraCIDemo11pMessage` packets. Without validating the received frame type, the original VEINS applications would attempt to cast jammer packets to `TraCIDemo11pMessage`, resulting in invalid casts during simulation.

These modifications are limited to packet validation and do not alter the original routing, forwarding, or communication logic of the VEINS applications.


## Design Considerations

The implementation was designed with the following objectives:

* **Modularity** — implemented entirely as a new application module.
* **Configurability** — all relevant parameters are defined in `omnetpp.ini`.
* **Compatibility** — integrates with the existing VEINS 5.3.1 architecture without modifying the framework source code.
* **Extensibility** — additional jamming strategies (for example continuous instead of reactive) can be implemented by extending the application logic while keeping the same interface.