## [DEPRECATED] This repository has been deprecated!
Latest working Alpine ROS Dockerfile is available at https://github.com/alpine-ros/alpine-ros

----

# Experimental ros_core image for Alpine Linux with custom apk repository

## Benefits

Using Alpine Linux as base system incredibly decreases installation size.
The image size of ros_core on Alpine Linux built with this package is 539MB.
Our good friend Ubuntu based ROS image (ros:melodic-ros-core) is 997MB.

```
ros        melodic-ros-core-alpine-custom-apk   0a7aeffebf4b        22 minutes ago      539MB  (Alpine based)
ros        melodic-ros-core                     56161463aa0c        8 days ago          997MB  (Ubuntu based)
```

## Build

```shell
$ docker build -t ros:melodic-ros-core-alpine-custom-apk .
```

## Enjoy

You can now play with the message communication!

```shell
$ docker run -it --rm ros:melodic-ros-core-alpine-custom-apk
```

```shell
/ # roscore &
/ # rostopic echo /test &
/ # rostopic pub -r1 -s /test std_msgs/Header 'frame_id: "frame"
stamp: now'
```

## How it works

### Building and providing custom dependent packages

1. Custom apks are built with https://github.com/seqsense/ros-abuild-docker script.
  - package definitions are at https://github.com/seqsense/aports-ros-experimental
  - this contains backport packages from alpine:edge and new not-yet-submitted packages
2. Generated custom apks are placed at http://alpine-ros-experimental.dev-sq.work/

### Enabling custom apk repository

This docker image uses following custom configurations:
- forked rosdistro for testing (https://github.com/at-wat/rosdistro/tree/alpine-custom-apk)
- custom apk repository and its public key
