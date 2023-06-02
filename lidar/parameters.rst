************
Parameters
************

In order to configure the lidar as we want, there is a yaml parameter file :code:`lidar_localization/config/urg_node.yaml` that is loaded by the urg_node package.

All the available parameters are listed below in the format required for ROS2 parameter files (note the urg_node heading and ros__parameters subheading):

.. code-block:: yaml

    urg_node:
        ros__parameters:
            ip_address: "192.168.0.10"
            ip_port: 10940
            #serial_port: "" # commented because you can't set a param with an empty string
            serial_baud: 115200
            laser_frame_id: laser
            angle_max: 3.14
            angle_min: -3.14
            publish_intensity: false
            publish_multiecho: false
            calibrate_time: false
            default_user_latency: 0
            diagnostics_tolerance: 0.05
            diagnostics_window_time: 5.0
            error_limit: 4
            get_detailed_status: false
            cluster: 0
            skip: 1

You can reconfigure parameters while the node is launched. For now, you can only reconfigure the following parameters:

.. code-block:: bash

    laser_frame_id
    error_limit
    default_user_latency
    angle_max # upper angle bound of lidar
    angle_min # lower angle bound of lidar
    cluster # cluster specified amount of data points together
    skip # for every data point, skip the specified amount of data points

For example, to reconfigure the cluster parameter:

.. code-block:: bash
    
    ros2 param set /urg_node cluster 1

Localization Parameters
There are also parameters stored in :code:`lidar_localization/config/lidar_localization_circle.yaml` for running the lidar localization node:

.. code-block:: yaml

    debug (boolean): Set to True if you want a lot of print statements to debug the program (see what the program is thinking). To make it run faster set it to False.
    board_radius (double): The true radius to the circle portion of the board.
    circle_length (double): The true secant length of the circle portion of the board.
    line_length (double): The true length of the line portion of the board.
    percent_error_length (double): The maximum percent error that we allow in the fit for the lengths of the circle, line, and interaction of the two. The smaller the value, the more selective (Note: 10% is 0.1).
    percent_error_radius (double): The maximum percent error that we allow in the fit for the radius of the circle portion of the board. The smaller the value, the more selective (Note: 10% is 0.1).
    circle_error_cutoff (double): The maximum error we allow in the circle fit for our board (in meters).
    line_error_cutoff (double): The maximum error we allow in the line fit for our board (in meters).
    no_averaged_points (integer): The number of points we perform the moving average on to smooth out the localization (but it lags behind the true position with higher numbers)