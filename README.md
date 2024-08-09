

# TurtleBot3 Simulation and Navigation

This guide demonstrates the integration of TurtleBot3 models (Burger and Waffle Pi) into ROS with Gazebo simulation. It covers setting up the simulation environment, performing SLAM (Simultaneous Localization and Mapping), and configuring navigation.

## **Table of Contents**

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Installation and Setup](#installation-and-setup)
   - [Clone Repositories](#clone-repositories)
   - [Set Up ROS Workspace](#set-up-ros-workspace)
   - [Move Repositories to Workspace](#move-repositories-to-workspace)
   - [Build Your Workspace](#build-your-workspace)
4. [Running Simulations](#running-simulations)
   - [TurtleBot3 Burger](#turtlebot3-burger)
   - [TurtleBot3 Waffle Pi](#turtlebot3-waffle-pi)
5. [Controlling TurtleBot3](#controlling-turtlebot3)
6. [SLAM and Navigation](#slam-and-navigation)
   - [Performing SLAM](#performing-slam)
   - [Navigation](#navigation)
7. [Customization](#customization)
   - [Configuration Files](#configuration-files)
   - [URDF Models](#urdf-models)
   - [Launch Files](#launch-files)
8. [Troubleshooting](#troubleshooting)
9. [Additional Information](#additional-information)

## **Overview**

- **TurtleBot3 Models**: Burger, Waffle Pi
- **Simulation Environments**: Empty World, TurtleBot3 World, TurtleBot3 House
- **Capabilities**: SLAM, Navigation, Teleoperation

## **Prerequisites**

- ROS Noetic installed
- Gazebo installed
- Basic knowledge of ROS and Gazebo

## **Installation and Setup**

### **Clone Repositories**

Clone the required repositories into your workspace:

```bash
# Clone the TurtleBot3 Simulations repository
git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git

# Clone the TurtleBot3 Gazebo Plugin repository
git clone https://github.com/ROBOTIS-GIT/turtlebot3_gazebo_plugin.git
```

### **Set Up ROS Workspace**

Create and configure your ROS workspace:

```bash
# Create a workspace directory
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
```

### **Move Repositories to Workspace**

Move the cloned repositories into the `src` directory:

```bash
# Move the repositories into the src folder
mv ~/turtlebot3_simulations ~/catkin_ws/src/
mv ~/turtlebot3_gazebo_plugin ~/catkin_ws/src/
```

### **Build Your Workspace**

Navigate to your ROS workspace, build it, and source the setup file:

```bash
# Navigate to the workspace
cd ~/catkin_ws

# Build the workspace
catkin_make

# Source the workspace
source devel/setup.bash
```

## **Running Simulations**

### **TurtleBot3 Burger**

- **Empty World**:
  ```bash
  roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch model:=burger
  ```
![image](https://github.com/user-attachments/assets/0ea381f8-dbba-49ac-980e-d8de670b9898)

- **TurtleBot3 World**:
  ```bash
  roslaunch turtlebot3_gazebo turtlebot3_world.launch model:=burger
  ```

- **TurtleBot3 House**:
  ```bash
  roslaunch turtlebot3_gazebo turtlebot3_house.launch model:=burger
  ```

### **TurtleBot3 Waffle Pi**

- **Empty World**:
  ```bash
  roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch model:=waffle_pi
  ```

- **TurtleBot3 World**:
  ```bash
  roslaunch turtlebot3_gazebo turtlebot3_world.launch model:=waffle_pi
  ```

![image](https://github.com/user-attachments/assets/63e5c2c8-ba91-408e-a3b0-16a42ad95610)

- **TurtleBot3 House**:
  ```bash
  roslaunch turtlebot3_gazebo turtlebot3_house.launch model:=waffle_pi
  ```

![image](https://github.com/user-attachments/assets/d9396f74-f3e1-436f-b6ed-f4c972eebbe3)

## **Controlling TurtleBot3**

To control TurtleBot3 using keyboard commands, launch the teleoperation node:

```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
Use the following keys to control the robot:

W: Move forward
S: Move backward
A: Turn left
D: Turn right
X: Stop

## **SLAM and Navigation**

### **Performing SLAM**

Start SLAM to create a map of your environment:

```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch
```

Drive the robot around to explore the environment. Save the generated map:

```bash
rosrun map_server map_saver -f ~/map
```

### **Navigation**

Load the saved map and start the navigation stack:

```bash
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=/home/<your_username>/map.yaml
```

Replace `<your_username>` with your actual username.

## **Customization**

### **Configuration Files**

Modify configuration files for parameters related to sensors, controllers, and other settings. These files are located in the `config` folder of the packages.

### **URDF Models**

To change the robot model, edit URDF files located in the `urdf` directory within the `turtlebot3_description` package.

### **Launch Files**

Customize launch files in the `launch` directory of each package to fit your needs.

## **Troubleshooting**

- **Verify Installation**: Ensure all packages are installed:
  ```bash
  rospack list | grep turtlebot3
  ```

- **Run Simulations**: Test simulations to ensure the TurtleBot3 models behave as expected.

- **Check Logs**: Use ROS logs to troubleshoot issues:
  ```bash
  roslaunch <package> <launch_file> --screen
  ```

## **Additional Information**

- **Dependencies**: Ensure all dependencies are installed:
  ```bash
  rosdep update
  rosdep install --from-paths src --ignore-src -r -y
  ```

- **Documentation**: Document your setup and configurations for future reference.

---
