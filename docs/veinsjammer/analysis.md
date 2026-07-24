---
title: Analysis
parent: Veins Jammer
nav_order: 5
---

# Analysis

## Evaluation

The impact of the reactive jammer is evaluated by comparing two simulation configurations:

* **jammerActive=false**: baseline scenario without malicious interference.
* **jammerActive=true**: scenario with the reactive jammer enabled.

The evaluation considers two different packet-loss metrics collected at different network layers and locations:

* **`SNIRLostPackets` measured at the RSU**: evaluates losses caused by insufficient Signal-to-Noise-plus-Interference Ratio during physical-layer reception.
* **`RXTXLostPackets` measured at vehicles (cars)**: evaluates packets that fail during the complete transmission and reception process at the MAC layer.

Together, these metrics provide a complete view of the jammer impact: `SNIRLostPackets` shows the degradation introduced at the wireless channel level, while `RXTXLostPackets` shows the final effect on vehicle communication reliability.

---

# Packet Loss Evaluation

## RSU Physical-Layer Losses (`SNIRLostPackets`)

The `SNIRLostPackets` metric is collected at the legitimate RSU and represents packets that cannot be successfully decoded because the received signal quality is degraded by noise and interference.

The obtained results are:

| Configuration | SNIRLostPackets |
|--------------|----------------:|
| Jammer disabled | 8 |
| Jammer enabled | 58 |

In the absence of the jammer, the RSU loses only 8 packets due to normal wireless effects, such as propagation loss, background noise, and channel variability.

When the jammer is activated, the number of SNIR-related losses increases to 58. This represents a significant increase in failures and confirms that the reactive jammer successfully introduces additional interference into the IEEE 802.11p channel.

The increase in `SNIRLostPackets` is the first evidence that the PHY-layer attack is effective. The jammer-generated signal reduces the received SNIR of legitimate transmissions when the interference overlaps with packet reception.

---

# Vehicle Communication Losses (`RXTXLostPackets`)

The `RXTXLostPackets` metric is measured at the vehicles and represents packets that are not successfully delivered after the complete transmission process. Unlike `SNIRLostPackets`, which only describes physical-layer degradation, this metric represents the final impact on vehicle-to-vehicle communication.

The aggregated results are:

| Configuration | Total RXTXLostPackets |
|--------------|----------------------:|
| Jammer disabled | 0 |
| Jammer enabled | 22 |

Without the jammer, all vehicles report ```RXTXLostPackets = 0```, indicating that all transmitted packets are successfully received under normal simulation conditions.

With the jammer enabled, the total number of vehicle-side losses increases to 22. The losses are distributed only among a subset of vehicles, while many nodes continue reporting zero losses.

This behaviour is expected because the reactive jammer does not create uniform interference over the entire simulation area. The impact depends on several factors:

* distance between the communicating vehicles and the jammer;
* relative position of the vehicles during transmission;
* propagation and shadowing effects;
* overlap between legitimate transmissions and jamming bursts.

The limited number of `RXTXLostPackets` compared with the increase in `SNIRLostPackets` shows that not every physical-layer degradation results in a complete communication failure. Some packets experience reduced signal quality but are still successfully decoded, while others are sufficiently affected by the interference to be lost at the MAC layer.

Therefore, the jammer does not completely isolate vehicles from the network. Instead, it selectively reduces communication reliability, which is the expected behaviour of a reactive jammer.

---

# Channel Capture Example

<video autoplay loop muted playsinline width="600">
  <source src="{{ '/assets/images/packet_capture.webm' | relative_url }}" type="video/webm">
</video>

The simulation video shows an example of the packet capture phenomenon in an IEEE 802.11 network. Two frames are transmitted from different directions, and the visualization demonstrates how overlapping transmissions interact at the receiver. In particular, a stronger frame, such as a jammer transmission, can dominate the channel and affect the reception of a weaker frame. This illustrates the influence of signal strength, interference, and collisions on wireless communication.


# Discussion

The experiment demonstrates that a PHY-assisted reactive jammer can significantly degrade IEEE 802.11p communication while maintaining selective behaviour.

The main observations are:

* Physical-layer losses at the RSU increase from **8 to 58 `SNIRLostPackets`**, showing that the jammer effectively reduces signal quality.
* Vehicle-side communication failures increase from **0 to 22 `RXTXLostPackets`**, proving that the interference affects end-to-end packet delivery.
* The impact is spatially dependent and varies according to vehicle position and channel conditions.

These results confirm that the implemented jammer is capable of introducing realistic PHY-layer interference into a VEINS VANET scenario while preserving the characteristics of a reactive attack.

---

# Limitations and Future Evaluation

The current evaluation is based on a single simulation replication and one default configuration. Additional experiments could investigate:

* different jammer transmission powers;
* different jamming burst durations;
* different jammer positions;
* varying vehicle densities;
* comparison with constant and random jamming strategies;

These extensions would provide a more complete characterization of the effectiveness, range, and efficiency of the reactive jamming strategy.