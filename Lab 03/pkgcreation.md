# Dependency Installation

Run the following commands to setup dependencies required for the open manipulator.

```Linux
sudo apt install ros-humble-python* ros-humble-rqt*
sudo apt-get install ros-humble-gazebo* ros-humble-moveit*
```

# Package Creation

Move inside the ROS workspace and clone open manipulator package
Assuming workspace name is 'robotics'.

```Linux
cd robotics/src
mkdir manipulator
cd manipulator
git clone -b ros2 https://github.com/ROBOTIS-GIT/DynamixelSDK.git
git clone -b ros2 https://github.com/ROBOTIS-GIT/dynamixel-workbench.git
git clone -b ros2 https://github.com/ROBOTIS-GIT/dynamixel-workbench-msgs.git
git clone -b ros2 https://github.com/ROBOTIS-GIT/open_manipulator.git
git clone -b ros2 https://github.com/ROBOTIS-GIT/open_manipulator_msgs.git
git clone -b ros2 https://github.com/ROBOTIS-GIT/open_manipulator_simulations.git
git clone -b ros2 https://github.com/ROBOTIS-GIT/robotis_manipulator.git
```

Move to workspace root and build the package

```Linux
colcon build --symlink-install
```
