# Localization & Mapping

Localization is the process of determining the location (position) and orientation of a robot relative to its environment. Solving the localization problem requires that the robot has a map of the entire environment from which it can determine its position.

Mapping is the process of generating a map of the robot's environment. In order to generate a map of the environment, the robot's exact position must be known (so that the map can be generated relative to the robot's position and orientation).

These two problems are inherently coupled and often must be solve simultaneously (determine the robot's location in an unknown environment). This is where simultaneous localization and mapping (SLAM) algorithms come in. These algorithms are capable of building a map of the environment while also localizing the robot relative to that map using probabilistic techniques.

## Resources
- [(Book) Probabilistic Robotics](http://www.probabilistic-robotics.org): math heavy but written by experts in the field  
- [(Videos) SLAM Course Lectures](https://www.youtube.com/playlist?list=PLgnQpQtFTOGQrZ4O5QzbIHgl3b1JHimN_): starts high level but dives deeper into the math and implementation details
- [(Videos) Kalman Filter Series](https://www.youtube.com/watch?v=CaCcOwJPytQ): Dives into math but also uses lots of good examples
- [(Paper) SLAM Essential Algorithms](https://people.eecs.berkeley.edu/~pabbeel/cs287-fa09/readings/Durrant-Whyte_Bailey_SLAM-tutorial-I.pdf): explains basic algorithms & implementations. Recommended by Dr. Peters