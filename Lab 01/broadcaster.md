Navigate to src/broadcaster_listener/broadcaster_listener 

```Linux
cd src/broadcaster_listener/broadcaster_listener
```

Now let's create the source files. For that, we need to create a python file for the broadcaster.

```Linux
code turtle_tf2_broadcaster.py
```

Now copy the content from [broadcaster.txt](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/broadcaster.txt) and paste in turtle_tf2_broadcaster.py file

Open src/broadcaster_listener folder and open setup.py file. In the file, add the following line between the ```'console_scripts': ``` brackets:

```Linux
'turtle_tf2_broadcaster = learning_tf2_py.turtle_tf2_broadcaster:main',
```

Now create a launch file for this demo. Create a new folder in src/broadcaster-listener called "launch" and inside launch create a new python file called "turtle_tf2_demo.launch.py". 
Open the launch file and add the following lines into the file and save it. 

```python
from launch import LaunchDescription
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
    ])
```

Then navigate to src/broadcaster_listener and open ```package.xml``` with your text editor. Add the following dependencies corresponding to your launch file’s import statements and save it:

```xml
<exec_depend>launch</exec_depend>
<exec_depend>launch_ros</exec_depend>
```

Then open ```setup.py``` and add the below line inside ```data_files```.

```python
data_files=[
    ...
    (os.path.join('share', package_name, 'launch'), glob(os.path.join('launch', '*launch.[pxy][yma]*'))),
],
```
Also add the appropriate imports at the top of the file:

```python
import os
from glob import glob
```
save the file.

Now navigate to the root of your workspace in the Ubuntu 22.04 terminal.

```Linux
cd
cd robotics
```

Run the following command to check for missing dependencies.

```Linux
rosdep install -i --from-path src --rosdistro humble -y
```

Still in the root of your workspace, build your package:

```Linux
colcon build --packages-select broadcaster_listener
```
