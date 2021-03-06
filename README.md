# Localization and Mapping
Overview of the subsystem:

![SLAM Overview](SLAM_ROS_Stack.png)

Note : Ellipses correspond to ROS Nodes and Rectangles correspond to the corresponding topics.

##  Build and Working Status
|Node|Build Status|Working Status|Credits|Future Work|
|----|------------|--------------|-------|------|
|cartographer_ros|![build_passing](https://img.shields.io/badge/Build-Passing-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|![Status_working](https://img.shields.io/badge/Status-Working-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|[Google Cartographer](https://github.com/googlecartographer)|Tuning Parameters|
|img_to_laser|![build_passing](https://img.shields.io/badge/Build-Passing-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|![Status_working](https://img.shields.io/badge/Status-Working-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|[IGVC IITK](https://github.com/IGVC-IITK)<br/>(Built from scratch)|Adding support for multiple virtual lidars|
|robot_localization|![build_passing](https://img.shields.io/badge/Build-Passing-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|![Status_need_modifications](https://img.shields.io/badge/Status-Need_modifications-orange.svg?longCache=true&longCache=true&style=flat-square)|[Charles River Analytics](https://github.com/cra-ros-pkg/robot_localization)|Tweaking Parameters|
|ros0xrobot|![build_passing](https://img.shields.io/badge/Build-Passing-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|![Status_working](https://img.shields.io/badge/Status-Working-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|[NEX Robotics](http://www.nex-robotics.com/)|-|
|scanignore|![build_passing](https://img.shields.io/badge/Build-Passing-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|![Status_need_modifications](https://img.shields.io/badge/Status-Need_modifications-orange.svg?longCache=true&longCache=true&style=flat-square)|[IGVC IITK](https://github.com/IGVC-IITK)<br/>(Built from scratch)|-|
|tf_calibration|![build_passing](https://img.shields.io/badge/Build-Passing-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|![Status_working](https://img.shields.io/badge/Status-Working-brightgreen.svg?longCache=true&longCache=true&style=flat-square)|[IGVC IITK](https://github.com/IGVC-IITK)<br/>(Built from scratch)|-|
## cartographer_ros
[Cartographer](https://github.com/googlecartographer/cartographer) is a system that provides real-time simultaneous localization and mapping ([SLAM](https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping)) in 2D and 3D across multiple platforms and sensor configurations.

![Cartographer SLAM Example](https://j.gifs.com/wp3BJM.gif)


## img_to_laser

This node gives laser scan as read by a virtual LiDAR put at some position on binary classified image. Used for mapping the data obtained from the vision pipeline via mapping nodes that require data to be in laser scan form only.

![Image to Laser-Scan Example](img_to_laser/img_to_laser.png)

## robot_localization

This node gives sensor-fused odometry. (Currently using wheel encoders, visual odometry and an IMU).

It is an open-source ROS package. Added an extra feature. Measured, calculated and tuned covariance matrices based on the robot dynamics, sensor configuration and the environment conditions.

## img_to_pcloud

The node gives a point cloud from a binary classified image using its top-left corner as a reference point.

## ros0xrobot

This node gives raw wheel odometry (and also provides a low-level controller) for the Firebird 0xDelta robot. This node is basically a driver for the robot's motors and encoders.

Acquired from NEX Robotics and added some fixes.

## rplidar_ros

This node acts as the driver for the range sensors (LiDARs) mounted on the robot. It generates filtered scans from the laser scan topics by removing range data that corresponds to points on the robot itself (so that the robot does not map itself).

Configured for the Firbird 0xDelta (Daksh IITK).

## tf_calibration

This is a **one-time** node used for calibrating sensor frames. It just publishes a tf that can be updated in real time using dynamic_reconfigure. One can visualize the sensor data on Rviz and then tune the tf till the data matches visually. Was used for LiDAR-LiDAR calibration on the Firebird 0xDelta.

![tf Calibration Example](tf_calibration/tf_calibration.png)
