You are going to use one of the worlds defined in the Gazebo examples called visualize_lidar.sdf. To run this example you should execute the following command in a terminal:
```Linux
ign gazebo -v 4 -r visualize_lidar.sdf
```

When the simulation is running you can check the topics provided by Gazebo with the ign command line tool:
```Linux
ign topic -l
```

Since you have not launched an ROS 2 nodes yet, the output from ros2 topic list should be free of any robot topics:
```Linux
ros2 topic list
```

