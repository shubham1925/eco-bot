<img src="/data/ecobot.png"/>

[![Build Status](https://travis-ci.org/Prasheel24/eco-bot.svg?branch=master)](https://travis-ci.org/Prasheel24/eco-bot)
[![Coverage Status](https://coveralls.io/repos/github/Prasheel24/eco-bot/badge.svg?branch=master&service=github)](https://coveralls.io/github/Prasheel24/eco-bot?branch=master&service=github)
[![License BSD 3-Clause](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://github.com/Prasheel24/eco-bot/blob/master/LICENSE)
[![Documentation](https://img.shields.io/badge/docs-generated-brightgreen.svg)](https://github.com/Prasheel24/eco-bot/docs)
---

## Authors

* **Raj Prakash Shinde** [GitHub](https://github.com/RajPShinde)
<br>I am a Masters in Robotics Engineering student at the University of Maryland, College Park. My primary area of interest are Legged Robotics and Automation. 
* **Prasheel Renkuntla** [GitHub](https://github.com/Prasheel24)
<br>I am a Master's in Robotics Engineering student at the University of Maryland, College Park. My primary area of interest is in Vision integrated Robot Systems.

## Overview
This is ROS Package developed for ACME Robotics to demonstrate the functionality of their new eco-bot in a simulated environment.

## Description
The eco-bot is a trash collecting robot, that once given the location of trash, goes to the location and collects all the trash. 
<br>The ecobot first needs to generate a map of the area, which is done by using GMapping and RRT Exploration package. The RRT Exploration Package uses the Rapidly-Exploring Random Tree (RRT) path planning algorithm. A LiDAR is used for GMapping insted of a Laser, which enables to generate map very quickly.
<br>Once the map is generated, it is stored as a pgm image file. The generated pgm file is used later during the trash collection. The ecobot is assumed to be connected to internet, from where it receives the trash location. The robot then navigated to the trash loacation, using A* Algorithm. After the robot reaches near the trash, it collects the trash. 
<img src="/data/pic.png"/>
## Sprint Planning and Discussion
Sprint- [Link](https://docs.google.com/document/d/1_uG7fMXPrtZlpRLsgD74NdLRX3DKDXxCicppZWBDNvQ)

## Agile Iterative Process Log
Log- [Link](https://docs.google.com/spreadsheets/d/1DkxCx4_GxvRXjRTTrmgZvdOQ4z0DMrpGEavg439tQak)

## Presentation
ecobot presentation- [Link](https://docs.google.com/presentation/d/1IUGE4VEXWjybyAAlP8kH_GjFQwXpRnje)

## Dependencies
1. Ubuntu 16.04
2. C++ 11/14/17
3. ROS Kinetic- [Install](http://wiki.ros.org/kinetic/Installation)
4. Turtlebot stack
<br> Install by running following command
```

sudo apt-get install ros-kinetic-turtlebot-gazebo ros-kinetic-turtlebot-apps ros-kinetic-turtlebot-rviz-launchers
```
5. RRT Exploration Package by [hasauino](http://wiki.ros.org/rrt_exploration)
6. GMapping
7. amcl
8. Navigation stack

## Build
Steps to build
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
source devel/setup.bash
cd src/
git clone https://github.com/Prasheel24/eco-bot
git clone https://github.com/hasauino/rrt_exploration.git
cd ~/catkin_ws/
catkin_make
```
## Run
**Generate Map**
<br> Open a new Terminal
```
source devel/setup.bash
roslaunch ecobot Mapping.launch
```
Now on rviz provide four publish points in following order, the fifth should be inside the world/room.
<img src="/data/seq.png"/>

**Save Map to Directory**
Once a satisfactory map is generated (Open a new Terminal)
```
rosrun map_server map_saver map:=/robot_1/map -f CollectorSpace
```

**Collect Garbage**
Press Ctrl+ C to close the previous sessions and start a this in a new Terminal
```
source devel/setup.bash
roslaunch ecobot Collecting.launch
```
wait till the odom is received on main terminal then Open a new Terminal,
```
source ./devel/setup.bash
rosrun ecobot trash
```
**Record bag while Mapping and Collecting**
<br> to record Mapping in a bag file, pass a record:=true argument as shown below (Open a new Terminal)
```
source devel/setup.bash
roslaunch ecobot Mapping.launch record:=true
```
<br> to record Collecting in a bag file, pass a record:=true argument as shown below (Open a new Terminal)
```
source devel/setup.bash
roslaunch ecobot Collecting.launch record:=true
```

**View Log Levels**
To view Log levels using rqt console and rqt logger level
Open a new Terminal
```
rosrun rqt_console rqt_console
```
Open a new Terminal
```
rosrun rqt_logger_level rqt_logger_level
```

**Run Bag Files**
Go to the directory consisting bag file(Open a new Terminal)
Run roscore
```
roscore
```
Open a new terminal
```
cd ~/catkin_ws/
source devel/setup.bash
cd ~/catkin_ws/src/eco-bot/results/
rosbag play recording.bag 
```

## Run Test
To run gtest and rostest (Open a new Terminal)
```
catkin_make run_tests_ecobot
```

## Gererate Doxygen docs
In a new terminal
```
sudo apt-get install doxygen
sudo apt install doxygen-gui
doxywizard
```


## Bugs
ecobot sometimes take more time to collect/delete garbage even after reaching near, because A* path planner takes more time to achieve exact target location.

## References
* http://wiki.ros.org/
* http://wiki.ros.org/rrt_exploration
* http://wiki.ros.org/navigation/Tutorials/Writing%20A%20Global%20Path%20Planner%20As%20Plugin%20in%20ROS
* https://www.geeksforgeeks.org/a-search-algorithm/

## Contributions
* **RRT Exploration Package-** *H. Umari and S. Mukhopadhyay, "Autonomous robotic exploration based on multiple rapidly-exploring randomized trees," 2017 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), Vancouver, BC, 2017, pp. 1396-1402.*
*doi: 10.1109/IROS.2017.8202319*
*keywords: {edge detection;mobile robots;multi-agent systems;navigation;path planning;random processes;robot vision;trees (mathematics);efficient robotic exploration;three-dimensional space;autonomous robotic exploration;randomized trees;efficient robotic navigation;autonomous exploration strategies;edge detection;dimensional exploration;multiple Rapidly-exploring Random Trees;RRT algorithm;Robot Operating System framework;frontier detection;image processing;Detectors;Image edge detection;Robot sensing systems;Path planning;Navigation},*
URL: http://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8202319&isnumber=8202121
* **Logo -** https://www.flaticon.com/authors/nhor-phai

## Disclaimer
```
BSD 3-Clause License

Copyright (c) 2019, Raj Shinde
Copyright (c) 2019, Prasheel Renkuntla
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its
   contributors may be used to endorse or promote products derived from
   this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```
