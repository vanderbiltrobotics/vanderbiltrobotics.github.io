**************************
Installing ROS2 on Windows
**************************

Current Package Support:
 - All of base ROS2
 - MoveIt2 (full support)
 - Navigation2 (Gazebo, path planning)

Not Yet Supported:
 - Realsense
 - RTAB-Map
 - warehouse-ros-sqlite

If you need any more packages ported for Windows, talk to Akash!

Environment Setup
=================

Let's start by installing `Chocolatey <https://chocolatey.org/>`_, which is a package manager for Windows.
In order to install it, you will need to run the commands it says in an administrator powershell.

Then, run the following commands to install all the dependencies.
If you already have Python installed, then don't run that line.
If you already have cmake installed, please uninstall it and let chocolatey install it.

.. code-block:: powershell

    choco install -y python --version 3.8.3
    choco install -y cmake.install --installargs '"ADD_CMAKE_TO_PATH=System"'
    choco install -y vcredist2013 vcredist140 ninja

Then, you need to upgrade pip and then install all the pip packages. Make sure to open a new powershell window. This one
does not have to be an administrator one.

.. code-block:: powershell

    python -m pip install --upgrade pip
    pip install -U vcstool colcon-common-extensions catkin_pkg cryptography EmPy ifcfg lark-parser lxml `
    netifaces numpy opencv-python pyparsing pyyaml setuptools rosdistro pydot PyQt5

Then, you need install MSVC which is Microsoft's C++ compiler. Download
`Visual Studio Community 2022 <https://visualstudio.microsoft.com>`_.
Make sure to have :code:`Desktop development with C+` checked and no C++ CMake tools are checked.

Now, it's time to actually install ROS2. Go ahead and run the following commands:

.. code-block:: powershell

    mkdir -p C:/opt/ros/foxy
    cd C:/opt/ros/foxy
    explorer .

This should open up a File Explorer window in :code:`C:/opt/ros/foxy`
You'll want to download
`our prebuilt ROS2 <https://github.com/Ace314159/ros2-foxy-windows-packages/releases/download/ros2-foxy-combined/ros2-foxy-combined.7z>`_.
Then, move the ZIP file to :code:`C:/opt/ros/foxy`, and extract it. You will need `7-zip <https://www.7-zip.org/>`_ to extract it.
In order to extract in the correct folder, right click the 7z file, Go to :code:`7-Zip --> Extract files...`.
This will open up a window. In the :code:`Extract to:` field put :code:`C:/opt/ros/foxy`. That's it! You have ROS installed.

To properly source ROS2, you'll want to add the following line to your Powershell profile. You can access the file by running
:code:`notepad $PROFILE` in a Powershell terminal. This will open the file in Notepad. Add the following line to the end and save:

.. code-block:: powershell

    C:/opt/ros/foxy/x64/local_setup.ps1

That's all!

Other Useful Setup
==================

Using ROS on Windows is extremely annoying, so I have some recommendations to make it much better. I highly recommend you
do these as well.

First, let's install a better terminal called Windows Terminal. Open the Microsoft Store and search for Windows Terminal.
Then, just click Get and Install. Now, you can open up Windows Terminal by just typing :code:`wt` in the start menu.
Windows Terminal allows you to have multiple tabs, better shortcuts, and just looks much cooler.

Next, let's add some utility functions to our powershell profile to make using ROS much simpler.

Before building any ROS 2 workspace, you need to launch a powershell developer shell. Instead of having to launch a separate
terminal, you can just use this utility function called :code:`setupDev` to make your current terminal have the same properties.

.. code-block:: powershell

    function setupDev {
      $dir = (Get-Item .).FullName
      $vsPath = &(Join-Path ${env:ProgramFiles(x86)} "\Microsoft Visual Studio\Installer\vswhere.exe") -property installationpath
      Import-Module (Join-Path $vsPath "Common7\Tools\Microsoft.VisualStudio.DevShell.dll")
      Enter-VsDevShell -VsInstallPath $vsPath -SkipAutomaticLocation -DevCmdArguments -arch=x64
      cd $dir
    }

Another issue is when there are CMake or compiler errors with MSVC, nothing is displayed. This is because error output
is printed out to stdout instead of stderr and colcon doesn't print it to the console. In order to show it, we need to enable the
:code:`console_cohesion` event handler.

Also, when building ROS 2 workspaces, using the default build system MSBuild is very slow. Ninja is a much faster build system.
In addition, when using MSBuild, :code:`colcon build` will always rebuild even if no code was changed. However, in order
to use Ninja, you need to add :code:`--cmake-args -G Ninja` to every single build command which can get annoying.

.. code-block:: powershell

    function colconBuild {
      colcon build --event-handlers console_cohesion+ --cmake-args -G Ninja -DCMAKE_BUILD_TYPE=RelWithDebInfo $args
    }

Now, all that functionality can be used using :code:`colconBuild`. You can
even add extra flags if you want: :code:`colconBuild --packages-skip-build-finished`

Verifying ROS2 Works
====================
In order to easily verify everything is installed and working correctly run the following commands and make sure there are no errors:

In one terminal run :code:`ros2 run demo_nodes_cpp talker` and in another terminal run :code:`ros2 run demo_nodes_cpp listener`.
If there are no errors while these run, that's great and means that C++ nodes work for ROS2 on your machine!

Next, in one terminal run :code:`ros2 run demo_nodes_py talker` and in another terminal run :code:`ros2 run demo_nodes_py listener`.
If there are no errors while these run, that's great and means that python nodes work for ROS2 on your machine!