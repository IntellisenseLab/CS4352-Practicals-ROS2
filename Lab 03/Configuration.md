To be able to communicate our simulation with ROS 2 you need to use a package called ros_gz_bridge. This package provides a network bridge which enables the exchange of messages between ROS 2 and Gazebo Transport. You can install this package by typing:
```Linux
sudo apt-get install ros-humble-ros-ign-bridge
```

At this point you are ready to launch a bridge from ROS to Gazebo. In particular you are going to create a bridge for the topic /model/vehicle_blue/cmd_vel:
```Linux
source /opt/ros/humble/setup.bash
ros2 run ros_gz_bridge parameter_bridge /model/vehicle_blue/cmd_vel@geometry_msgs/msg/Twist]ignition.msgs.Twist
```

Once the bridge is running the robot is able to follow your motor commands. There are two options:
Send a command to the topic using ros2 topic pub
```Linux
ros2 topic pub /model/vehicle_blue/cmd_vel geometry_msgs/Twist "linear: { x: 0.1 }"
```

teleop_twist_keyboard package. This node takes keypresses from the keyboard and publishes them as Twist messages. You can install it typing:
```Linux
sudo apt-get install ros-humble-teleop-twist-keyboard
```

The default topic where teleop_twist_keyboard is publishing Twist messages is /cmd_vel but you can remap this topic to make use of the topic used in the bridge:
```Linux
source /opt/ros/humble/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/model/vehicle_blue/cmd_vel
```

