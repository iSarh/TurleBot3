# TurleBot3 ROS1_Noetic

This repository is about how to bring up the TurtleBot3 and perform navigation using ros1 noetic

**What Is TurtleBot3**

TurtleBot3 is an educational robot that supports learning and research in robotics and artificial intelligence. It features a flexible and customizable design and operates on the Robot Operating System (ROS). TurtleBot3 has sensors such as cameras and LIDAR, making it suitable for various projects like mapping and environmental interaction. Its compact and lightweight design makes it an excellent choice for students and researchers in robotics.
 
**1. Setting Environment**

***Requirement***
- ubuntu 20.04
- ROS Noetic
- Gazebo
  
for more detailed installation instructions please refer to the setup section of the TurtleBot3 manual: https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup

![image](https://github.com/user-attachments/assets/41d313c3-f765-4447-bef4-559f8f56c538)

**2. Install dependency packages & build**

this is the step of installing the required dependency packages for TurtleBot3

Install ROS Packages:

```bash
sudo apt-get install ros-noetic-joy ros-noetic-teleop-twist-joy \
  ros-noetic-teleop-twist-keyboard ros-noetic-laser-proc \
  ros-noetic-rgbd-launch ros-noetic-rosserial-arduino \
  ros-noetic-rosserial-python ros-noetic-rosserial-client \
  ros-noetic-rosserial-msgs ros-noetic-amcl ros-noetic-map-server \
  ros-noetic-move-base ros-noetic-urdf ros-noetic-xacro \
  ros-noetic-compressed-image-transport ros-noetic-rqt* ros-noetic-rviz \
  ros-noetic-gmapping ros-noetic-navigation ros-noetic-interactive-markers
```

Install TurtleBot3 Packages:

```bash
sudo apt install ros-noetic-dynamixel-sdk
sudo apt install ros-noetic-turtlebot3-msgs
sudo apt install ros-noetic-turtlebot3
```
**3. Operate gazebo & Teleop Turtlebot3**

visit the simulation of the TurtleBot3 manual for more detailed: https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#gazebo-simulation

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

![image](https://github.com/user-attachments/assets/3e15cbe1-8f84-4f52-99b7-59d55b4ea484)

Create a new terminal and run the ``teleoperation`` node

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_teleop turtlebot_teleop_key.launch
```
