*******************
Localization Theory
*******************

We are going to look at the very high level theory of this algorithm and walk through sections of the code during it. The goal of this documentation is to act as a tutorial to the lidar localization codebase.
It is assumed that basic ROS principles are known such as transforms, subscribers, publishers, etc.


The code starts with the __init__ method of the LidarLocalizer class. In this method we:

1. Get all yaml parameters and set them as class variables.

2. Create a subscription to the /scan topic output by the urg node.

3. Create necessary class variables to hold state information (last_board_stop_right/left, buffer, tf_listener, moving_average)

4. Create a broadcaster for our final transform to be published.


After this init method, anytime that a LaserScan /scan topic is published by the urg node, it will get run in the listener_callback function of our class. We will not be going into a deep dive into the rest of the code but rather going through a high level idea of what the code does.


When we get the /scan topic, we go through three main stages:

1. Get possible boards from all the points (self.find_segments). We perform this with a 4 pointer approach (O(n)) where we are looking for continuous regions of points that satisfy our distance condition for the line portion and circle portion of the board. 

2. Select which board is our board (self.test_segments). We perform this with by running 6 tests on each of the segments... length of line, secant length of circle, radius of circle, error of line fit, error of circle fit, secant length of circle and line intersection. If all these checks are passed, we then try to minimize the total error which is found by multiplying each individually.

3. Calculate the transform from our board (self.calc_transformation). We perform this by finding the x and y translation as described by the center of the circle, and we find the theta rotation through the normal line of the line because both are resistant to missing points. We then do a lot of transform math to find what we specifically want to find ad publish it.
