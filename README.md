# TurleBot3 ROS1_Noetic

This repository is about how to bring up the TurtleBot3 and perform navigation using ros1 noetic

## What Is TurtleBot3

TurtleBot3 is an educational robot that supports learning and research in robotics and artificial intelligence. It features a flexible and customizable design and operates on the Robot Operating System (ROS). TurtleBot3 has sensors such as cameras and LIDAR, making it suitable for various projects like mapping and environmental interaction. Its compact and lightweight design makes it an excellent choice for students and researchers in robotics.
 
## 1. Setting Environment

***Requirement***
- ubuntu 20.04
- ROS Noetic
- Gazebo
  
for more detailed installation instructions please refer to the setup section of the TurtleBot3 manual: https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup

![image](https://github.com/user-attachments/assets/41d313c3-f765-4447-bef4-559f8f56c538)

## 2. Install dependency packages & build

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
## 3. Operate gazebo & Teleop Turtlebot3

visit the simulation of the TurtleBot3 manual for more detailed: https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#gazebo-simulation

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

![image](https://github.com/user-attachments/assets/3e15cbe1-8f84-4f52-99b7-59d55b4ea484)

Create a new terminal and run the ``teleoperation`` node

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
> [!NOTE]
> If the turtle not moving try the following command to make the gazebo subscribe to cmd_vel.
> ```bash
> sudo apt-get install ros-noetic-gazebo-ros-pkgs ros-noetic-gazebo-ros-control
> ```
![turtlebot3](https://github.com/user-attachments/assets/25b82d4d-6df3-4fcb-81bc-1e9860d5e775)


## 4. SLAM & Save the map

Run gazebo using an identical command 

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

Create a new terminal and run the turtle3 slam node

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```

![image](https://github.com/user-attachments/assets/45439afc-a4e3-4aac-80ac-c148a9f3bb75)

Create a new terminal and run the Teleoperation Node

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
Now move the turtle3 burger with your keyboard to create a map 

![turtlewithslam - Made with Clipchamp](https://github.com/user-attachments/assets/bf8e6f2e-5589-4725-bf69-826c5dc17517)


## 5. Save map 
when you have finished creating the map create new terminal and save the map 

```bash
rosrun map_server map_saver -f ~/map
```
![image](https://github.com/user-attachments/assets/85dcbc36-4278-492b-9439-d0887c40e86a)

## 5. launch Navigation

In the previous SLAM section, TurtleBot3 World is used to creat a map. The same Gazebo environment will be used for Navigation.

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
Open a new terminal and run the Navigation node.

```bash
 export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```
When turtle3 navigation is executed you can see the rivz with the map we created earlier

![Screenshot 2024-08-10 001228](https://github.com/user-attachments/assets/57f56a17-6397-415c-ba03-0bf8802e025c)

click the 2D pose to estimate button in rivz menu bar then click where the turtle3 is located and drag to the direction the robot is facing 

finally, click the 2D navigation goal button and specify the destination and direction

you will see the turtle3 moving toward the destination


![turtle3 navigation](https://github.com/user-attachments/assets/f0a04075-89d8-4411-a98f-001020ea941b)

