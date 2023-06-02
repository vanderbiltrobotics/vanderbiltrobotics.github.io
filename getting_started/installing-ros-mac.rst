*************************
Installing ROS2 on macOS
*************************

Current Package Support:
 - All of base ROS2
 - MoveIt2 (full support, & warehouse-ros-sqlite)
 - Navigation2 (Gazebo, path planning, Intel RealSense, erg_node for Hokuyo LiDAR)

Not Yet Supported:
 - RTAB-Map
 - ros_phoenix (internal support)

Currently Broken:
 - Some builds against MoveIt -- library matching issues

You must be on the **latest** version of macOS to use this install system.
If you require builds for earlier versions of macOS, or if you need any more
packages ported for macOS, talk to Nisala!

.. note::
    If you have an M1 Mac, also keep in mind that this installation must be done in a 
    Rosetta Terminal. You can set this up using 
    `this guide <https://osxdaily.com/2020/11/18/how-run-homebrew-x86-terminal-apple-silicon-mac/>`_.

ROS2 Base
==========

Let's start by installing dependencies. First, you'll need Xcode developer tools
installed. Check for these by running :code:`xcode-select -v`. If they're not installed, 
run :code:`xcode-select --install`.

You'll also want to make sure Homebrew is installed. If you haven't installed :code:`brew`, do
that by running :code:`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

**If you're on M1** and you created a new Intel terminal for this (see the earlier note), know that you'll need to install brew
on your Intel terminal separately -- that is to say, even if you had brew installed on your other Terminal,
it doesn't carry over. You'll also want to add the following brew switch code to your :code:`.zshrc / .bash_profile`
(depending on what shell you use), in order to make sure that the shell uses the correct brew architecture.
Delete any other :code:`brew shellenv` commands in this file, if they exist, before putting this in:

.. code-block:: bash

    if [ "$(arch)" = "i386" ]
    then
        eval "$(/usr/local/bin/brew shellenv)"
    else
        eval "$(/opt/homebrew/bin/brew shellenv)"
    fi

To be clear -- if you're not on M1, this is not needed.

Finally, you'll want to make sure that you don't have Anaconda or any other conda in your environment.
If you have Anaconda installed, remove it from your terminal environment by either
uninstalling it altogether, or by removing the code that loads it into your shell in your :code:`.zshrc`
or :code:`.bash_profile`.

Now, let's actually begin installation. Run the following commands:

.. code-block:: bash

    brew update
    xcode-select -p
    brew install cppcheck eigen pcre poco tinyxml wget bullet bison
    export PATH="/usr/local/opt/bison/bin:$PATH"
    brew install python@3.8
    brew unlink python
    brew link --force --overwrite python@3.8
    brew install python@3.9
    brew install asio tinyxml2 opencv console_bridge openssl cmake
    export OPENSSL_ROOT_DIR=$(brew --prefix openssl)
    brew install log4cxx spdlog cunit qt@5 freetype assimp
    export CMAKE_PREFIX_PATH=$CMAKE_PREFIX_PATH:/usr/local/opt/qt@5
    export PATH=$PATH:/usr/local/opt/qt@5/bin
    brew install graphviz pyqt5 sip
    sudo python3 -m pip install -U \
        argcomplete catkin_pkg colcon-common-extensions coverage \
        cryptography empy flake8 flake8-blind-except flake8-builtins \
        flake8-class-newline flake8-comprehensions flake8-deprecated \
        flake8-docstrings flake8-import-order flake8-quotes ifcfg \
        importlib-metadata lark-parser lxml mock mypy netifaces \
        nose pep8 pydocstyle pydot pygraphviz pyparsing \
        pytest-mock rosdep setuptools vcstool rosdistro numpy

Add the following commands to your :code:`~/.bash_profile` file if you're using bash, or
:code:`~/.zshrc` if you're using zsh (the default for newer Macs). If you see a $ at the end
of your terminal, it's probably bash. If you see a %, it's probably zsh.

.. code-block:: bash

    export PATH="/usr/local/opt/bison/bin:$PATH"
    export OPENSSL_ROOT_DIR=$(brew --prefix openssl)
    export CMAKE_PREFIX_PATH=$CMAKE_PREFIX_PATH:/usr/local/opt/qt@5
    export PATH=$PATH:/usr/local/opt/qt@5/bin

Finally, quit and re-open your terminal.

Now, it's time to actually install ROS2. Go ahead and run the following commands:

.. code-block:: bash

    sudo mkdir -p /opt/ros/foxy
    sudo chown "$(whoami)" /opt/ros /opt/ros/foxy

Now, open up Finder, click Go > Go to folder in the top bar menu, and type in :code:`/opt/ros/foxy`.
You'll want to download ROS2 base `here <https://github.com/nkalupahana/ros2-foxy-macos/releases/download/ros2-foxy-base/ros2-foxy-base.zip>`_.
Then, move the ZIP file to :code:`/opt/ros/foxy`, and extract it. That's it! You have ROS installed.

To properly source ROS2, you'll want to add the following line to your :code:`.bash_profile` if you're using Bash:

.. code-block:: bash

    source /opt/ros/foxy/ros2-foxy-base/setup.bash

Or to your :code:`.zshrc` if you're using zsh:

.. code-block:: bash

    source /opt/ros/foxy/ros2-foxy-base/setup.zsh

Finally, these binaries aren't codesigned or verified by Apple, so in order to run them,
you'll have to clear Gatekeeper's warnings about them. To do that, run:

.. code-block:: bash

    xattr -cr /opt/ros/foxy

Eventually, we should have most of our binaries codesigned and notarized,
but that's... a lot of work I don't have time for right now.

Other Packages
===============

You'll see several other ROS package bundles on `the releases page <https://github.com/nkalupahana/ros2-foxy-macos/releases>`_,
in addition to ROS2 base. To install these, as needed:

- `Open the corresponding .bash file for the package you want to install <https://github.com/nkalupahana/ros2-foxy-macos/tree/main/setup>`_, and run any brew install commands it contains.
- Download the release zip, unzip it in :code:`/opt/ros/foxy`, and add a source line (like with base) in your :code:`.bash_profile` or :code:`.zshrc`.
- Run :code:`xattr -cr /opt/ros/foxy` to clear Gatekeeper warnings.

Verifying ROS2 Works
====================
In order to easily verify everything is installed and working correctly run the following commands and make sure there are no errors:

In one terminal run :code:`ros2 run demo_nodes_cpp talker` and in another terminal run :code:`ros2 run demo_nodes_cpp listener`.
If there are no errors while these run, that's great and means that C++ nodes work for ROS2 on your machine!

Next, in one terminal run :code:`ros2 run demo_nodes_py talker` and in another terminal run :code:`ros2 run demo_nodes_py listener`.
If there are no errors while these run, that's great and means that python nodes work for ROS2 on your machine!
