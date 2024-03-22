# Lab 07

## Installation

Follow the instructions [here](https://docs.ros.org/en/humble/Tutorials/Advanced/Simulators/Webots/Installation-Ubuntu.html) to install Webots in ROS2.
Note : If installing from distributed package does not work for you please try installing it from the source files.

## Create Package 

Create a new package named "sim_robot" in your src folder of your workspace.
Navigate to robotics/src and run:

```Linux
ros2 pkg create --build-type ament_python --license Apache-2.0 --node-name my_robot_driver sim_robot --dependencies rclpy geometry_msgs webots_ros2_driver
```

Run the following to add launch and world folders.
```Linux
cd sim_robot
mkdir launch
mkdir worlds
```
You will need a world file containing a robot to launch your simulation. [Download this file](https://docs.ros.org/en/humble/_downloads/5ad123fc6a8f1ea79553d5039728084a/my_world.wbt) and move it inside sim_robot/worlds/.

## Edit my_robot_driver plugin

Open sim_robot/sim_robot/my_robot_driver.py and replace the contents with the following : 

```python
import rclpy
from geometry_msgs.msg import Twist

HALF_DISTANCE_BETWEEN_WHEELS = 0.045
WHEEL_RADIUS = 0.025

class MyRobotDriver:
    def init(self, webots_node, properties):
        self.__robot = webots_node.robot

        self.__left_motor = self.__robot.getDevice('left wheel motor')
        self.__right_motor = self.__robot.getDevice('right wheel motor')

        self.__left_motor.setPosition(float('inf'))
        self.__left_motor.setVelocity(0)

        self.__right_motor.setPosition(float('inf'))
        self.__right_motor.setVelocity(0)

        self.__target_twist = Twist()

        rclpy.init(args=None)
        self.__node = rclpy.create_node('my_robot_driver')
        self.__node.create_subscription(Twist, 'cmd_vel', self.__cmd_vel_callback, 1)

    def __cmd_vel_callback(self, twist):
        self.__target_twist = twist

    def step(self):
        rclpy.spin_once(self.__node, timeout_sec=0)

        forward_speed = self.__target_twist.linear.x
        angular_speed = self.__target_twist.angular.z

        command_motor_left = (forward_speed - angular_speed * HALF_DISTANCE_BETWEEN_WHEELS) / WHEEL_RADIUS
        command_motor_right = (forward_speed + angular_speed * HALF_DISTANCE_BETWEEN_WHEELS) / WHEEL_RADIUS

        self.__left_motor.setVelocity(command_motor_left)
        self.__right_motor.setVelocity(command_motor_right)
```

## Create my_robot.urdf file

In the sim_robot/resource folder create a text file named my_robot.urdf with this content:

```python
<?xml version="1.0" ?>
<robot name="My robot">
    <webots>
        <plugin type="sim_robot.my_robot_driver.MyRobotDriver" />
    </webots>
</robot>
```

## Create launch file

In the sim_robot/launch folder create a new text file named robot_launch.py with this code:

```python
import os
import launch
from launch import LaunchDescription
from ament_index_python.packages import get_package_share_directory
from webots_ros2_driver.webots_launcher import WebotsLauncher
from webots_ros2_driver.webots_controller import WebotsController


def generate_launch_description():
    package_dir = get_package_share_directory('my_package')
    robot_description_path = os.path.join(package_dir, 'resource', 'my_robot.urdf')

    webots = WebotsLauncher(
        world=os.path.join(package_dir, 'worlds', 'my_world.wbt')
    )

    my_robot_driver = WebotsController(
        robot_name='my_robot',
        parameters=[
            {'robot_description': robot_description_path},
        ]
    )

    return LaunchDescription([
        webots,
        my_robot_driver,
        launch.actions.RegisterEventHandler(
            event_handler=launch.event_handlers.OnProcessExit(
                target_action=webots,
                on_exit=[launch.actions.EmitEvent(event=launch.events.Shutdown())],
            )
        )
    ])
```

## Edit additional files

Now you have to modify the setup.py file to include the extra files you added. Open sim_robot/setup.py and replace its contents with:

```python
from setuptools import setup

package_name = 'my_package'
data_files = []
data_files.append(('share/ament_index/resource_index/packages', ['resource/' + package_name]))
data_files.append(('share/' + package_name + '/launch', ['launch/robot_launch.py']))
data_files.append(('share/' + package_name + '/worlds', ['worlds/my_world.wbt']))
data_files.append(('share/' + package_name + '/resource', ['resource/my_robot.urdf']))
data_files.append(('share/' + package_name, ['package.xml']))

setup(
    name=package_name,
    version='0.0.0',
    packages=[package_name],
    data_files=data_files,
    install_requires=['setuptools'],
    zip_safe=True,
    maintainer='user',
    maintainer_email='user.name@mail.com',
    description='TODO: Package description',
    license='TODO: License declaration',
    tests_require=['pytest'],
    entry_points={
        'console_scripts': [
            'my_robot_driver = my_package.my_robot_driver:main',
        ],
    },
)

```

## Test the code

From a terminal in your ROS 2 workspace run:

```Linux
colcon build
source install/local_setup.bash
ros2 launch my_package robot_launch.py
```

Then, open a second terminal and send a command with:

```Linux
ros2 topic pub /cmd_vel geometry_msgs/Twist  "linear: { x: 0.1 }"
```

Record and submit a screen recording of what happens when you run the above codes. 
Note : Name your recording "simulation_basic_<index_no>.mp4"
