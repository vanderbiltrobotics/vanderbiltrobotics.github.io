**************
Best Practices
**************

This is a guide for best practices to follow when contributing to the repo.
Having consistency across a big codebase makes it much easier to maintain and onboard new members  

Logging
=======
- Make use of the built in logging capabilities and levels in ROS2. 
- DEBUG, INFO, WARN, ERROR, and FATAL are the levels in ascending order. 
- Add debug statements instead of print statements
    - DEBUG level is not printed to console by default (all other levels are printed by default)
    - To see DEBUG statements add arguments to the node you want debugged in the launch file: 

.. code-block:: python

    launch_ros.actions.Node(
        package='demo_nodes_cpp',
        executable='talker',
        output='screen', 
        arguments=['--ros-args', '--log-level', 'debug']
    )


- Loggers use the node's name and namespace so its easier to manage debugging sessions with lots of nodes 
- Use `rqt_console <https://docs.ros.org/en/foxy/Tutorials/Rqt-Console/Using-Rqt-Console.html>`_ for easy filtering and exporting of log messages. 
    - Exporting log messages to text files is good for keeping a record of errors we run into and sharing them with others for help debugging 

Launch Files
============
- Use python to launch nodes/components and add complex launch logic
- Use xml to include other launch files (using python for this is quite messy)
- Store parameters in a :code:`.yaml` file in a :code:`config` folder and load them into your launch file instead of hardcoding parameter values

Naming 
======
- Use descriptive names! or else its very hard to debug weeks or months later
- For python files variables use :code:`snake_case`
- For C++ files variables use :code:`camelCase`
- Classes are always :code:`PascalCase`