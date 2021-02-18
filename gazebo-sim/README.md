# Gazebo Simulator

Here we explain how to run a [Gazebo](http://gazebosim.org/) simulation on Docker.

A gazebo image is created after [this](https://hub.docker.com/_/gazebo). The Dockerfile is available in ./docker/gazebo/.

Building the Docker image:

```
$ cd docker/gazebo/
$ docker build -t gazebo .
```

Now you need to configure your OS for running GUI apps on Docker. Note that the right thing would be to connect to the Gazebo server (gzserver) from a remote client (gzclient). However, we want to reduce network overhead. Therefore, we choose to run Docker apps with [Rocker](https://github.com/osrf/rocker).

Installing Rocker:
```bash
$ pip install rocker
```

Running with NVidia display cards:
```bash
$ rocker --nvidia --x11 --user --home gazebo
```

Running with other/generic cards:
```bash
$ rocker --devices /dev/dri/card0 --x11 --user --home gazebo
```
## Gazebo + ROS

First of all, check the following tutorials:
- [Simulation on ROS2](https://emanual.robotis.com/docs/en/platform/turtlebot3/ros2_simulation/)
- [Possible Dependencies](https://emanual.robotis.com/docs/en/platform/turtlebot3/ros2_setup/)

A preset Dockerfile is available in ./docker/gazebo-ros/.

Building the Docker image (it is going to take a while):
```bash
$ cd docker/gazebo-ros/
$ docker build -t gazebo-ros .
```

Running a containered image:
```bash
$ docker --nvidia --x11 --user --home gazebo-ros 
```

From now on you will be in the Docker container shell. You must configure the environment (need to put this in the Dockerfile):
```bash
# ./setup.sh
# source source.sh
```

Running a simulation example:
```
# ros2 launch turtlebot3_gazebo empty_world.launch.py
```

## Creating a World (Gazebo Model)

You can follow [this](http://gazebosim.org/tutorials?tut=build_world) tutorial.

## Our Models

For specific experiments, we have been using the following world.

- [Indoor Navigation](#)

You can also play with other models from [there](https://github.com/osrf/gazebo_models).

## Gazebo and ROS

```bash
$ cd ../gazebo-ros/
$ docker build -t gazebo-ros .
$ rocker --devices /dev/dri/card0 --x11 --user --home gazebo-ros
```

## Robot Runner and Gazebo

...