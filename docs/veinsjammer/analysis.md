---
title: Analysis
parent: Veins Jammer
nav_order: 5
---

# Analysis

## Results

The simulation evaluates the influence of jammer position on vehicular communication performance. Three configurations are considered:

* **Disabled jammer scenario:** vehicles communicate without intentional interference and provide the baseline network performance.
* **Near jammer scenario (20 mW, position: 2050, 2050):** the reactive jammer is positioned closer to the main communication area, resulting in stronger interference during detected transmissions.
* **Far jammer scenario (20 mW, position: 1400, 1400):** the reactive jammer is moved farther from the communication area, reducing the interference effect due to increased propagation distance.

The objective is to evaluate how the jammer location affects packet reception reliability, SNIR degradation, and overall V2V communication performance.

## Performance Metrics

The communication performance is evaluated using:

* Total received WSMs
* Mean received WSMs per vehicle
* SNIR lost packets
* Packet Delivery Ratio (PDR)
* Packet Loss Ratio (PLR)

---

# Disabled Jammer Scenario (Baseline)

The disabled jammer configuration represents normal vehicular communication without malicious interference. It provides the reference performance used to evaluate the impact of jammer activation.

The measured performance is:

| Metric                         |      Value |
| ------------------------------ | ---------: |
| Total generated WSMs           |     **87** |
| Total received WSMs            |   **1640** |
| Mean received WSMs per vehicle |  **24.07** |
| SNIR lost packets              |    **245** |
| Packet Delivery Ratio (PDR)    | **87.00%** |
| Packet Loss Ratio (PLR)        | **13.00%** |

The Packet Delivery Ratio is calculated as:

$$
PDR=\frac{\text{Received Packets}}
{\text{Received Packets}+\text{Lost Packets}}
\times100
$$

The Packet Loss Ratio is:

$$
PLR=\frac{\text{Lost Packets}}
{\text{Received Packets}+\text{Lost Packets}}
\times100
$$

The baseline losses are caused by normal wireless effects, including propagation loss, packet collisions, and channel conditions.

---

# Near Reactive Jammer Scenario (20 mW, Position: 2050, 2050)

![Simulation topology]({{ "/assets/images/near.png" | relative_url }})

*Figure 1. Jammer near to the RSU*

In the near jammer configuration, the reactive jammer is placed at **(2050,2050)**. The reduced distance between the jammer and communication participants increases the received interference level and produces stronger degradation during active transmissions. During the simulation, the reactive jammer is activated **23 times**, generating interference bursts in response to detected channel activity.

The measured performance is:

| Metric                         |      Value |
| ------------------------------ | ---------: |
| Total generated WSMs           |     **87** |
| Total received WSMs            |   **1729** |
| Mean received WSMs per vehicle |  **25.81** |
| SNIR lost packets              |    **442** |
| Packet Delivery Ratio (PDR)    | **79.64%** |
| Packet Loss Ratio (PLR)        | **20.36%** |

The Packet Delivery Ratio is:

$$
PDR=\frac{1729}{1729+442}\times100
$$

$$
PDR=79.64%
$$

The Packet Loss Ratio is:

$$
PLR=\frac{442}{1729+442}\times100
$$

$$
PLR=20.36%
$$

Compared with the disabled jammer case, the near jammer introduces:

$$
442-245=197
$$

additional SNIR-related packet losses.

The Packet Delivery Ratio decreases from:

$$
87.00% \rightarrow 79.64%
$$

while the Packet Loss Ratio increases from:

$$
13.00% \rightarrow 20.36%
$$

This demonstrates that the near jammer has a strong impact on communication reliability.

---

# Far Reactive Jammer Scenario (20 mW, Position: 1400, 1400)

![Simulation topology]({{ "/assets/images/far_away.png" | relative_url }})

*Figure 2. Jammer far-away from the RSU*

For the far jammer configuration, the jammer is moved to **(1400,1400)**. The increased distance modifies the interference conditions experienced by vehicles and reduces the number of packets affected by jamming.

The measured results are:

| Metric                         |      Value |
| ------------------------------ | ---------: |
| Vehicle-generated WSMs         |     **60** |
| RSU-generated WSMs             |     **28** |
| Total generated WSMs           |     **87** |
| Total received WSMs            |   **1538** |
| Mean received WSMs per vehicle |  **23.30** |
| SNIR lost packets              |    **322** |
| Packet Delivery Ratio (PDR)    | **82.69%** |
| Packet Loss Ratio (PLR)        | **17.31%** |

The Packet Delivery Ratio is:

$$
PDR=\frac{1538}{1538+322}\times100
$$

$$
PDR=82.69%
$$

The Packet Loss Ratio is:

$$
PLR=\frac{322}{1538+322}\times100
$$

$$
PLR=17.31%
$$

Compared with the near jammer configuration, the far jammer reduces the number of SNIR-related packet losses:

$$
442-322=120
$$

packets are successfully recovered when changing the jammer position.

---

# Comparison Between Disabled, Near Jammer, and Far Jammer Cases

| Metric                         | Disabled Jammer | Near Jammer (2050,2050) | Far Jammer (1400,1400) |
| ------------------------------ | --------------: | ----------------------: | ---------------------: |
| Total generated WSMs           |              87 |                      87 |                     87 |
| Total received WSMs            |            1640 |                    1729 |                   1538 |
| Mean received WSMs per vehicle |           24.07 |                   25.81 |                  23.30 |
| SNIR lost packets              |             245 |                     442 |                    322 |
| Packet Delivery Ratio          |          87.00% |                  79.64% |                 82.69% |
| Packet Loss Ratio              |          13.00% |                  20.36% |                 17.31% |

---

# Discussion

The results confirm that jammer placement has a significant influence on vehicular communication performance.

Without interference, the network achieves a Packet Delivery Ratio of **87.00%** with **245 SNIR-related packet losses**. When the reactive jammer is placed at **(2050,2050)**, the communication performance degrades more significantly, reaching a Packet Delivery Ratio of **79.64%** and increasing SNIR losses to **442 packets**.

When the jammer is moved to **(1400,1400)**, the Packet Delivery Ratio improves to **82.69%**, and SNIR losses decrease to **322 packets**. This indicates that increasing the distance between the jammer and the communication area reduces the effectiveness of the interference.

The comparison demonstrates that reactive jamming performance depends on the jammer position relative to the communication topology. A jammer located closer to active transmitters and receivers can produce stronger interference because the jamming signal experiences lower propagation attenuation. Increasing the distance reduces the received interference power and limits the degradation of V2V communication.