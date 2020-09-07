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
+ **github link**: [MIT-SPARK](https://github.com/MIT-SPARK/Kimera-VIO-ROS)
***
<br>




# Index
### 1. Prerequisites & install
####    &nbsp;&nbsp;&nbsp;&nbsp;● GTSAM >= 4.0
####    &nbsp;&nbsp;&nbsp;&nbsp;● OpenCV >= 3.3.1
####    &nbsp;&nbsp;&nbsp;&nbsp;● OpenGV
####    &nbsp;&nbsp;&nbsp;&nbsp;● Glog, Gflags
####    &nbsp;&nbsp;&nbsp;&nbsp;● Gtest (installed automagically)
####    &nbsp;&nbsp;&nbsp;&nbsp;● DBoW2
####    &nbsp;&nbsp;&nbsp;&nbsp;● Kimera-RPGO
####    &nbsp;&nbsp;&nbsp;&nbsp;● ANMS
### 2. Truoble Shooting
### 3. Jetson Boards
####    &nbsp;&nbsp;&nbsp;&nbsp;● Actually, there is no installation difference among TX2, Xavier, and NX
### 4. Run
<br><br>

## 1. Prerequisites & Install
+ install guide using ROS from [here](https://github.com/MIT-SPARK/Kimera-VIO-ROS#1-installation)
```
$ sudo apt install -y ros-melodic-image-geometry ros-melodic-pcl-ros ros-melodic-cv-bridge ros-melodic-image-proc*
$ sudo apt -y install -y --no-install-recommends apt-utils
$ sudo apt-get install -y \
      cmake build-essential unzip pkg-config autoconf \
      libboost-all-dev \
      libjpeg-dev libpng-dev libtiff-dev \
      libvtk6-dev libgtk-3-dev \
      libatlas-base-dev gfortran \
      libparmetis-dev \
      python-wstool python-catkin-tools
```
+ Kimera VIO ROS wrapper install
```
# Download #
$ cd ~/catkin_ws
$ catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release && source ~/catkin_ws/devel/setup.bash
$ cd ~/catkin_ws/src && git clone git@github.com:MIT-SPARK/Kimera-VIO-ROS.git

# Install dependencies from rosinstall file using wstool #
$ wstool merge Kimera-VIO-ROS/install/kimera_vio_ros_ssh.rosinstall
$ wstool update

# Compile #
$ cd ~/catkin_ws && catkin build -j $(nproc)
$ source ~/catkin_ws/devel/setup.bash
```
## 2. Trouble Shooting
+ Project 'image_proc' specifies '/usr/include/opencv' as an include dir,
  which is not found while catkin builds 'disparity_image_proc' <br>. This error may occur if you have built OpenCV manually, not using sudo apt install command. <br>
=> In line 96 of /opt/ros/melodic/share/image_proc/cmake/image_procConfig.cmake, <br>
&nbsp;&nbsp;change:
```
set(_include_dirs "include;/usr/include;/usr/include/opencv")
to
set(_include_dirs "include;/usr/include;/usr/local/include/opencv")
```
+ While catkin builds 'opencv3_catkin', 
```
Some (but not all) targets in this export set were already defined.

  Targets Defined: gflags_shared;gflags_nothreads_shared<br>
  Targets not yet defined: gflags_static;gflags_nothreads_static<br>
```
=> This is because glogs & gflags already installed via sudo apt install invoke crash. So remove those and try to compile the 'opencv3_catkin'
```
# remove #
$ sudo apt remove -y libgflags*
$ sudo apt remove -y sudo apt install libgoogle-glog*

# build opencv3_catkin #
$ catkin build -j $(nproc) opencv3_catkin

# reinstall glog & catkin build #
$ sudo apt install -y libgoogle-glog*
$ catkin build -j $(nproc)
```


## 3. Jetson Boards
#### ● Actually, no installation difference among TX2, Xavier, and NX

## 4. Run
#### ● you have to get a calibration data using [kalibr](https://github.com/zinuok/kalibr)
```
$ roslaunch
```

