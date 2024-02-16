# Time travelling using ROS2 and Python

Go to the broadcaster_listener package from lab 01 and open turtle_tf2_listener.py and replace ```python if self.turtle_spawned:```. Keep the ```python except``` block as it is.

```python
when = self.get_clock().now() - rclpy.time.Duration(seconds=5.0)
                try:
                    t = self.tf_buffer.lookup_transform(
                        to_frame_rel,
                        from_frame_rel,
                        when,
                        timeout=rclpy.duration.Duration(seconds=0.05))
```

Now launch the fixed_frame launch file.

```Linux
ros2 launch broadcaster_listener turtle_tf2_fixed_frame_demo.launch.py
```

Observe the second turtle and explain what happens ? 

Now stop the simulation and again open the turtle_tf2_listener.py and replace the code you have added already.
```python
when = self.get_clock().now() - rclpy.time.Duration(seconds=5.0)
trans = self.tf_buffer.lookup_transform_full(
        target_frame=to_frame_rel,
        target_time=rclpy.time.Time(),
        source_frame=from_frame_rel,
        source_time=when,
        fixed_frame='world',
        timeout=rclpy.duration.Duration(seconds=0.05))
```

Run the simulation.

```Linux
ros2 launch broadcaster_listener turtle_tf2_fixed_frame_demo.launch.py
```

Observe the second turtle and explain what happens ? 
