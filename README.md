# CS4352-Practicals-ROS2

This repository contains practicals designed for the CS3340 and CS4352 - Robotics and Automation module offered by Department of Computer Science and Engineering of University of Moratuwa. This branch contains lab activities related to Batches starting from 2019. This series of practicals are designed to support the theroy components taught in the CS4352 and CS3340 lectures and will have complementing activities each week. This work assumes that the students have a basic understanding of Robot Operating System (ROS) including its internal structure, Publisher-Subscriber architecture and Client-Server architecture which can be covered by following the ROS Introduction webinar series.

This practical series uses the latest version of Robot Operating System (ROS2) running in Ubuntu 22.04

Best practice is to create a new directory for every new workspace. Let's create a new workspace for all our practicals related to the module. [Follow this instructions](https://github.com/IntellisenseLab/CS4352-Practicals-ROS2/blob/main/CreateWorkspace.md) and create the "robotics" workspace.

## Lab 1

This lab focuses on learning about TF broadcasters & TF listeners. The practical focuses on creating a TF broadcaster that recives input from keybaord and bradocasting them as a tf transform and a listener that listens to the broadcasted transform and controls the velocity of the turrtlesim accodingly. The static frame transform braodcasts a fixed transformatin which a second tutrle follows. The dynamic frame transformation broadcasts a dnamic frame that a second turtle follow.

This practical is based on "Writing a simple publisher and subscriber" available in [https://docs.ros.org/en/humble](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Tf2-Main.html#)).

1. Package Creation - [here]
1. Publisher creation - [here]
1. Subscriber creation - [here]
1. Additional static frame - [here]
1. Additional dynamic frame - [here]
1. Compiling and Running - [here]
