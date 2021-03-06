***************************
Project 3: Rosbag & Mapping
***************************

While previous projects were done on your local machine, this project will be done on the team laptop for 2 reasons:
1. RTABMAP for ros2 can be tricky to get installed from source on all platforms so we will just use the one on the team laptop
2. The bag files containing the camera data are multiple GBs so it would be impractical to be transferring them around

Objectives
==========
- Access and playback a rosbag file using terminal commands
- Use the launch files to launch the correct RTABMAP configuration 
- Use rviz2 to display the occupancy grid (map) of the environment

.. note::
    The bag files are stored in the :code:`/bagfiles` directory.

Testing
=======
You can consider the project a success once you have a map displayed in rviz2