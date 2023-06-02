****************
Launch Urg Node
****************
Urg Node

The `urg_node_driver` node within the `urg_node` package must be run to translate the ethernet lidar signal to a LaserScan (/scan).


.. tabs::

    .. group-tab:: run directly
        
        .. code-block:: bash

            ros2 run urg_node urg_node_driver --ros-args --params-file ~/lunabot-ros2/src/lidar_localization/config/urg_node.yaml
            
    .. group-tab:: launch file

        .. code-block:: bash

            ros2 launch lidar_localization urg_node.launch.py

If you want to visualize the LaserScan in RVIZ, you need to either set the RVIZ frame to laser or create a static transform from map to laser:

.. code-block:: bash

    ros2 run tf2_ros static_transform_publisher 0 0 0 0 0 0 "map" "laser"

Once you have the lidar running, you should be able to visualize the point scan in rviz2 by
simply runnning :code:`rviz2` in a terminal and then selecting to visualize the :code:`/scan` topic 
that the urg_node publishes the lidar data to.