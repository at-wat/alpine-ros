<div style="width: 100%; background: 0xFFFF99">
**[DEPRECATED] This repository has been deprecated. Latest working Alpine ROS Dockerfile is available at https://github.com/alpine-ros/alpine-ros**
<div>

# Experimental ros_core image for Alpine Linux

## Build

```shell
$ docker build -t ros:melodic-ros-core-alpine .
```

## Enjoy

You can now play with the message communication!

```shell
$ docker run -it --rm ros:melodic-ros-core-alpine
```

```shell
bash-4.4# roscore &
bash-4.4# rostopic echo /test &
bash-4.4# rostopic pub -r1 -s /test std_msgs/Header 'frame_id: "frame"
stamp: now'
```
