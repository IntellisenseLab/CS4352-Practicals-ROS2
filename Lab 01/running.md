#Running the Broadcaster

Move to the root of the ROS workspace and launch the program.

```Linux
. install/setup.bash
ros2 launch broadcaster_listener turtle_tf2_demo.launch.py
```

On a separate terminal window, type the following command:

```Linux
ros2 run turtlesim turtle_teleop_key
```

Now, use the tf2_echo tool to check if the turtle pose is actually getting broadcast to tf2:

```Linux
ros2 run tf2_ros tf2_echo world turtle1
```

#Running the Listener

Open a new terminal, navigate to the root of your workspace, and source the setup files:

```Linux
. install/setup.bash
ros2 launch broadcaster_listener turtle_tf2_demo.launch.py
```

In the second terminal window type the following command:

```Linux
ros2 run turtlesim turtle_teleop_key
```

Now simply drive around the first turtle using the arrow keys (make sure your terminal window is active, not your simulator window), and you’ll see the second turtle following the first one!

#Adding a static carrot!

Open a new terminal, navigate to the root of your workspace, and source the setup files:

```Linux
. install/setup.bash
ros2 launch broadcaster_listener turtle_tf2_fixed_frame_demo.launch.py
```
Now you’ll see the second turtle following the carrot instead of the first turtle!

#Adding a dynamic carrot!

Open a new terminal, navigate to the root of your workspace, and source the setup files:

```Linux
. install/setup.bash
ros2 launch broadcaster_listener turtle_tf2_dynamic_frame_demo.launch.py
```
You should see that the second turtle is following the carrot’s position that is constantly changing.


