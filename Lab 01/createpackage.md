First source your ROS2 installation by running the following command in the Ubuntu 22.04 terminal.

```Linux
source /opt/ros/humble/setup.bash
```
Now navigate to the "src" directory in the "robotics" workspace.

```Linux
cd ~/robotics/src
```

Now create a package called "broadcaster_listener" by running the following command.

```Linux
ros2 pkg create --build-type ament_python --license Apache-2.0 -- broadcaster_listener
```

The package has been created. Now continue the next steps to develop the Broadcaster node.
