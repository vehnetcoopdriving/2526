---

title: Analysis
parent: Veins Jammer
nav_order: 5
---

# Analysis

## Evaluation

The implemented jammer was evaluated by comparing three simulation scenarios:

* **Disabled jammer:** baseline communication without interference.
* **Near jammer:** jammer positioned at **(2050 m, 2050 m)**.
* **Far jammer:** jammer positioned at **(1400 m, 1400 m)**.

The objective is to assess how the jammer position influences IEEE 802.11p communication performance.

The following metrics are considered:

* Total generated WSMs
* Total received WSMs
* Mean received WSMs per vehicle
* SNIR lost packets
* Packet Delivery Ratio (PDR)
* Packet Loss Ratio (PLR)

The Packet Delivery Ratio and Packet Loss Ratio are computed as:

$$
PDR=\frac{\text{Received Packets}}
{\text{Received Packets}+\text{Lost Packets}}\times100
$$

$$
PLR=\frac{\text{Lost Packets}}
{\text{Received Packets}+\text{Lost Packets}}\times100
$$

---

## Disabled Jammer (Baseline)

The baseline scenario represents normal network operation without malicious interference.

| Metric                         |      Value |
| ------------------------------ | ---------: |
| Total generated WSMs           |     **87** |
| Total received WSMs            |   **1640** |
| Mean received WSMs per vehicle |  **24.07** |
| SNIR lost packets              |    **245** |
| Packet Delivery Ratio          | **87.00%** |
| Packet Loss Ratio              | **13.00%** |

---

## Near Jammer

![Simulation topology]({{ "/assets/images/near.png" | relative_url }})

*Figure 1. Jammer positioned near the RSU.*

The jammer is placed at **(2050 m, 2050 m)**, close to the main communication area. During the simulation it detects channel activity and activates **23** times.

| Metric                         |      Value |
| ------------------------------ | ---------: |
| Total generated WSMs           |     **87** |
| Total received WSMs            |   **1729** |
| Mean received WSMs per vehicle |  **25.81** |
| SNIR lost packets              |    **442** |
| Packet Delivery Ratio          | **79.64%** |
| Packet Loss Ratio              | **20.36%** |

Compared with the baseline, the near jammer increases SNIR-related packet losses from **245** to **442**, reducing the Packet Delivery Ratio by more than **7 percentage points**.

---

## Far Jammer

![Simulation topology]({{ "/assets/images/far_away.png" | relative_url }})

*Figure 2. Jammer positioned farther from the RSU.*

The jammer is moved to **(1400 m, 1400 m)**, increasing its distance from the main communication area.

| Metric                         |      Value |
| ------------------------------ | ---------: |
| Total generated WSMs           |     **87** |
| Total received WSMs            |   **1538** |
| Mean received WSMs per vehicle |  **23.30** |
| SNIR lost packets              |    **322** |
| Packet Delivery Ratio          | **82.69%** |
| Packet Loss Ratio              | **17.31%** |

Compared with the near configuration, the greater distance reduces the impact of the jammer, decreasing SNIR-related packet losses from **442** to **322**.

---

## Comparison

| Metric                         | Disabled | Near Jammer | Far Jammer |
| ------------------------------ | -------: | ----------: | ---------: |
| Total generated WSMs           |       87 |          87 |         87 |
| Total received WSMs            |     1640 |        1729 |       1538 |
| Mean received WSMs per vehicle |    24.07 |       25.81 |      23.30 |
| SNIR lost packets              |      245 |         442 |        322 |
| Packet Delivery Ratio          |   87.00% |      79.64% |     82.69% |
| Packet Loss Ratio              |   13.00% |      20.36% |     17.31% |

---

## Discussion

The results show that jammer placement has a significant impact on communication reliability.

The **near jammer** produces the strongest interference, increasing the number of SNIR-related packet losses by approximately **80%** compared with the baseline and reducing the Packet Delivery Ratio from **87.00%** to **79.64%**.

Moving the jammer farther from the communication area reduces its effectiveness. Although the **far jammer** still degrades network performance, the Packet Delivery Ratio improves to **82.69%**, and the number of lost packets decreases compared with the near configuration.

Although the near jammer scenario reports a higher total number of received WSMs than the baseline, this metric represents all successful receptions across all vehicles rather than unique transmitted packets. Because vehicle positions and connectivity change during the simulation, the total number of receptions may vary independently of the packet loss caused by interference. For this reason, SNIR losses and PDR provide a more reliable indication of the jammer's impact.

Overall, the experiments demonstrate that the effectiveness of reactive jamming depends strongly on the jammer's position. A jammer located closer to the communicating vehicles generates stronger interference, whereas increasing the distance reduces the received jamming power and limits its impact on IEEE 802.11p communications.
