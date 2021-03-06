# ROS Overview

## What is ROS?
ROS stands for Robot Operating System. While the name suggests it is an operating system, that is not really the case as it operates more like a framework for developing robotics applications and must still run on an underlying OS such as Ubuntu.

Using ROS allows us to run a network of nodes that communicate to each other by publishing messages containing relevant data to topics. Other nodes can then subscribe to those topics to retrieve those messages.

![GIF of Nodes + Topics](https://docs.ros.org/en/foxy/_images/Topic-MultiplePublisherandMultipleSubscriber.gif)

 For instance, in order to detect objects in a camera frame we would have the following node structure:

The camera driver node would take the incoming images from the camera and publish them as an img message to the `/camera_image` topic. Multiple nodes can now subscribe to this camera topic to perform different functions such as detecting objects in the robot's path. ROS handles directing messages to where they need to go and allows us to focus on writing nodes to do what we want.

The pub-sub architechture in ROS allows nodes to be run on seperate computers and still communicate with each other. This helps a lot with multiple robots communicating or with offboarding some heavy computation to a seperate computer from the robot. 

While looking at the [ROS2 tutorials](https://docs.ros.org/en/foxy/Tutorials.html) can seem intimidating with so many topics such as actions, services, and plugins, you don't need to worry because most all of our repository relies on only the simple publishing and subscribing abilities of nodes. This means you can focus your efforts on learning the core of ROS-- writing and launching nodes to publish and subscribe to data --and not worry about the more advanced topics that can be explored later on.

## Packages in ROS
Packages are how we organize nodes in ROS. In order to do a complex task like mapping the environment, many nodes might be involved and then all of these nodes would be included in a single package and called `mapping` which also contains launch files for running the nodes.

Just like how other developers will provide open source npm packages for people to use with their node.js projects, robotics developers often provide open source ROS packages that can be easily downloaded and run by other roboticists. Some of the main external packages we rely on for our robot are:
- RTABMAP: for mapping the environment and getting velocity estimates from the camera inputs 
- Nav2: for taking the map from RTABMAP and planning a path around any obstacles to the goal position & orientation on the map
- MoveIt2: for planning the arm's trajectory to a goal position & orientation

Using these external packages is quite easy as all we have to do is install the package and then launch any of the nodes provided using any of the supplied launch files or by writing our own launch files to launch nodes from the package.
In fact, many of the packages we write in our repository are to just contain the configuration and launch files necessary to use these external packages for our needs (ex: `navigation` )