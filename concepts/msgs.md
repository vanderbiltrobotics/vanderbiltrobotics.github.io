# Messages
A message is simply a chunk of data published at one point in time from one node. Message types are used to define the type and format of data being published so that subscribers to a topic know the type and format the of data they can expect to receive.  

Message types are defined in `.msg` files.
These message files are used to generate the source code for corresponding data types in multiple languages but you don't need to really worry about that to use messages. The most important part of messages is that there is a common library provided by ROS that contains most of the types you will ever need. The only time we have used custom messages is for the motor control and status messages in `ros_phoenix` and they are stored in a `msgs` folder within the package.

Messages are often composed of other message types. For example, a Point message is composed of 3 float64 message types (one each for x,y, & z). All common message types can be found [here](https://github.com/ros2/common_interfaces) 

## Commonly used Message Types
- **Header**- contains a *coordinate frame id* and *timestamp* and is often included in other message types to provide additional metadata
- **Pose**- consists of a Point representing the *position* (x,y,z) and Quaternion representing the *orientation*
  - A raw pose will not have a Header specifying the coordinate frame so it is used in instances where the coordinate frame is implied   
- **Transform**- consists of a Vector3 representing a *translation* and a Quaternion representing the *rotation*. This is used to represent a transformation between two coordinate frames 
  - The difference between a Point and Vector3 is that Vector3 is thought to be anchored at the origin while a point is just in free space (Terminology difference, functionally the same)  
- **Twist**- expresses *linear and angular velocity* (both Vector3s)
  - **TwistWithCovariance**- also expresses the uncertainty in the velocities using a 6 x 6 covariance matrix
    - Often used for state estimation with algorithms such as the extended kalman filter since these algorithms rely on uncertainty to make their estimates
- For sending images from cameras and data from other sensors like lidar, the **sensor_msgs** library is used   
- For sending maps and other navigation related data, the **nav_msgs** library is used
- For controlling the arm, the **trajectory_msgs** library is used

For many of these messages such as Pose and Transform, there is a Stamped variant which contains a header with important metadata like the coordinate frame the message is associated with and timestamp of when the message was published

When writing nodes, we want to use stamped messages as often as possible because they provide useful debugging information such as timestamps and coordinate frames. These headers often come in handy after a node is developed and a subscribing node is running into issues with the data being published. They can help diagnose transform tree errors and timing delays causing backlog issues or dropped messages. 