---
title: Scenario
parent: Platoon splitting
nav_order: 2
---

# Scenario

## Platoon Configuration

We customized the default [`GettingStartedScenario`](https://github.com/vehnetcoopdriving/platoonsplitting/blob/platoonsplitting/src/plexe/scenarios/GettingStartedScenario.ned#L11-L13) to introduce three novel parameters that govern the splitting protocol:

1. **`splittingVehicleId`** — identifies the vehicle that will become the leader of the sub-platoon detaching from the main platoon.
2. **`leavingTime`** — the simulation instant at which that vehicle sends a request to the current platoon leader, seeking approval for the detach maneuver.
3. **`leavingDistance`** — together with the detach request, the vehicle also asks for authorization to keep using the CACC controller (e.g., PATH) up to this distance from the split point. Once this distance is reached, the leader grants the final authorization and the platoon formation records are updated accordingly.

This two-step authorization protocol — first approving the intent to leave, then confirming the transition after the agreed distance — is fully configurable through the `GettingStartedScenario` parameters listed above.


## Protocol design

![Diagramma]({{'/assets/images/diagramma.png' | relative_url }})