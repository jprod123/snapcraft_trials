## Making dependant snaps

Making a pair of snaps that which one snap depends on the other is very well
documented:
(https://kyrofa.com/posts/distributing-a-ros-system-among-multiple-snaps)

What isn't how ever is how to make a snap that has a second-order dependancy.
Turns out the catkin plugin doesn't help much in this scenario. This is an issue
because if we were to make each ROS package its own snap then it could have
multiple dependancies which would have their own dependancies. It gets very
messy quickly.
