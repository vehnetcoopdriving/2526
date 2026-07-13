---

title: How to Run
parent: Veins Jammer
nav_order: 4
---

# How to Run

## Prerequisites

The project was developed using **VEINS 5.3.1** and requires a standard VEINS simulation environment.

Before running the simulation, ensure that the following software is installed:

* OMNeT++ (compatible with VEINS 5.3.1)
* SUMO (Simulation of Urban MObility)
* VEINS 5.3.1
* A supported C++ compiler

In addition:

* the VEINS installation must be correctly configured;
* the SUMO executables must be available in the system `PATH`;
* the project must be imported and built successfully in the OMNeT++ workspace.

---

## Building the Project

Compile the project from the root directory using:

```bash
make
```

Alternatively, build the project from the OMNeT++ IDE using **Project → Build Project**.

---

## Running the Simulation

<video autoplay loop muted playsinline width="400">
  <source src="{{ '/assets/images/sumo_jammer_video.webm' | relative_url }}" type="video/webm">
</video>

The default simulation uses the `Default` configuration defined in `omnetpp.ini`.

### OMNeT++ IDE

1. Open the project.
2. Open `omnetpp.ini`.
3. Select **Run As → OMNeT++ Simulation**.
4. Choose the desired configuration.

During execution, SUMO is started automatically, vehicles are created through TraCI, and simulation results are written to the `results/` directory.

### Command Line

The same simulation can be started from the terminal:

```bash
opp_run -u Cmdenv -f omnetpp.ini -c Default
```

If the project includes a launch script, it can also be used:

```bash
./run_veins_jammer.sh
```

---

## Available Configurations

The project provides three simulation configurations through `omnetpp.ini`.

| Configuration          | Description                                         |
| ---------------------- | --------------------------------------------------- |
| `Default`              | Standard scenario with the reactive jammer enabled. |
| `WithBeaconing`        | Enables periodic beacon transmission.               |
| `WithChannelSwitching` | Enables IEEE 1609.4 channel switching.              |

The desired configuration can be selected from the OMNeT++ IDE or with the `-c` command-line option.

---

## Results

After each simulation, OMNeT++ generates scalar and vector result files in the `results/` directory.

The jammer records statistics including:

* detected channel activities;
* jammer activations;
* reaction delay;
* jamming duration;
* transmission power.

These results can be analysed using the OMNeT++ Result Analysis tools.
