************************************
Installing ROS2 on Linux (RyanRules)
************************************

ROS2 is well supported on linux so the installation documentation they provide works out of the box.

You can install ROS2 using pre-built binaries following `these directions <https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Binary.html>`_ or you can use the debian packages by following `these instructions <https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html>`_
. Either way works, but using the debians is probably simpler.

.. note::
    
    If using the debians, you want to install :code:`ros-foxy-desktop` since you want GUI tools.

    Also do not worry about the bridge to ROS1 since we currently do not use it

.. note::

    If packages are failing to build, remember to do the rosdep commands which will install the packages' dependencies:
    :code:`rosdep install -i --from-path src --rosdistro foxy -y`

Verifying ROS2 Works
====================
In order to easily verify everything is installed and working correctly run the following commands and make sure there are no errors:

In one terminal run :code:`ros2 run demo_nodes_cpp talker` and in another terminal run :code:`ros2 run demo_nodes_cpp listener`.
If there are no errors while these run, that's great and means that C++ nodes work for ROS2 on your machine!

Next, in one terminal run :code:`ros2 run demo_nodes_py talker` and in another terminal run :code:`ros2 run demo_nodes_py listener`.
If there are no errors while these run, that's great and means that python nodes work for ROS2 on your machine!