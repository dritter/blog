---
layout: post
title: ROS Hydro + Baxter SDK + Gazebo + MoveIt!
category: How-To
tags: ros baxter gazebo moveit program how-to
description: ros know how series
---

## INSTALL KEYS AND PACKAGES

```sh
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu precise main" > /etc/apt/sources.list.d/ros-latest.list'
wget http://packages.ros.org/ros.key -O - | sudo apt-key add -

sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu precise main" > /etc/apt/sources.list.d/gazebo-latest.list'
wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -

sudo apt-get update
sudo apt-get install -y ros-hydro-desktop-full python-rosinstall git-core python-argparse python-wstool python-vcstools python-rosdep ros-hydro-control-msgs ros-hydro-joystick-drivers python-wstool python-rosdep ros-hydro-pcl-conversions ros-hydro-control-msgs ros-hydro-cmake-modules ros-hydro-qt-build ros-hydro-moveit-full ros-hydro-driver-common ros-hydro-image-common ros-hydro-rostest gazebo ros-hydro-moveit-full ros-hydro-gazebo-ros-pkgs ros-hydro-gazebo-ros-control

sudo rosdep init
rosdep update
```

## WORKSPACE

```sh
mkdir -p $P/src

cd $P/src
source /opt/ros/hydro/setup.bash
catkin_init_workspace
wstool init .
wstool merge https://raw.githubusercontent.com/RethinkRobotics/baxter/master/baxter_sdk.rosinstall

git clone git@github.com:RethinkRobotics/baxter_simulator.git
git clone https://github.com/ros-planning/moveit_robots.git
wstool merge baxter_simulator/baxter_simulator.rosinstall
wstool update

cd $P
wget https://github.com/RethinkRobotics/baxter/raw/master/baxter.sh
chmod +x baxter.sh
```

## BUILD

```sh
cd $P
catkin_make
catkin_make install
```

> Modify `baxter.sh` to set hosts and hydro

## TEST

### TERMINAL 1


```sh
cd $P
./baxter.sh sim
roslaunch baxter_gazebo baxter_world.launch
```

### TERMINAL 2

```sh
cd $P
./baxter.sh sim
rosrun baxter_interface joint_trajectory_action_server.py
```

### TERMINAL 3

```sh
cd $P
./baxter.sh sim
roslaunch baxter_moveit_config demo_baxter.launch
```
