************
Installation
************

Here's how you install MoveIt and its related tools for ROS2 Foxy.
This should handle everything you need for the remainder of this section.
MoveIt2 is a little strange in that you can't install it from apt -- instead,
you install it into its own separate ROS2 workspace, and then source that to bring
MoveIt tools into your ROS2 environment.

.. tabs::
  .. group-tab:: Linux

    .. code-block:: bash

      sudo apt install python3-rosdep2
      rosdep update
      sudo apt update
      sudo apt dist-upgrade
      sudo apt install python3-colcon-common-extensions
      sudo apt install python3-vcstool
      mkdir -p ~/ws_moveit2/src
      cd ~/ws_moveit2/src

      git clone https://github.com/ros-planning/moveit2.git
      wget https://raw.githubusercontent.com/ros-planning/moveit2/main/moveit2.repos
      vcs import < moveit2.repos
      wget https://raw.githubusercontent.com/ros-planning/moveit2_tutorials/main/moveit2_tutorials.repos
      vcs import < moveit2_tutorials.repos

      cd ~/ws_moveit2/src
      rosdep install -r --from-paths . --ignore-src --rosdistro foxy -y
      echo 'source ~/ws_moveit2/install/setup.bash' >> ~/.bashrc

    Finally, relaunch your terminal.

  .. group-tab:: macOS

    .. code-block:: bash

      TODO

To ensure installation was successful, try running:

.. code-block:: bash

  ros2 launch moveit2_tutorials demo.launch.py rviz_tutorial:=true

You should get no errors in the console, and you should be presented
with a blank word in rviz2. If you click "Add" in the bottom left-hand
corner and select "MotionPlanning", the motion planning interface should
pop up, along with the Panda robot.