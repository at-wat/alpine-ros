# Experimental ros_core image for Alpine Linux with custom apk repository

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
bash-4.4# roscore &
bash-4.4# rostopic echo /test &
bash-4.4# rostopic pub -r1 -s /test std_msgs/Header 'frame_id: "frame"
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
