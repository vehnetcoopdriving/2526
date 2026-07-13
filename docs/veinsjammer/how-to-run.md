---
title: How to Run
parent: Veins Jammer
nav_order: 4
---

# How to Run

## Prerequisites

The project was developed using **VEINS 5.3.1** and requires the standard VEINS simulation environment. Before running the simulation, ensure that the following software is installed and correctly configured:

* OMNeT++ (compatible with VEINS 5.3.1)
* SUMO (Simulation of Urban MObility)
* VEINS 5.3.1
* A C++ compiler supported by OMNeT++

In addition, verify that:

* the `VEINS_ROOT` environment variable (or equivalent project configuration) correctly points to the VEINS installation;
* SUMO binaries are available in the system `PATH`;
* the project has been imported into the OMNeT++ IDE and built successfully.

---

## Building the Project

If the project has not yet been compiled, build it from the project directory using:

```bash
make
```

Alternatively, from the OMNeT++ IDE:

1. Import the project into the workspace.
2. Build the project (**Project → Build Project**).
3. Verify that no compilation errors are reported.

---

## Running the Simulation

The default simulation uses the `Default` configuration defined in `omnetpp.ini`.

### Using the OMNeT++ IDE

1. Open the project in the OMNeT++ IDE.
2. Open `omnetpp.ini`.
3. Right-click inside the editor.
4. Select **Run As → OMNeT++ Simulation**.
5. Choose the desired configuration (`Default`, `WithBeaconing`, or `WithChannelSwitching`).

During execution:

* SUMO is launched automatically through the TraCI Scenario Manager;
* vehicles are created dynamically according to the traffic scenario;
* the jammer node remains active throughout the simulation;
* simulation results are stored in the `results/` directory.

---

### Using the Command Line

The simulation can also be executed from the terminal.

```bash
opp_run -u Cmdenv -f omnetpp.ini -c Default
```

Alternatively, if a project-specific launch script is available:

```bash
./run_veins_jammer.sh
```

---

## Available Configurations

The project provides multiple simulation configurations through `omnetpp.ini`.

| Configuration          | Description                                                 |
| ---------------------- | ----------------------------------------------------------- |
| `Default`              | Standard scenario with the reactive jammer enabled.         |
| `WithBeaconing`        | Enables periodic beacon transmission for vehicles and RSUs. |
| `WithChannelSwitching` | Enables IEEE 1609.4 service channel switching.              |

The desired configuration can be selected using the `-c` command-line option or directly from the OMNeT++ IDE.

---

## Simulation Results

After each simulation, OMNeT++ generates scalar and vector result files that can be analysed using the built-in Result Analysis tools.

The implemented jammer records, among others:

* number of legitimate transmissions detected;
* number of jammer activations;
* configured reaction delay;
* configured jamming duration;
* configured transmission power.

Additional statistics and signals can be enabled or customized through the `omnetpp.ini` configuration file.
