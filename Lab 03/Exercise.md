Complete the Visualization part and submit a screen recording of the successfully running system.

Submit the output from the teleop_twist_keyboard after running the below command as a pdf file.

```Linux
source /opt/ros/humble/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/model/vehicle_blue/cmd_vel
```
