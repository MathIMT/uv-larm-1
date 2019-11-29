# What is SLAM in a Nutshell?

Mobile robots rely heavily on accurate representations of the environment (i.e *maps*) to fulfill their tasks (autonomous navigation, exploration, ...). Inside buildings, GPS signals are too weak to be used to localize robots. Hence we face a so-called Chicken-and-Egg-Problem, as *localization* requires a map, and map building (i.e. *mapping*) requires the current location.
One solution consists in doing *Simultaneous Localization and Mapping* (a.k.a. SLAM) using a SLAM algorithm that typically reaches centimetric precision. 

There are many different flavors of SLAM especially regarding the map format. The dominating 2D map format is the occupancy grid, also called grid map. A grid map is a matrix whose cells represents a defined region of the real world; this is the *resolution* of the grid map (typically a square of 5cm). A cell holds the estimated probability that the space it represents is traversable (free space) or not (obstacle). The simplest format is the 3-state occupancy grid in which a cell has 3 different possible values: 0 (free space), 0.5 (unknown) and 1 (obstacle).

![Overview of a SLAM algorithms that produces a 3-state occupancy grid map and the robot pose (i.e. the robot position and its orientation)](files/SLAM/SLAMGridMaps.jpg)

<!-- {% hint style="info" %}
Deeper explanation can be found in
{% endhint %} -->

<!-- Localization
- Dead Reckoning
- Particle Filters
- Kalman Filters
- Pose Graph Optimization
- Scan matching -->

# Goal of this Tutorial

- Discover and use ROS tools: `roscore`, `rosrun`, `roslaunch` (launch files), `rqt_graph`, catkin, `rviz`, `rosbag`
- Use robotics simulators: **stage** (2d), **gazebo** (3d)
- Use *GMapping* (a ROS-based SLAM implementation) to build a map of an indoor environment both in simulation and in real world  

# ROS Prerequisites

- ROS correctly installed (cf. [Setup](tutorials/setup.md))
- A *catkin workspace* directory (usually `~/catkin_ws`) in which you will create your catkin packages or install third party ones

# 2d Simulation with Stage 

Let's start with a first 2d ROS simulation with the [stage](http://wiki.ros.org/stage) simulator.

>Stage provides several sensor and actuator models, including sonar or infrared rangers, scanning laser rangefinder, color-blob tracking, fiducial tracking, bumpers, grippers and mobile robot bases with odometric or global localization. 

##Install Stage

Check that stage is installed:

	```shell
	$ dpkg -l | grep stage
	ii  ros-melodic-stage        4.3.0-0bionic.20191008.154542    amd64    Mobile robot simulator http://rtv.github.com/Stage
	ii  ros-melodic-stage-ros    1.8.0-0bionic.20191008.204912    amd64    This package provides ROS specific hooks for stage 
	```

Install it otherwise:
	
	```shell
	$ sudo apt update
	$ sudo apt install ros-melodic-stage ros-melodic-stage-ros
	```

You can explore the files installed by these two packages:

	```shell
	$ roscd stage_ros
	```

##Stage Simulation with one Robot

[Source](http://wiki.ros.org/stage/Tutorials/SimulatingOneRobot)

	```shell
	$ roscore
	...
	# another shell
	$ rosrun stage_ros stageros $(rospack find stage_ros)/world/willow-erratic.world
	```

<!-- 
rostopic list	
rqt_image
rviz
move robot around
.world format
-->

##Advanced Stage 

[Documentation](https://player-stage-manual.readthedocs.io/en/stable/WORLDFILES/)

You can customize your simulation by changing the `.world` and for example:
- change the map
- change the robot model (sensors, body shape, ...)
- add multiple robots into the scene
- ...

#Create and Version control your first catkin package

1. Create a catkin package `larm1_mapping`

	```shell
	$ cd ~/catkin_ws
	$ create_catkin_package larm1_mapping
	catkin_make
	```

2. Ensure you have an account on [gvipers](https://gvipers.imt-lille-douai.fr/) (IMT Lille Douai gitlab)

3. Create a repository named `larm1_mapping` 

4. rename ~/catkin_ws/src/larm1_mapping into ~/catkin_ws/src/larm1_mapping.old

4. Clone your git repository into `~/catkin_ws/src` 

	```shell
	$ cd ~/catkin_ws/src
	$ git clone https://gvipers.imt-lille-douai.fr/XXXX/larm1_mapping
	```

5. Move files and commit 
	
	```shell
	$ mv ~/catkin_ws/src/larm1_mapping.old/* ~/catkin_ws/src/larm1_mapping/
	$ rm -fr ~/catkin_ws/src/larm1_mapping.old
	$ cd ~/catkin_ws/src/larm1_mapping
	$ git add -A
	$ git commit -m "my mapping package"
	$ git push
	```

<!-- The floorplan map is given (*dia.pgm*). -->
<!-- The directory `~/catkin_ws/src/larm1_mapping` should contains: -->
<!-- - Create a *launch file* named (`imt.launch`) -->

#**Your** first launch file

The objective is to implement a full-fledge simulation using stage with one robot equipped with 2d laser ranger.
Everything should be launched with one *launch file* and committed in **your** git repository.


	```shell
	roslaunch larm1_mapping robot_stage.world
	```

it should open stage, rviz


## Rviz


# Gazebo Simulator



# Save and Replay Topic Data using `rosbag`


Data sets

http://car.imt-lille-douai.fr/polyslam/


# Map building using GMapping

both in simul and real world

<!-- Map accurracy and comparison -->

# Bibliography 

[1] Phd Johann