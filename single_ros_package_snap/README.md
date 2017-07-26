# Building a snap containing a single ROS package

The first step in this adventure was getting familiar with how Snaps works with
ROS. I figured making a Snap to launch turtlesim would be a great start.

I created a new workspace to build my snap 
```
$ mkdir -p single_snap/src
$ cd single_snap/src
$ git clone https://github.com/ros/ros_tutorials.git
```
This would provide the turtlesim package that I want to make into a snap. 

We also have to edit the CmakeLists.txt file for the turtlesim package. We have to tell catkin to install our desired files.
I added the following to the bottom of the Cmakelists.txt located in the single_snap/src/ros_tutorials/turtlesim/ directory
```
install(FILES launch/multisim.launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
```
Next I have to init Snapcraft in my new workspace, run `snapcraft init` in the root of your workspace

This creates a new file snap/snapcraft.yaml. The yaml file provides instructions
for Snapcraft on how to build the snap.

I editted the yaml file to look like this:
```
name: turtle-snap
version: '0.1' 
summary: Snap containing the turtlesim package
description: |
  Snap containing the turtlesim package

confinement: devmode

apps:
  launch:
    command: roslaunch turtlesim multisim

parts:
  turtlesim:
    plugin: catkin
    rosdistro: kinetic
    catkin-packages: [turtlesim]
```
The first several line of the yaml file are just general information about the
snap. I set the confinement of my snap to devmode. My goal is to make snaps that
would work in conjunction with my existing ROS system. Snaps are generally
confined into their own environment.

I defined an app named 'launch' which excutes the command:
`roslaunch turtlesim multisim.launch`

And defined a part 'turtlesim' that builds the turtlesim package with catkin.
The catkin plugin will then look for the turtlesim package in my /src directory
and then build it into the snap
.

I then build the snap by running `snapcraft` at the root of the directory and
waited for the build process, then installed and ran the snap
```
$ sudo snap install turtle-snap turtle-snap_0.1_amd64.snap --devmode --dangerous
$ turtle-snap.launch
```

You will get immediately greeted with the error:
`This application failed to start because it could not find or load the Qt platform plugin "xcb".`

This is caused by Qt plugins not being automatically pulled in to the snap, aswell as Qt expecting to be ran out of system paths. The solution is to use a ‘remote part’(sometimes called cloud part). The nessecary corrections are as follows:
```
name: turtle-snap
version: '0.1' 
summary: Snap containing the turtlesim package
description: |
  Snap containing the turtlesim package

confinement: devmode

apps:
  launch:
    command: desktop-launch roslaunch turtlesim multisim

parts:
  turtlesim:
    plugin: catkin
    rosdistro: kinetic
    catkin-packages: [turtlesim]
    after: [desktop-qt5]
```
This manual pulls down the Qt-5 plugin from the magical cloud, with these adjustments the snap will work and launch two turtlesims.
