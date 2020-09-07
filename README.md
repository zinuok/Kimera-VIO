***
# Kimera-VIO
+ **hardware setup**
    + jetson TX2 - Jetpack 4.2
    + jetson AGX Xavier
    + jetson Xavier NX - Jetpack 4.4
    + realsense D435i (color, infra1, infra2)
    + pixhawk4 mini
    <br>
+ **software setup**
    + Ubuntu: 18.04 
    + ROS: Melodic 
    + OpenCV 3.4.1
    <br>
+ **github link**: [MIT-SPARK](https://github.com/MIT-SPARK/Kimera-VIO)
***
<br>




# Index
### 1. Prerequisites
####    &nbsp;&nbsp;&nbsp;&nbsp;● GTSAM >= 4.0
####    &nbsp;&nbsp;&nbsp;&nbsp;● OpenCV >= 3.3.1
####    &nbsp;&nbsp;&nbsp;&nbsp;● OpenGV
####    &nbsp;&nbsp;&nbsp;&nbsp;● Glog, Gflags
####    &nbsp;&nbsp;&nbsp;&nbsp;● Gtest (installed automagically)
####    &nbsp;&nbsp;&nbsp;&nbsp;● DBoW2
####    &nbsp;&nbsp;&nbsp;&nbsp;● Kimera-RPGO
####    &nbsp;&nbsp;&nbsp;&nbsp;● ANMS
### 2. Install
### 3. Jetson Boards
####    &nbsp;&nbsp;&nbsp;&nbsp;● Actually, there is no installation difference among TX2, Xavier, and NX
### 4. Run
<br><br>

## 1. Prerequisites & Install
+ refer the installation guide from [install](https://github.com/MIT-SPARK/Kimera-VIO/blob/master/docs/kimera_vio_install.md)

## 3. Jetson Boards
#### ● Actually, no installation difference among TX2, Xavier, and NX

## 4. Run
#### ● you have to get a calibration data using [kalibr](https://github.com/zinuok/kalibr)
```
$ roslaunch realsense2_camera rs_camera.launch
$ roslaunch mavros px4.launch
$ roslaunch vins_estimator realsense_color.launch
$ roslaunch vins_estimator vins_rviz.launch
```

