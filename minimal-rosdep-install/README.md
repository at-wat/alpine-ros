## [DEPRECATED] This repository has been deprecated!
Latest working Alpine ROS Dockerfile is available at https://github.com/alpine-ros/alpine-ros

----

# rosdep install in alpine docker container

This repository has sample manifest with a dependency to tinyxml.
Following command demonstrates that `rosdep install --from-paths src` command installs tinyxml package by using apk installer.

```shell
$ docker build -t ros:kinetic-alpine-demo .
```
