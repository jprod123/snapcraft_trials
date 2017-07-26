# Snapcraft Trials
This repository contains documentation and examples of my attempts on using
snapcraft with ROS. The goal of these trails was to find an alternative
distribution method of ROS binary packages. This would lower the entry
barrier to publishing ROS binaries, allowing for variations on different
packages to be published and installed rather than building them from source.
Unfortunately I was unable to succeed in this endeavor but these trails may
prove useful to someone trying to use snapcraft with ROS in the future

Some of these examples are adapted from existing guides on using snapcraft with
ROS. These guides are very informative and I highly recommend looking through
them as well.

##### General information on snaps and how they work with ROS
http://wiki.ros.org/ROS/Tutorials/Packaging%20your%20ROS%20project%20as%20a%20snap

##### Basic ROS snap
https://github.com/snapcore/snapcraft/tree/master/demos/ros

##### Using ROSinstall with snaps
https://github.com/snapcore/snapcraft/tree/master/demos/rosinstall

##### Distributing a ROS package over multiple snaps
https://github.com/snapcore/snapcraft/tree/master/demos/shared-ros
https://kyrofa.com/posts/distributing-a-ros-system-among-multiple-snaps
https://kyrofa.com/posts/from-ros-prototype-to-production-on-ubuntu-core-1-5

##### Using rosinstall to make snaps from github
https://github.com/snapcore/snapcraft/tree/master/demos/rosinstall

---


I hope to offer a novice's perspective on snap and ROS in general that will
help lower the entry barrier to these ecosystems.

## Approach

The end goal was to create a new way to distribute ROS binaries. I thought of
approaching this issue in smaller modular tasks. I broke down the end goal into
smaller more beginner friendly steps. Each step being a proof of concept for
the larger end goal and having sub goals of their own

1. Creating a Snap containing a single ROS package
    * Preliminary introduction to Snaps...(got to start somewhere)
    * Create a snap that one could overlay onto their existing workspace further probing the idea of a fully modular ROS ecosystem as Snaps

2. Creating a pair of Snaps where one depended on the other
    * Probing the idea if ROS could be distributed as modular snaps
    * Create a snap with a second-order dependency

3. Building a Snap directly from GitHub:
    * Proof of concept that one could automate building of snaps from GitHub
    
 
 ---
 
 This was done on Ubuntu 16.04 with ROS Kinetic
