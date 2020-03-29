# Water Drone with Robonomics

This repository is dedicated to process of sending of water mesuarment data for autonomous marine vessels with sensors.

The code is provided for the publication of an article "Trustable Environmental Monitoring by means of Sensors Networks on Swarming Autonomous Marine Vessels and Distributed Ledger Technology" for Frontiers in Robotics and AI.

## Explanation of repository

An explanation is needed about some of the files in this repository:

* *model.txt* — the behavioral model of the vessel, it contains all the necessary ROS topics.
* *objective_virtual_month_smartwater.bag* — rosbag-file with the model parameters, this file is published in IPFS.
* *grid_25-04-2091.waypoints* — mission plan containing its route. Generated in the [ArduPilot GUI](https://ardupilot.org/).
* *trader.launch* — this file launches the *scripts/trader_node*. Trader's node is responsible for the economic behavior of vessel: it monitor messages on the liability market and select those that satisfy the CPS behaviour model.
* *worker.launch* — this file launches the *scripts/worker_node*. When an event of new liability creation is received the vessel runs the mission with parameters got via the objective.
* *scripts/approve.py*, *scripts/gen_objective.py*, *scripts/pub_demand.py* — Robonomics service scripts for interacting with smart contracts, generating a rosbag file and publishing a Demand message.
* **waspmote** — directory containing the files for this particular vessel: firmware for the Waspmote board to which the sensors are connected, logging software for Pixhawk autopilot.

## Testing

### Prerequisites

* [AIRA](https://github.com/airalab/aira) — Robonomics network client for ROS-enabled cyber-physical systems.

This project works on the basis of Robonomics, so you need to install image of AIRA to your cyber-physical systems (in our case, the vessel). Image installation guide can be found [here](https://aira.readthedocs.io/). 

### Installing and launch

Clone the repository into your AIRA image:

```
$ git clone https://github.com/Fingerling42/frontiers-vessel-code.git
```

Build the cloned repository using Nix environment:

```
    $ nix build -f release.nix
```

Or [standard ROS tools](http://wiki.ros.org/ROS/Tutorials/BuildingPackages). 

Launch ros-files:

```
$ roslaunch drone_on_volga trader.launch
$ roslaunch drone_on_volga worker.launch
```

## Experiments

Experiments took place in Volga river in Kuibyshev reservoir near storm drains of Avtozavodsky district, Togliatti, Samara region, Russia. Processed and visualized measurement results can be found in [this repository](https://github.com/Fingerling42/frontiers-vessel-data-processing). 

## Acknowledgments

We want to thank the [Airalab team](https://aira.life/en/) for the development and support of the unmanned surface vessel, as well as for providing the Robonomics platform support and related software.