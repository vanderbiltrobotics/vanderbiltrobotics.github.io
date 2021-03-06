# Representing Rotation
There are multiple ways to represent rotation so here is an overview of the ways, which are defined in [ROS REP 103](https://www.ros.org/reps/rep-0103.html). The following are described in descending order of preferred use.

## Quaternions
The preferred way of representing rotation. 

Consists of a 4 element vector. Even though there are only 3 axis around which to rotate, a certain situation called [gimbal lock](https://en.wikipedia.org/wiki/Gimbal_lock) can occur when describing rotation around the 3 axis (not important to know what gimbal lock is for our purposes). Quaternions are used to eliminate the problem of gimbal lock in computations.

## Rotation Matrix
Often used to represent the rotation of a vector since vector-matrix multiplication is easy and fast to do. Rotation of a vector in 2D is given by a 2 x 2 rotation matrix while rotation of a vector in 3D is given by a 3 x 3 rotation matrix. [Read More](https://mathworld.wolfram.com/RotationMatrix.html)

We most see rotation matrices when using OpenCV for image processing and computer vision tasks.

## Roll, Pitch, & Yaw
- Roll describes rotation about the x axis
- Pitch describes rotation about the y axis
- Yaw describes rotation about the z axis
Often used for angular velocities.

## Euler Angles
Similar to roll, pitch, and yaw expect instead of being in the x, y, z representation, they are in the z, y, x representation of yaw, pitch, and roll.

Generally discouraged from using Euler Angles in ROS robotics applications.