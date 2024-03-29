The diff drive robot has a lidar. To send the data generated by Gazebo to ROS 2, you need to launch another bridge. In the case the data from the lidar is provided in the Gazebo Transport topic /lidar2, which you are going to remap in the bridge. This topic will be available under the topic /lidar_scan:
```Linux
source /opt/ros/humble/setup.bash
ros2 run ros_gz_bridge parameter_bridge /lidar2@sensor_msgs/msg/LaserScan[ignition.msgs.LaserScan --ros-args -r /lidar2:=/laser_scan
```

To visualize the data from the lidar in ROS 2 you can use Rviz2:
```Linux
source /opt/ros/humble/setup.bash
rviz2
```

Then you need to configure the fixed frame:
![fixed_frame](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/assets/58034992/326c168d-9e78-4210-99c0-208440962af2)

And then click in the button “Add” to include a display to visualize the lidar:
![add_lidar](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/assets/58034992/74f6c76f-8589-48b5-8b05-1f907b824f4b)

Now you should see the data from the lidar in Rviz2:
![rviz2](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/assets/58034992/dbbeac83-8255-4bfe-81ea-91b542244a12)
