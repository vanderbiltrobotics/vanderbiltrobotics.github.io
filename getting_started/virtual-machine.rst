***************
Virtual Machine
***************

Setting up a virtual machine to run Ubuntu 20.04 on your windows or mac laptop is one possibility if 
you are having trouble installing ROS2 on your laptop.

#. Download and install `Virtual Box <https://www.virtualbox.org>`_
#. Create a new virtual machine and running Ubuntu Desktop 20.04 LTS by following `these <https://linuxhint.com/install_ubuntu_virtualbox_2004/>`_ directions 
#. Install ROS2 Foxy according to the linux install documentation

.. warning::

    USB passthrough for camera data or joystick data is tricky to get working with virtual box but the
    intro projects have been designed to not require either 