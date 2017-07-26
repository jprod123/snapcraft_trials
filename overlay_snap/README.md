# Overlaying a snap onto my existing workspace

The end goal being to distribute a single ROS package as a snap requires that we
be able to overlay the snap. The issue with this is because the snap create its
own isolated enviroment all of its files are relative to the enviroment variable
'$SNAP' meaning if I were to source it from outside the snap it would not be
defined. Luckily we can change the snap confinement to 'classic'. This would
change all the relative paths to absolute paths. 

In this case we have a very similar snapcraft.yaml file to our previous
single_ros_package_snap:
```
name: turtle-snap
version: '0.1' 
summary: Snap containing the turtlesim package
description: |
  Snap containing the turtlesim package

confinement: classic

parts:
  turtlesim:
    plugin: catkin
    rosdistro: kinetic
    catkin-packages: [turtlesim]
```

The key difference here is changing the confinement from devmode to classic and
the removal of the snap app. Because the paths of the snap are absolute we no
longer need snap to create a command wrapper for us.

When installing a snap they install into the '/snap/'snap-name' directory. We
can now go and source the snap's setup.bash file
```
$ source /snap/turtle-snap/x1/opt/ros/kinetic/setup.bash --extend
```

We can now run ros packages that are in the snap and execute the command from
the previous example.

```
$ roslaunch turtlesim multisim.launch
```