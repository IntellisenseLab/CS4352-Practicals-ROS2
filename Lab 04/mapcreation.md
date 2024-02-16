# Using Cartographer

This lab is to understand how to use the Cartographer for mapping and localization.

As the initial step source the ROS2 installation.

```Linux
source install/setup.bash
```

Check if there are cartographer packages.

```Linux
ros2 pkg list |grep cartographer
```
You will get 
cartographer_ros
cartographer_ros_msgs

If you don’t have “cartographer_ros” and “cartographer_ros_msgs”, you can install cartographer by performing the following:
```Linux
sudo apt install ros-humble-cartographer
```

Check if there are turtlebot3* packages.

```Linux
ros2 pkg list | grep turtlebot3
```

If you don’t have turtlebot3 packages, you can install debian packages or from source code.
![Screenshot 2024-02-16 111747](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/assets/58034992/40dd06b5-596b-46ba-a519-6ddeacd12bde)

Set up turtlebot model
```Linux 
export TURTLEBOT3_MODEL=burger
```

Set up Gazebo model path
```Linux 
export GAZEBO_MODEL_PATH=`ros2 pkg \
prefix turtlebot3_gazebo`/share/turtlebot3_gazebo/models/
```

Launch Gazebo with a simulation world
```Linux 
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

## Run teleoperation node

Open a new terminal and source ROS environment.
```Linux
source install/setup.bash
```
Set up turtlebot model
```Linux
export TURTLEBOT3_MODEL=burger
```
Run teleoperation node
```Linux
ros2 run turtlebot3_teleop teleop_keyboard
```

## Run SLAM nodes

Open a new terminal and source ROS environment.
```Linux
source install/setup.bash
```

Run the SLAM nodes.
```Linux
ros2 launch turtlebot3_cartographer \
cartographer.launch.py \
use_sim_time:=True
```

## Create a map
Make sure that the Fixed Frame (in Global Options) in RViz is set to “map”.

Use the teleoperation keys to move the robot here and there with which we will create a map.

Hints : 
* Try to drive as slow as possible
* Avoid to drive linear and rotate at the same time
* Do not drive too close to the obstacles

## Save the Map
Open a new terminal, source the ROS2 installation and enter your workspace 'robotics'.

Run the map saver node.
```Linux
ros2 run nav2_map_server map_saver_cli
```

You also can define a name of the map by
```Linux
ros2 run nav2_map_server map_saver_cli -f my_map
```

The node will create a map.pgm and a map.yaml files in the current directory, which is your 'robotics' directory in this case.
