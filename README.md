# OpenPaws: Open-Source Quadruped Robotic Framework

OpenPaws is an open-source framework designed for building Field Oriented Control (FOC) motor-based quadruped robotic pets. This project focuses on delivering low-cost, modular, and cross-platform solutions in both software and hardware to robotics enthusiasts and developers.

## Our Philosophy

OpenPaw is a project created by and for the open-source community. We believe in the principles of transparency, collaboration, and innovation. By sharing our work, we hope to contribute to the growth of the robotics ecosystem and empower others to build upon it.

## Leg Assembled

<video width="300" height="200" autoplay="true" src="https://github.com/wangpuhk1/openpaws/blob/main/readme/leg.mp4"></video>

## Installation

## Step 1: Build ROS Workspace

```bash
# Clone repository
git clone https://github.com/wangpuhk1/openpaws.git

source /opt/ros/melodic/setup.bash

# Navigate to ROS workspace
cd openpaws/software/ROS1

# Initialize and build packages
catkin_make
```

## Step 2: Launch Gazebo Simulation

```bash
# Source environment and launch simulation
cd openpaws/software/ROS1
source devel/setup.bash  # Load ROS environment variables
roslaunch openpaws_config gazebo.launch
```
<img src="https://github.com/wangpuhk1/openpaws/blob/main/readme/gazebo.png" width="300px">

## Step 3: Start Teleoperation (New Terminal)

```bash
# In separate terminal session
cd openpaws/software/ROS1
source devel/setup.bash  # Re-source environment
roslaunch openpaws_teleop teleop.launch  # Activate control interface
```

## Step 4: Hardware Integration

Create a hardware interface for your actuators that is able to do the following:

- Subscribe to [trajectory_msgs/JointTrajectory](http://docs.ros.org/melodic/api/trajectory_msgs/html/msg/JointTrajectory.html) . This ROS message contains the joint angles (12DOF) that the actuators can use to move the robot.

- Publish all the actuators' current angle using [sensor_msgs/JointState](http://docs.ros.org/melodic/api/sensor_msgs/html/msg/JointState.html) to 'joint_states' topic.

- Control the actuators and read its angle (optional) programmatically.

## Community

Join our community to share ideas, ask questions, and collaborate:  

- [Discord Channel](https://discord.gg/qjGJGtSM)
- [wechat/微信]

<img src="https://github.com/wangpuhk1/openpaws/blob/main/readme/code.jpg" width="300px">

## License

OpenPaw is licensed under the MIT License. See `LICENSE` for more details.

## Acknowledgments

Some code and design are borrowed from following projects:  
[Cheetah](https://github.com/mit-biomimetics/Cheetah-Software)  
[Champ](https://github.com/chvmp/champ)  
[3D model Design](https://oshwhub.com/gulu666/detector-disaster-scene-3d-reconstruction-robot-dog)  
Thanks for their contributions!
