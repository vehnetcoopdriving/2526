---
title: Analysis
parent: Platoon splitting
nav_order: 5
---

# Analysis

The simulation was conducted using a parametric analysis approach. Values related to the fundamental dynamics and trigger timings, such as leavingTime and the various ACC controller calibration parameters, were kept constant. The execution focused instead on varying the leavingDistance parameter, which defines the distance threshold at which the leaving vehicle detaches from the original platoon.

The graph illustrates the time evolution of the headway (relative frontal distance) between the simulation nodes.
In the initial phase (t < 3s ), the system operates in a steady state: the trailing vehicles maintain a nominal constant spacing of 5 meters, confirming the successful coupling and stability of the cooperative CACC dynamics. Upon the triggering of the leavingTime parameter,  the leaving vehicle (the future leader of the sub-platoon)  begins to widen the spatial gap with respect to the preceding vehicle, creating an increasing distance ramp. This phase represents the kinematic separation transient, whose objective is to push the gap up to the leavingDistance threshold in order to trigger the controller state transition.
Concurrently, the slight fluctuations (ranging between 3 and 5 meters) observable in the trailing vehicles' curves during the first 15 seconds depict the physiological settling phase of the vehicular string following the perturbation. The control loop progressively dampens the tracking error, ensuring the absorption of the transient and restoring full spatial stability for the remainder of the formation.


![Grafico 8]({{'/assets/images/grafico8.png' | relative_url }})

![Grafico 16]({{'/assets/images/grafico16.png' | relative_url }})

![Grafico 32]({{'/assets/images/grafico32.png' | relative_url }})


The comparison among the three simulated scenarios, obtained by setting the leavingDistance parameter to 8, 16, and 32 meters respectively, highlights a marked kinematic trade-off during the transient phase of the platoon separation.

On one hand, as the requested leavingDistance increases, there is a natural increase in the frontal safety margin. The leaving vehicle (the new leader) opens a much deeper spatial gap relative to the tail of the original formation. Reaching an inter-vehicle distance of 32 meters guarantees a clear physical separation before authorizing the controller downgrade to autonomous mode (ACC), minimizing the risk of frontal collisions in the event of sudden braking by the old platoon.

On the other hand, this frontal advantage generates a severe repercussion on the stability of the trailing vehicular string. To accumulate a larger spatial delay (as in the 32-meter case), the new leader is forced to maintain a lower speed, significantly prolonging its relative deceleration phase. This maneuver induces a strong compression effect on the trailing vehicles (the members of the sub-platoon).

Since the followers, in the initial phases of the transient, are still bound to maintaining the constant spacing and are subject to the inertia of the original network dynamics (structured around the old leader's cruising speed), the prolonged braking of the intermediate vehicle drastically reduces the headway of the tail nodes. In summary, the pursuit of maximum frontal spatial safety amplifies the backward kinematic perturbation: the delay wave dangerously narrows the inter-distances between the vehicles following the new leader, stressing the responsiveness of the control loop and temporarily reducing the internal safety margins within the newly formed convoy.

## Future work

An emergency braking scenario has been implemented to serve as a comprehensive kinematic stress test. This fault-injection mechanism is fully parameterizable within the simulation environment, allowing for the dynamic configuration of the trigger time, braking duration, and absolute deceleration force.

Future research will focus on utilizing this testing framework to conduct extensive parametric sweeps. By systematically varying these stress conditions, the objective is to identify the optimal control parameters and safety thresholds for the separation maneuver, ensuring maximum string stability and collision avoidance even under the most critical dynamic constraints.





