************************
Project 2: State Machine
************************

This project will extend on what you built in project 1 so make sure that is working!

Objectives
==========
- Explain how the state machine is used to implement logic for autonomous operations
- Create a state machine that uses data from a topic to make decisions

State Machine Specifications
============================
Before going any further, go read up on the state machine part of the documentation. 
Now that you have an understanding of state machines, you will create a state machine that:

- Starts in a :code:`waiting` state that simply logs to the terminal it is waiting for user input
- Any key press except :code:`w` makes the state machine enter a :code:`try-again` state
- Exits the state machine when :code:`w` key is pressed

Using Nodes in a State
======================
In order to listen to topics in order to build more dynamic states, you will want to integrate a node into your state class.
There are 3 options for how to use a node in a state:

1) The state can inherit from the :code:`Node` class as well as the :code:`State` class
2) The state constructor can create a :code:`Node` object as a member variable
3) The state constructor can take in a :code:`Node` as a parameter

Test your States
================
Run the state machine and ensure it works according to the specs by observing the ouputs logged to the terminal
