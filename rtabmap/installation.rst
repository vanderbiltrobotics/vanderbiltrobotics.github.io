************
Installation
************

Unfortunately, Rtabmap has to be built from source for ROS2. This is actually a lot easier than it sounds with the following commands. Make sure that this is installed in a separate ROS2 workspace, and then source it in the bashrc.

RTAB-Map & Rtabmap_ros library:

.. code-block:: bash

    mkdir ~/ros2_ws
    cd ~/ros2_ws
    git clone https://github.com/introlab/rtabmap.git src/rtabmap
    git clone --branch ros2 https://github.com/introlab/rtabmap_ros.git src/rtabmap_ros
    export MAKEFLAGS="-j6" # Can be ignored if you have a lot of RAM
    colcon build
    echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc 

The colcon build may actually fail the first time, but for some reason if you build it 1-3 more times, it will work. This is a bug on colcon. Also, the build may take like 20 minutes.
