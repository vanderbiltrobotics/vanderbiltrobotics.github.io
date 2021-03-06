**************************
Basics & Setting Up States
**************************

Relevant package: `state_machine <https://github.com/vanderbiltrobotics/lunabot-ros2/tree/main/state_machine>`_

Robots typically operate in different states. When our robot starts up, it needs to localize, 
move to the digging area, dig there, move to the deposotion area, deposit, and then repeat. Each of
these can be thought of as a different "state", and all the robot does is move from state to state
as it completes its tasks. The state_machine package provides the framework for setting up and moving
between states, and provides a useful logging infrasturcture for use within states.

How To Set Up A State
======================

In the tests folder of the :code:`state_machine` pacakge, there are a few sample states.
**This is probably your best reference for this package, because these tests
make up a full state machine.** We recommend you run :code:`python3 main.py` 
in the tests folder to check out this sample state machine.
Let's take a look at a sample state in the tests -- in this case, this is a Navigation state that moves
the robot to a given pose.

.. note::

    Make sure you've run :code:`colcon build` on our workspace and sourced it,
    in order to get access to the state_machine package!


.. code-block:: python

    from state_machine import State
    from time import sleep
    import find_charuco
    import random

    class Navigation(State):
        def __init__(self):
            self.pose = [0, 0]

        def executors(self):
            return [
                Navigation.go_to_pose,
                Navigation.check_map_lost,
            ]

        def go_to_pose(self, kwargs):
            goal_pose = kwargs["goal_pose"]
            while self.pose[0] < goal_pose[0] or self.pose[1] < goal_pose[1]:
                self.log(f"Current Pose: {self.pose}")
                if self.pose[0] < goal_pose[0]:
                    self.pose[0] += 0.1
                if self.pose[1] < goal_pose[1]:
                    self.pose[1] += 0.1
                sleep(0.5)
            return None, {}

        def check_map_lost(self):
            while True:
                sleep(2)
                if random.random() < 0.05:
                    return find_charuco.FindCharuco(), {}

Let's take a look at the important parts of this file, starting from the top.

.. code-block:: python

    from state_machine import State

:code:`State` is an abstract class from the state_machine package, and it's what
all states you create should inherit from.

.. code-block:: python

    class Navigation(State):

And here's that inheritance.

Now, this state machine library has been set up to allow for each state to
execute multiple functions in parallel (at the same time). We call each of these functions **executors**.
In this state, you can see that there are two exectors -- :code:`go_to_pose` and :code:`check_map_lost`.
When you enter the Navigation state, both executors will be started, and will
run in parallel. In this case, the :code:`go_to_pose executor` moves the robot to 
the pose, while :code:`check_map_lost` checks to see if mapping has lost the map.

Executors must be registered via the :code:`executors` function, whose only argument is self and returns
a list of all executors that the state should run. If you forget to do this, you will not be able to instantiate the class.

The first executor that returns determines which state the state machine
will go to next. For example, if we lose the map (and let's face it, we probably will), :code:`check_map_lost`
will detect that and return a tuple -- a constructed object of the state to move to next 
(in this case, :code:`FindCharuco()`), and any arguments you want to give that state 
(in a map: e.g. :code:`{"arg1": 1, "arg2", 2}`). Future states can use the arguments you 
put in the map to change their behavior. You can actually see
that in this state -- in :code:`go_to_pose`, :code:`goal_pose` is from :code:`kwargs`, which means
it came from the arguments of the previous state. 

This is another important feature of this state machine library -- states can pass information
to each other to change their behavior. Here's another potential use case for this
(not in our tests, just an example of what this might look like).

.. code-block:: python

    from state_machine import State
    from time import sleep
    import back_up
    import random

    class Navigation(State):
        def __init__(self):
            self.pose = [0, 0]

        def executors(self):
            return [
                Navigation.go_to_pose,
                Navigation.check_map_lost,
            ]

        def go_to_pose(self, kwargs):
            goal_pose = kwargs["goal_pose"]
            while self.pose[0] < goal_pose[0] or self.pose[1] < goal_pose[1]:
                self.log(f"Current Pose: {self.pose}")
                if self.pose[0] < goal_pose[0]:
                    self.pose[0] += 0.1
                if self.pose[1] < goal_pose[1]:
                    self.pose[1] += 0.1
                sleep(0.5)
            return None, {}

        def check_map_lost(self, kwargs):
            while True:
                sleep(2)
                if random.random() < 0.05:
                    return back_up.BackUp(), {
                        "return_to": Navigation,
                        "goal_pose": kwargs["goal_pose"]
                    }

Look at :code:`check_map_lost`. Even if this exits Navigation to regain our map by backing up,
the :code:`BackUp` state knows what state to return to (:code:`Navigation`) once it's done regaining the map.
You can even include :code:`Navigation`'s original arguments here, so :code:`BackUp` can pass them back to :code:`Navigation`.

Executors can either have one or two parameters: :code:`self`, or :code:`self` and :code:`kwargs` (the argument map from the
previous state). If you don't need arguments, then you don't need to include the :code:`kwargs` parameter.

Finally, one more feature: instead of using the :code:`print` function, use :code:`self.log`. This will automatically print
the name of the state along with your log message, allowing for smoother debugging.

Running the State Machine
==========================

In order to start the state machine, construct the intitial state and run its :code:`start()` function. For example:

.. code-block:: python

    import find_charuco
    find_charuco.FindCharuco().start()

States will move to their next states automatically, so only call :code:`start()` on the initial state.
In order to end the state machine, :code:`return (None, {})` at the end of an executor 
(see the end of :code:`go_to_pose` for an example of this).

