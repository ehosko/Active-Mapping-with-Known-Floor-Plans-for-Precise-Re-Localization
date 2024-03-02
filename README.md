# Active-Mapping-with-Known-Floor-Plans-for-Precise-Re-Localization

[Report](./docs/Report.pdf)

Cutting-edge devices like augmented reality headsets or micro aerial vehicles require
precise localization to complete a variety of tasks. An approach to enable an agent
to localize itself in a particular area is to first create a map and then re-localize
itself in the created map. The autonomous creation of such maps is a non-trivial
and widely researched problem. The numerous active exploration and mapping
approaches may pursue different objectives, such as accurate 3D reconstruction,
surface inspection, or the aforementioned localization, but often share a framework
structure.
Many traditional approaches do not consider any prior information. However, in
real-world scenarios, 2D floor plans are widely available and can be used to influence
the decision of the planner with the information at hand.
This project aims to implement an exploration planner that maps an environment
with the goal of precise re-localization. To that end, the frequent availability of
2D floor plans is exploited for a more informed exploration and mapping process.
A novel exploration planner is introduced in four variants trying to revisit drifty
regions during the mapping process to increase the localization ability.
The four variants of the proposed planner are compared against three different planners
using a custom evaluation framework quantifying the re-localization accuracy
of the created map. Further analysis is conducted regarding the precision of pose
estimation during the mapping process and the efficiency of the exploration. The
analysis shows that the novel exploration planner improves the re-localization accuracy
compared to the other planners. However, the prior information gained from
the 2D floor plan could not be exploited to its full potential.

## Components
- [Main framework structure](https://github.com/ehosko/optimal_active_guidance_in_mixed_reality_using_prior_floorplans)
- [maplab](https://github.com/ehosko/maplab)
- [Floor Plan Localization](https://github.com/ehosko/localization_using_floorplans)
- [Evaluation](https://github.com/ehosko/rpg_trajectory_evaluation)

## Setup
This project is built and run on Ubuntu 18.04 using ROS Melodic.

### Install
To install the different components of the framework, follow the descriptions in the respective READMEs of the components above. The [Floor Plan Inclusion](https://github.com/ehosko/localization_using_floorplans) is automatically installed with the [Main framework structure](https://github.com/ehosko/optimal_active_guidance_in_mixed_reality_using_prior_floorplans), so there is no need for an extra installation. Follow the installation given for maplab and the evaluation, but replace the repository URL with the forked URL from above, when cloning. In the end, the framework should consist of three catkin workspaces, one for the main framework and the floor plan inclusion, one for maplab, and one for the evaluation.

### Simulation Environments
Two simulation environments, a maze, and a warehouse, are made available for Isaac Sim : [Environments](https://polybox.ethz.ch/index.php/s/SPR7wtBlBgyCn26)

### Test Installation

1. Launch Isaac Sim and load the maze environment. Press the play button in Isaac Sim.
2. Navigate to the utils folder in the main framework workspace. Launch the test experiment to verify a correct setup.

```
bash run_experiment_test.sh
```
In a correct setup, the Isaac Sim Game Play should change views, and two terminators should pop up: one for the planner and one for ROVIOLI. Moreover, two Rviz windows should open, one showing the planned trajectory and moving agents, the other is just blank.
In the output folder, you should see a created map and logging files.

## Run experiments and evaluation
The utils folder in the main framework workspace offers different bash scripts to run and evaluate experiments. Furthermore, multiple Python scripts are implemented to visualize the findings.

### Run experiment

To run the experiments with all planners over several runs, you can run the following command in the utils folder. Do not forget to first press play in Isaac Sim.

```
bash run_experiments.sh
```

Make sure to edit the amount of runs and the planners you want to use in the script. The experiment run time can be adjusted in the launch file.

### Evaluate experiment 

Most visualization scripts utilize pandas, matplotlib and seaborn.

#### Re-Localization accuracy

1. In the utils folder of the main framework, utilize the following script to collect the loop closure edges with maplab. Make sure to adapt the yaml files accordingly. Examples for the yaml files are given in `maplab/applications/maplab-console/share`.
```
bash run_eval.sh
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; This should create lc_edges.csv files in the corresponding output folders.

2. To create the re-localization accuracy statistics and visualize them for a single run, use the following command (in the evaluation framework).

```
rosrun rpg_trajectory_evaluation ros_align_traj.py
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; This should create reloc_error files in the corresponding output folders.

3. Finally, to visualize the re-localization accuracy over multiple runs, use the Python script in the utils folder of the main framework.

```
python plot_planner_comp.py
```

#### Drift

To evaluate the drift, the evaluation workspace is used. The implementation is taken from [this repository](https://github.com/uzh-rpg/rpg_trajectory_evaluation) and requires a specific folder structure for the evaluation process.
To construct this folder structure with the respective files, which are generated during the experiment run, utilize the following command in the scripts folder of the evaluation framework.

```
python2 restructure_folders.py
```

After restructuring the folders, the multiple runs can be evaluated by following the instructions given [here](https://github.com/ehosko/rpg_trajectory_evaluation).

#### Coverage over Time
After running the experiment, the file occupancy.csv should be created in the respective output folder. To plot the coverage against time, you can run the following Python script:

```
python plot_time_coverage.py
```
