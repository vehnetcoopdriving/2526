---
title: Analysis
parent: Platoon splitting
nav_order: 5
---

# Analysis

The simulation was conducted using a parametric analysis approach. Values related to the fundamental dynamics and trigger timings, such as leavingTime and the various ACC controller calibration parameters, were kept constant. The execution focused instead on varying the leavingDistance parameter, which defines the distance threshold at which the leaving vehicle detaches from the original platoon.

The graph illustrates the time evolution of the headway (relative frontal distance) between the vehicles.
In the initial phase (t < 3s ), the system operates in a steady state maintaining a nominal constant spacing of 5 meters between vehicles, confirming the successful coupling and stability of the cooperative CACC dynamics. Upon the triggering of the leavingTime parameter,  the leaving vehicle (the future leader of the sub-platoon)  begins to widen the spatial gap with respect to the preceding vehicle, creating an increasing distance ramp. This phase represents the kinematic separation transient, whose objective is to push the gap up to the leavingDistance threshold in order to trigger the controller state transition.
Concurrently, the slight fluctuations (ranging between 3 and 5 meters) observable in the vehicles' curves during the first 15 seconds depict the physiological settling phase of the vehicular string following the perturbation. The control loop progressively dampens the tracking error, ensuring the absorption of the transient and restoring full spatial stability for the remainder of the formation.


![Grafico accelerazione 8]({{'/assets/images/accelerazione_8.png' | relative_url }}) ![Grafico distanza 8]({{'/assets/images/distance_8.png' | relative_url }})

![Grafico accelerazione 16]({{'/assets/images/accel_16.png' | relative_url }}) ![Grafico distanza 16]({{'/assets/images/distance_16.png' | relative_url }})

![Grafico accelerazione 32]({{'/assets/images/accel_32.png' | relative_url }}) ![Grafico distanza 32]({{'/assets/images/dist_32.png' | relative_url }})


The comparison among the three simulated scenarios, obtained by setting the leavingDistance parameter to 8, 16, and 32 meters respectively, highlights a marked kinematic trade-off during the transient phase of the platoon separation.

On one hand, as the requested leavingDistance increases, there is a natural increase in the frontal safety margin. The leaving vehicle (the new leader) opens a much deeper spatial gap relative to the tail of the original formation. Reaching an inter-vehicle distance of 32 meters guarantees a clear physical separation before authorizing the controller downgrade to autonomous mode (ACC), minimizing the risk of frontal collisions in the event of sudden braking by the old platoon.

On the other hand, this frontal advantage generates a severe repercussion on the stability of the vehicular string. To accumulate a larger spatial delay (as in the 32-meter case), the new leader is forced to maintain a lower speed, significantly prolonging its relative deceleration phase. This maneuver induces a strong compression effect on the vehicles (the members of the sub-platoon).

Since the followers, in the initial phases of the transient, are still bound to maintaining the constant spacing and are subject to the inertia of the original network dynamics (structured around the old leader's cruising speed), the prolonged braking of the intermediate vehicle drastically reduces the headway of the tail nodes. In summary, the pursuit of maximum frontal spatial safety amplifies the backward kinematic perturbation: the delay wave dangerously narrows the inter-distances between the vehicles following the new leader, stressing the responsiveness of the control loop and temporarily reducing the internal safety margins within the newly formed convoy.

To mitigate this critical compression and enhance overall string stability, a more robust separation procedure should be considered for future implementations. Rather than executing the maneuver under the original network hierarchy, an optimized approach would introduce a preliminary logical reconfiguration. This improved procedure would involve electing the splitting vehicle as a temporary leader and explicitly synchronizing the sub-platoon followers to its telemetry prior to initiating the physical gap-opening braking. Such an anticipatory synchronization would prevent the dangerous spatial narrowing and ensure a much safer kinematic transition for the entire trailing convoy.

## Emergency braking simulation

To evaluate the robustness of the splitting maneuver, a fault injection analysis was conducted by simulating a severe emergency braking maneuver by the original leader. The kinematic fault parameters were set to a deceleration of 6 m/s² (brakingAcceleration) maintained for 4s (timeBraking). The results highlight a marked dependence of active safety on the longitudinal controller in use at the time of the event:

Braking after the switch (Crash): When the emergency is triggered after the logical completion of the separation, the leaving vehicle has already been downgraded to the autonomous ACC mode. In the absence of network telemetry, the system relies solely on the radar detection loop. The intrinsic latency of the sensor, combined with a spatial gap that is not yet wide enough to dissipate the violent deceleration applied (6 m/s² for 4s), saturates the reaction capabilities of the control loop. As visible from the collapse to zero of the inter-distance curve, the accumulated delay inevitably leads to a rear-end collision.

![Grafico incidente]({{'/assets/images/incidente.png' | relative_url }})

Braking before the switch (Safe): When the perturbation occurs during the separation transient, the leaving vehicle is still operating under the CACC controller. Leveraging V2V communication, the vehicle receives the instantaneous feedforward of the leader's deceleration, compensating for the velocity delta with near-zero latency. The vehicular string successfully absorbs the braking wave while maintaining safe spatial margins, avoiding a collision entirely.


![Grafico no incidente]({{'/assets/images/noIncidente.png' | relative_url }})





## Future work

This fault-injection mechanism is fully parameterizable within the simulation environment, allowing for the dynamic configuration of the trigger time, braking duration, and absolute deceleration force.

Future research will focus on utilizing this testing framework to conduct extensive parametric sweeps. By systematically varying these stress conditions, the objective is to identify the optimal control parameters and safety thresholds for the separation maneuver, ensuring maximum string stability and collision avoidance even under the most critical dynamic constraints.





