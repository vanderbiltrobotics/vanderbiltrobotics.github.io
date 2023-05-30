************
Installation
************

.. tabs::
  .. group-tab:: Linux

    .. code-block:: bash
    
      sudo apt-get install ros-foxy-realsense2-camera
      sudo apt-get install ros-foxy-tf2-ros
      sudo apt-get install ros-foxy-depthimage-to-laserscan
      
    The tf2 and depthimage_to_laserscan packages should be installed automatically with a desktop ROS installation. However, these packages can also be installed separately with the above commands.


To ensure the realsense installation was successful, first make sure Realsense is plugged in. Then, test the package with the below commands. You should be able to echo a non empty message published to /camera/color/image_raw

.. tabs::
  .. group-tab:: Realsense Terminal 1

    .. code-block:: bash

      ros2 launch realsense2_camera realsense.launch.py

  .. group-tab:: Realsense Terminal 2

    .. code-block:: bash

      ros2 topic echo /camera/color/image_raw

To ensure tf2_ros installation was successful, run the following commands. The tf echo (terminal 2) should be displaying the static transform.

.. tabs::
  .. group-tab:: Transform Terminal 1

    .. code-block:: bash
      
      ros2 run tf2_ros static_transform_publisher 1 2 3 0.5 0.1 -1.0 foo bar

  .. group-tab:: Transform Terminal 2

    .. code-block:: bash

      ros2 topic echo ros2 run tf2_ros tf2_echo foo bar

To ensure depthimage_to_laserscan installation was successful, run the following commands. Make sure the realsense is plugged in. The scan topic echo (terminal 3) should be non-empty.

.. tabs::
  .. group-tab:: Depth to Scan Terminal 1

    .. code-block:: bash

      ros2 launch depthimage_to_laserscan depthimage_to_laserscan.launch.py

  .. group-tab:: Depth to Scan Terminal 2

    .. code-block:: bash

      ros2 launch realsense2_camera realsense.launch.py

  .. group-tab:: Depth to Scan Terminal 3

    .. code-block:: bash

      ros2 topic echo /scan
