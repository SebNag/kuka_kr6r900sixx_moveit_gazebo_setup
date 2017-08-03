# KUKA KR6R900SIXX Gazebo

## Overview

This package contains the configuration files and ros packages required to simulate the _kuka kr6r900sixx_ manipulator in `gazebo` together with the `ros_control` packages and the `MoveIt!` motion planner. 

Directory structure of the `kuka_experimantal/kuka_kr6_gazebo` package: 
 * _launch directory_:  
    * Requires a valid `xarco URDF model` in the `kuka_experimantal/kuka_kr6_support` package to load the robot model onto the parameter server. The robot model parameter is saved as `robot_description`.  
    * Inits and starts the `gazebo ros_control interface`

* _config directory:_
    * `joint_state_controller.yaml` joint state controller to publishes the joint values of the robot 
    * `arm_controller.yaml` JointTrajectoryController which takes in a trajector e.g. from moveit and drives the joints of the robot  

* _urdf directory:_
    * xml elements, which are required by gazebo to make the urdf file(s) provided in the `kuka_experimental/kuka_kr6_support` package usable with gazebo, are inserted into the `kuka_kr6r900sixx_macro.xarco` file!
    * The currently used _intertia_ xml elements are **not well/randomly defined**, values were added only to provide a functional test simulation! Basic transmission elements have been added to the URDF files. Further improvement may be required to acquire a more realistic simulation.  

## Build the setup 

1. Install up-to-date ros distribution and source the `setup.sh` script 
1. `cd` in the cloned directory from this repo and run `catkin_make` to build the containing packages. 
1. make sure you have the `ros_gazeo_pkgs` package installed 
1. if not already in your `~/.basrc` file: `source $CATKIN_WS/devel/setup.sh`

## Using Moveit! together with Gazebo Simulator

1. Bring the robot model into gazebo and load the `ros_control` controllers:
   ```roslaunch kuka_kr6_gazebo kr6r900sixx_gazebo.launch``` 

2. Launch moveit! and ensure that it is configured to run alongside Gazebo:
```roslaunch kuka_kr6r900sixx_moveit_config moveit_planning_execution_rsi.launch sim:=true``` 

## Useful Links 

* Based on [ABB Gazebo Simulation](https://github.com/ros-industrial/abb_experimental/tree/kinetic-devel/abb_irb120_gazebo)
* Install the `ros_gazebo_pkgs` [HowTo](http://gazebosim.org/tutorials?tut=ros_installing&cat=connect_ros) 
* URDF in gazebo [Tutorial](http://gazebosim.org/tutorials?tut=ros_urdf&cat=connect_ros) 
* Gazebo and ros_control [Tutorial](http://gazebosim.org/tutorials?tut=ros_control&cat=connect_ros) 
