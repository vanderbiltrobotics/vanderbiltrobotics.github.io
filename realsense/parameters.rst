************
Parameters
************

The realsense node has many parameters that we will be editing throughout the year. Currently, there are 3 main parameters to be concerned about.

1. align_depth=true
Setting align_depth to true will allow for the depth camera stream to be available for other camera streams such as color or potentially infared.

2. enable_depth=true 
Enable depth will publish a depth image to the /camera/depth/image_rect_raw topic 

3. enable_gyro & enable_accel=true
Enable gyro and and enable accel will publish an IMU topic that could potentially be used for a Kalman filter
