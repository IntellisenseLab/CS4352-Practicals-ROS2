# CS4352-Practicals-ROS2

This repository contains practicals designed for the CS3340 and CS4352 - Robotics and Automation module offered by Department of Computer Science and Engineering of University of Moratuwa. This branch contains lab activities related to Batches starting from 2019. This series of practicals are designed to support the theory components taught in the CS4352 and CS3340 lectures and will have complementing activities each week. This work assumes that the students have a basic understanding of Robot Operating System (ROS) including its internal structure, Broadcaster-Listener architecture and Client-Server architecture which can be covered by following the ROS Introduction webinar series.

This practical series uses the latest version of Robot Operating System (ROS2) running in Ubuntu 22.04

Best practice is to create a new directory for every new workspace. Let's create a new workspace for all our practicals related to the module. [Follow these instructions](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/CreateWorkspace.md) and create the "robotics" workspace.

## Lab 1

This lab focuses on learning about TF broadcasters & TF listeners. The practical focuses on creating a TF broadcaster that recives input from keybaord and bradocasting them as a tf transform and a listener that listens to the broadcasted transform and controls the velocity of the turrtlesim accodingly. The static frame transform braodcasts a fixed transformation which a second tutrle follows. The dynamic frame transformation broadcasts a dynamic frame that a second turtle follow.

1. Package Creation - [here](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/createpackage.md)
1. Broadcaster creation - [here](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/broadcaster.md)
1. Listener creation - [here](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/listener.md)
1. Additional static frame - [here](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/static_frame.md)
1. Additional dynamic frame - [here](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/dynamic_frame.md)
1. Compiling and Running - [here](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/running.md)
2. Exercise - [here](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/Lab%2001/Exercise)

## Lab 2

This lab focuses on learning about the relationship between 3 Angle representation, Quaternions and ROS2. The server implements a converter that converts the 3 angle representation to quarternions. The client can send the 3 angle representation and receive the converted quaternion value back. This lab exercise will also give an understating of ROS Server client architecture.

1. Package Creation - here
1. Srv creation - here
1. Server and Client creation - here
1. Exercise - here
