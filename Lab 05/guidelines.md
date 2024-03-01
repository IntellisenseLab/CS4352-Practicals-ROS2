# Lab 05

In this lab, we will use 'MoveIt' to interact with our robot.

Move to robotics/src

```Linux
cd robotics/src
```

Clone the MoveIt demo repository.

```Linux
git clone --branch humble https://github.com/ros-planning/moveit2_tutorials
```

Next we will download the source code for the rest of MoveIt:

```Linux
vcs import < moveit2_tutorials/moveit2_tutorials.repos
```

Run rosdep to install any dependencies that miss out.

```Linux
sudo apt update && rosdep install -r --from-paths . --ignore-src --rosdistro humble -y
```

Source the workspace

```Linux
source ~/robotics/install/setup.bash
```

Install and export ROS2 Middleware Cyclon DDS 

```Linux
sudo apt install ros-humble-rmw-cyclonedds-cpp

export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
```

Now follow the instructions [on this page](https://moveit.picknik.ai/humble/doc/tutorials/quickstart_in_rviz/quickstart_in_rviz_tutorial.html).

## Activity

1. After completing the Step 3, you should record a video of the screen that shows what happens when you use these markers to drag the arm around and change its orientation.
2. After completing [this](https://moveit.picknik.ai/humble/doc/tutorials/quickstart_in_rviz/quickstart_in_rviz_tutorial.html#moving-joints-or-in-null-space) in Step 3 you should record a video of the screen that shows what happens when you move the “null space exploration” slider.
3. After completing Step 4, you should be able to see a visualization of the arm moving and a trail, record the movement.

   You should submit 3 screen recordings and a Lab report consists of the task description, RViz screenshots and your understandings from the lab.

