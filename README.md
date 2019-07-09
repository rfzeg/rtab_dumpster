# ROS rtab_dumpster package
Author: Roberto Zegers R.

## Abstract
The package contains a URDF model of a differential drive robot equipped with an RGB-D camera.

## Brief description of the robot model
rtab_dumpster is a mobile robot base that has a differential drive conﬁguration.
The robot model comprises the following components: a rigid chassis, two independently driven wheels ﬁxed on a common horizontal axis and two passive support castor wheels one at the front and one at the back.
It also features a dump bin on top of its chassis. Additionally, both a laser scanner and a RGBD-camera are included in an elevated position in order to improve/maximize the sensors ﬁeld of view.  
The main skills required for developing this robot model include the following: joint and link modeling with **URDF and XACRO**, integration of **Gazebo plugins** to provide the URDF model with sensors and actuators, **CAD modelling** of mesh files with Fusion 360 and version control with **GIT**.

<img src="https://raw.githubusercontent.com/rfzeg/rtab_dumpster/master/docs/imgs/robot_model_in_gazebo.png" width="541" height="286">
Fig.1 Image of the robot model in Gazebo  

<img src="https://raw.githubusercontent.com/rfzeg/rtab_dumpster/master/docs/imgs/robot_model_dimentions.png" width="468" height="377">
Fig.2 Size of the robot model's bounding box LENGTH x WIDTH x HEIGHT = 620 x 560 x 520mm  

<img src="https://raw.githubusercontent.com/rfzeg/rtab_dumpster/master/docs/imgs/rgbd_dumpster_rtab-map.png" width="541" height="291">
Fig.3 The scene displayed by Rviz on startup showing the proper conﬁgured depth cloud orientation  

## Default topics
+ Image Topic: /camera/rgb/image_raw
+ Depth Image Topic: /camera/depth/image_raw
+ Laser Scan Topic: /scan
+ Odometry Topic: /odom
+ Movement Commands: /cmd_vel

## Gazebo differential drive controller parameters
Following parameters used by the diff_drive plugin can be customized editing the `spawn_rtab_dumpster.launch` file:  
+ odometryTopic: the topic to which publish the nav_msgs/Odometry messages that store an estimate of the position and velocity of a robot in free space, default="odom"  
+ odometryFrame: the name to use to broadcast the TF frame for odometry, default="odom"  
+ robotBaseFrame: the name of the TF frame for the base (root) link of the robot, default="robot_footprint"  
+ diff_drive_publishTf: boolean that sets whether to publish any TF data at all, default="true"  
+ diff_drive_publishOdomTF: boolean that sets whether to publish the odom TF. Set to false for situations where a different source for simulated odom is used, default="true"   

These parameters can also be modified by passed in an argument when running the `spawn_rtab_dumpster.launch` file like this:  
`$ roslaunch rtab_dumpster spawn_rtab_dumpster.launch odometryTopic:=odom_perfect`  
 
## Repository architecture
### Directories
+ **urdf/** : (required) contains the files that generate the robot model and provide simulated actuators and sensors
+ **meshes/** : (required) contains the mesh files that are part of the geometry of that robot
+ **config/** : (optional) contains YAML files that store the Navigation Stack configuration files for the robot
+ **rviz/** : (optional) contains Rviz configuration settings for displaying the robot model
+ **launch/** : (optional) contains launch file for running the robot model in Gazebo
+ **worlds/** : (optional) contains scene/environment files for Gazebo
+ **maps/** : (optional) contains the occupancy grid based maps required for navigation

### Robot model files
+ **rtab_dumster.xacro** : the xacro file that generates the urdf description file of the robot
+ **rtab_dumster.gazebo** : contains the Gazebo plugins that provide an interface to control the robot wheels and simulate the laser sensor
+ **kinect.xacro** : contains the plugins to simulate a Kinect sensor in Gazebo

## Direct usage
- Clone this repository into a ROS catkin workspace
- Build and source the workspace
- To launch this package including an empty Gazebo world and Rviz: `roslaunch rtab_dumpster demo.launch`
or  
- To spawn the robot into another already opened Gazebo world:  
`$ roslaunch rtab_dumpster robot_description.launch`  
`$ roslaunch rtab_dumpster spawn_rtab_dumpster.launch`  

If you want to move the robot using a keyboard you will also need to start a teleop node.  
To run the robot with the Navigation Stack type in a new window: `roslaunch rtab_dumpster amcl.launch`  

To view raw images on the topic /camera/rgb/image_raw, use:  
`$ rosrun image_view image_view image:=/camera/rgb/image_raw`  

## Known Issues
+ Kinect camera in Gazebo does not publish topics: It seems there is a bug with Gazebo 7.0.0 inside Virtual Machines, which then got resolved in a later version of Gazebo 7.
The solution is to upgrade Gazebo.

This package has only been tested on Ubuntu 16.04 LTS with ROS Kinetic and Gazebo 7.0 and 7.15.
