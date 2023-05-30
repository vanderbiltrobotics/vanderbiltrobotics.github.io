*******************************
VU Robotics ROS2 documentation
*******************************

Welcome to VUR's main documentation site! 
There are three main types of documentation here:

1. **Package Use.** The most important part -- how to properly use packages and code (how to write a ROS controller, creating a URDF, tuning mapping packages, etc.) 
2. **Theory.** Theory behind important autonomy and ROS2 concepts (EKF, ChArUco, etc.) 
3. **Tutorials.** Starter projects to get people introduced to ROS2 and robotics concepts.

Building From Source
--------------------

* `Install Sphinx. <https://www.sphinx-doc.org/en/master/usage/installation.html>`_
* :code:`cd docs`
* Install package requirements with :code:`pip install -r requirements.txt`
* :code:`make html`
* Open :code:`index.html` in the :code:`_build` folder, and you're up and running!

.. note:: 
    If you added something to the table of contents in :code:`index.rst` and it is not showing 
    up after you build, run :code:`make clean` and then :code:`make html` 

Contributing
------------
Contributing to the ROS2 version of our code requires you to
document both your code process and theory. Here's how our documentation is structured:

* When documenting a new major package group (e.g. MoveIt), it goes in its own folder.
* Every time you create a new section/file/anything that should end up on the table of contents, it should be added in :code:`index.rst`.
* Our docs are written in `ReStructured Text <https://sublime-and-sphinx-guide.readthedocs.io/en/latest/index.html>`_ and `Markdown <https://guides.github.com/features/mastering-markdown/>`_. 

When you PR into the ROS2 repository, you'll be expected to have your documentation updated.