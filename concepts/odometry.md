# Odometry
Odometry is the use of motion sensors to *estimate* the robot's change in position relative to its initial position.
 
The ROS odometry message consists of a pose with covariance (position & orientation with uncertainty) and a twist with covariance (linear & angular velocities with uncertainty).

**Further Reading:**
- [(Paper) Review of Odometry Techniques](https://springerplus.springeropen.com/articles/10.1186/s40064-016-3573-7)
- [(Slides) Odometry & Reference Frames](https://web2.qatar.cmu.edu/~gdicaro/16311-Fall17/slides/16311-LabNotes-Odometry-ROSFrames.pdf)

## Wheel Odometry
If a robot is traveling in a straight line and  the diameter of its wheels is known, then by counting the number of wheel revolutions we can calculate how far it has traveled: distance = revolutions * circumference of wheel. While this is an overly simplified example, this is the basic idea behind wheel odometry which uses encoders to count the number of wheel or motor rotations over a certain timestep.

Odometry is a cumulative measurement so errors will accumulate as time increases. Read this [article](https://groups.csail.mit.edu/drl/courses/cs54-2001s/odometry.html) to get a better intuition for how wheel odometry errors occur.

In our robot which must move and turn on sand, the main source of wheel odometry error is when wheels get stuck spinning in the sand, drastically increasing the drift in the wheel odometry estimate from the true value. Due to this reason, we are unlikely to use wheel odometry for our robot, though it is good to be aware of since it is often used in indoor environments where slippage is drastically less.

## Visual Odometry
Visual odometry estimates the motion of the robot using sequential images from a camera.

Here is what occurs at a high level to estimate the motion of robot between two camera frames:
1. Features are detected in the current frame
2. Features in the current frame are matched with the same features from the previous frame
3. Motion estimate is generated based on how far certain features moved between the previous and current frame
This use of image processing in robotics is computationally expensive, but can yield better odometry estimates than wheel odometry (immune to wheel slippage) and IMU odometry in many cases.

One of the main challenges of using visual odometry for our robot on a simualted lunar environment is the lack of unique features on the lunar surface that the camera is pointed at. Another challenge is with lighting as shadows from objects and even the robot itself can introduce drift into the odometry estimates. 

While these challenges make it difficult to accurately estimate odometry, we can be inspired by the success NASA has had in using visual odometry for the Mars rovers.

One thing to look into in the future is the difference odometry estimates between monocular and stereo cameras since monocular cameras lack the sense of depth that that stereo cameras can achieve by having two cameras at different angles.

**Further Reading:** [(Slides) Visual Odometry](http://www.cs.toronto.edu/~urtasun/courses/CSC2541/03_odometry.pdf)

## IMU Odometry
Inertial measurement units (comprised of accelerometers & a gyroscope) provide linear and angular acceleration as well as orientation. The accelerations can be integrated to get a linear and angular velocity estimate which in turn can be intergrated to get a position and orientation estimate. 

It is important to keep in mind that each integration adds drift from the true value, so the drift associated with the position and velocity estimates from the IMU is quite high. Cheaper IMUs are less precise meaning the drift in measured acceleration from true acceleration is often too high to make the resulting position and velocity estimates of any use.

We have had issues with the IMU data from the Realsense D435i (i stands for IMU) so goal for this year is to use a seperate IMU module to hopefully acheive better results. 

Given better IMU odometry, we can fuse it with the visual odometry estimate in a sensor fusion algorithm to produce a better odometry estimate than either could produce on their own. While in theory this sounds great, in practice this has proven quite challenging fusing together odometry estimates to get a better estimate. You can read more on sensor fusion in a following article.