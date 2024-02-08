Navigate to src/broadcaster_listener/broadcaster_listener

```Linux
cd src/broadcaster_listener/broadcaster_listener
```

Now let's create the source files. For that, we need to create a python file for the listener.

```Linux
code turtle_tf2_listener.py
```
Now copy the content from [listener.txt](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/listener.txt) and paste in turtle_tf2_listener.py file.

Open src/broadcaster_listener folder and open setup.py file. In the file, add the following line between the ```'console_scripts': ``` brackets:

```Linux
'turtle_tf2_listener = broadcaster_listener.turtle_tf2_listener:main',
```

Open the launch file called turtle_tf2_demo.launch.py with your text editor, add two new nodes to the launch description, add a launch argument, and add the imports. The resulting file should look like:

```python
from launch import LaunchDescription
from launch.actions import DeclareLaunchArgument
from launch.substitutions import LaunchConfiguration

from launch_ros.actions import Node


def generate_launch_description():
    return LaunchDescription([
        Node(
            package='turtlesim',
            executable='turtlesim_node',
            name='sim'
        ),
        Node(
            package='broadcaster_listener',
            executable='turtle_tf2_broadcaster',
            name='broadcaster1',
            parameters=[
                {'turtlename': 'turtle1'}
            ]
        ),
        DeclareLaunchArgument(
            'target_frame', default_value='turtle1',
            description='Target frame name.'
        ),
        Node(
            package='broadcaster_listener',
            executable='turtle_tf2_broadcaster',
            name='broadcaster2',
            parameters=[
                {'turtlename': 'turtle2'}
            ]
        ),
        Node(
            package='broadcaster_listener',
            executable='turtle_tf2_listener',
            name='listener',
            parameters=[
                {'target_frame': LaunchConfiguration('target_frame')}
            ]
        ),
    ])
```
save the file.

Now navigate to the root of your workspace and run ```rosdep``` to check for missing dependencies.

```Linux
rosdep install -i --from-path src --rosdistro humble -y
```

Build your package.

```Linux
colcon build --packages-select broadcaster_listener
```
