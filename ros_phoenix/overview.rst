********
Overview
********
This package is used to interface with CTRE motor controllers.
Currently the package consists of components and nodes for controlling 
Victor SPXs, Talon SRXs, and Falcon 500s. We use Talon SRXs on the robot so 
you don't need to worry about the others for now. Additionally, we currently use
only the node version for controlling the Talons as the launching multiple talons
using components has a underyling issue that needs to be resolved (soon to be fixed). This means the primary files of 
interest in the package are:

* :code:`include/base_component.hpp`- contains all the core implementation for controlling victors, talons, and falcons.
* :code:`src/talon_node.cpp`- initializes and runs a talon node 
* :code:`launch/arm.launch.py`- launches the talon nodes for controlling the motors in the excavation arm
* :code:`launch/drive.launch.py`- launches the talon nodes for the 4 motors that move the robot 