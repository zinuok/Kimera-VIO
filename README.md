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

## 1. Prerequisites
### ● GTSAM >= 4.0: from [GTSAM](https://github.com/borglab/gtsam)
+ Boost >= 1.58, CMake >= 3.0, gcc >= 4.7.3
```
$ sudo apt install -y libboost-all-dev
$ sudo apt install -y cmake
$ git clone https://github.com/borglab/gtsam.git
$ cd gtsam && mkdir build && cd build
$ cmake ../
$ make check -j6 #optional, runs unit tests
$ sudo make install -j6
```

### ● OpenCV >= 3.3.1: from [zinuok/OpenCV install](https://github.com/zinuok/Xavier_NX#1-opencv-ver-341-install-1)

### ● OpenGV: from [OpenGV](https://github.com/laurentkneip/opengv)
+ If a message like "Could NOT find Eigen (missing: EIGEN_INCLUDE_DIR EIGEN_VERSION_OK)" appears. It's certainly because that you does not have Eigen3 installed on your computer system path. You can specify to cmake the path where Eigen is located by adding: mkdir build && cd build && cmake .. -DEIGEN_INCLUDE_DIR:STRING="EigenIncludePath" && make
```
$ git clone https://github.com/laurentkneip/opengv.git
$ cd opengv && mkdir build && cd build
$ cmake ../
$ make -j6
$ sudo make install -j6
```

### ● Glog, Gflags
```
$ sudo apt install -y libgflags-dev
$ sudo apt install -y libgoogle-glog-dev
```

### ● Gtest (installed automagically)
+ it is installed automagically

### ● DBoW2: from [dbow2](https://github.com/dorian3d/DBoW2)
```
$ git clone https://github.com/dorian3d/DBoW2.git
$ cd DBoW2 && mkdir b uild && cd build
$ cmake ../ && make -j6
$ sudo make install -j6
```

### ● Kimera-RPGO: from [kimera-rpgo](https://github.com/MIT-SPARK/Kimera-RPGO)
```
$ git clone https://github.com/MIT-SPARK/Kimera-RPGO.git
$ cd Kimera-RPGO && mkdir build && cd build
$ cmake ..
$ make -j6
```

### ● ANMS: from [anms](https://github.com/BAILOOL/ANMS-Codes)
```
$ git clone https://github.com/BAILOOL/ANMS-Codes.git
```
<br><br>

## 2. Install
+ from [kimera install](https://github.com/MIT-SPARK/Kimera-VIO/blob/master/docs/kimera_vio_install.md)
```
$ cd ~/catkin_ws/src
$ git clone https://github.com/HKUST-Aerial-Robotics/VINS-Mono.git
$ cd ../ && catkin build -DCMAKE_BUILDTYPE=Release -j3
$ source ~/catkin_ws/devel/setup.bash
```

## 3. Jetson Boards
#### ● Actually, no installation difference among TX2, Xavier, and NX
<br><br>

## 4. Run
#### ● you have to get a calibration data using [kalibr](https://github.com/zinuok/kalibr)
```
$ roslaunch realsense2_camera rs_camera.launch
$ roslaunch mavros px4.launch
$ roslaunch vins_estimator realsense_color.launch
$ roslaunch vins_estimator vins_rviz.launch
```

