In our turtle example, we’ll add a new frame carrot1, which will be the child of the turtle1. This frame will serve as the goal for the second turtle.

Inside src/broadcaster_listener/broadcaster_listener create a python file called fixed_frame_tf2_broadcaster.py

Now copy the content [from static_frame.txt](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/static_frame.txt) and paste in the fixed_frame_tf2_broadcaster.py

Now open src/broadcaster_listener and open setup.py file.
Add the following line between the 'console_scripts': brackets:

```Linux
'fixed_frame_tf2_broadcaster = broadcaster_listener.fixed_frame_tf2_broadcaster:main',
```
Now let’s create a launch file for this example. With your text editor, create a new file called launch/turtle_tf2_fixed_frame_demo.launch.py, and add the following lines:

```python
import os

from ament_index_python.packages import get_package_share_directory

from launch import LaunchDescription
from launch.actions import IncludeLaunchDescription
from launch.launch_description_sources import PythonLaunchDescriptionSource

from launch_ros.actions import Node


def generate_launch_description():
    demo_nodes = IncludeLaunchDescription(
        PythonLaunchDescriptionSource([os.path.join(
            get_package_share_directory('broadcaster_listener'), 'launch'),
            '/turtle_tf2_demo.launch.py']),
        launch_arguments={'target_frame': 'carrot1'}.items(),
        )

    return LaunchDescription([
        demo_nodes,
        Node(
            package='broadcaster_listener',
            executable='fixed_frame_tf2_broadcaster',
            name='fixed_broadcaster',
        ),
    ])
```
Run ```rosdep``` in the root of your workspace to check for missing dependencies.

```Linux
rosdep install -i --from-path src --rosdistro humble -y
```

Still in the root of your workspace, build your package:

```Linux
colcon build --packages-select broadcaster_listener
```

