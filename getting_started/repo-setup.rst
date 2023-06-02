****************
Repository Setup
****************
In order to work on the robot, you will need to setup the repository on your local machine eventually so we will have you 
do it before startingt the intro project. You will just complete the intro project on a seperate personal branch on your local machine

#. Make a :code:`lunabot_ws` folder
#. Change directory into :code:`lunabot_ws` in the terminal
#. Clone the repository into a folder called source by running: :code:`git clone https://github.com/vanderbiltrobotics/lunabot-ros2.git src`
#. Change directory back to :code:`lunabot_ws` in the terminal
#. Build the code by running :code:`colcon build` (you will likely get errors if you are on macOS or Windows since not all the packages are fully supported on those platforms)
    - Use :code:`colcon build --packages-select <package-1> <package-2>` to only build selected packages
#. To be able to use any nodes built, you must run :code:`. install/local_setup.bash` (ubuntu terminal), :code:`. install/local_setup.zsh` (macOS terminal), or :code:`. install/local_setup.ps1` (powershell)
#. Now you can run any nodes/launch files

.. note:: 
    Your :code:`lunabot_ws` folder should look like this when you are finished:

    .. image:: static/ros-ws.png
        :width: 300


.. note:: 
    Before starting the intro projects, switch from the main branch to your own local branch for the project by running:
    :code:`git checkout -b intro/<name>`
    Also, you can make commits to this branch but do not push it to the github repository since then everyone else will 
    be deprived of figuring out the projects themselves :)
