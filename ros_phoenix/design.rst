**************
Package Design
**************
In the goal of a package that can be easily used to interface with any of the CTRE motors, this package
was designed using templates.
:code:`base_component.hpp` contains the core implementation for controlling all the motors and is a template class.
In order to get a Talon implementation, a type definition is used on a template of the base component that
takes in 4 classes specific to a talon. Ideally, any motor type could be templated with just one class but that's
not how the CTRE libraries were designed so we use a type definition to wrap the ugly template with 4 classes into 
an easy to use TalonSPX type in the :code:`talon_component.hpp`. This TalonSPX type is then used in 
:code:`talon_node.cpp` to create a TalonSPX node, with all the implementation details abstracted away to the 
base_component, leaving a very simple file that simply initializes and runs the node.

.. warning::
    Launching multiple talons using composition and :code:`talon_component.cpp` currently does not
    work due to each component trying to launch a diagnostic server on the same port.

.. note::
    The diagnostic server is on by default. Adding :code:`c_SetPhoenixDiagnosticsStartTime(-1);` 
    turns the diagnostic server off. 
