# ROS rtab_dumpster package

## Abstract
The package contains a URDF model of a differential drive robot equipped with an RGB-D camera.

## Brief description of the robot model
rtab_dumpster is a mobile robot base that has a differential drive conﬁguration.
The robot model comprises the following components: a rigid chassis, two independently driven wheels ﬁxed on a common horizontal axis and two passive support castor wheels one at the front and one at the back.
It also features a dump bin on top of its chassis. Additionally, both a laser scanner and a RGBD-camera are included in an elevated position in order to improve/maximize the sensors ﬁeld of view.

![dumpster_kinect](https://user-images.githubusercontent.com/40167051/56146084-de941500-5fa5-11e9-9bf5-e003da14a7cf.png)
Image of the robot model

The scene displayed by Rviz on startup showing the proper conﬁgured depth sensor
![mapping_rviz_1](https://user-images.githubusercontent.com/40167051/56146153-02575b00-5fa6-11e9-8d4c-155533cd5402.png)

## Repository architecture
### Directories :
+ **urdf/** : (required) contains the files that generate the robot model and provide simulated actuators and sensors
+ **meshes/** : (required) contains the mesh files that are part of the geometry of that robot
+ **config/** : (optional) contains YAML files that store the Navigation Stack configuration files for the robot
+ **rviz/** : (optional) contains Rviz configuration settings for displaying the robot model
+ **launch/** : (optional) contains launch file for running the robot model in Gazebo
+ **worlds/** : (optional) contains scene/environment files for Gazebo
+ **maps/** : (optional) contains the occupancy grid based maps required for navigation

### Robot model files :
+ **dumster.xacro** : the xacro file that generates the urdf description file of the robot
+ **dumster.gazebo** : file accompanying the .xacro file, it contains the gazebo specific plugins that provide an interface to control the robot and simulate sensors

## Direct usage:

- Clone this repository into a ROS catkin workspace
- Build and source the workspace
- To launch this package including Rviz: `roslaunch dumpster dumpster.launch`

If you want to move the robot using a keyboard you will also need to start a teleop node.
To run the robot with the Navigation Stack type in a new window: `roslaunch dumpster amcl.launch`

This package has only been tested on Ubuntu 16.04 LTS with ROS Kinetic and Gazebo 7.0.
