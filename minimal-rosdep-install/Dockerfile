FROM alpine:3.7

RUN apk add --no-cache \
    py-pip \
    python \
  && apk add --no-cache --virtual .temp \
    git \
  && pip install \
    rosinstall \
    rosinstall_generator \
    wstool \
    git+https://github.com/at-wat/rospkg.git@fix-alpine-detect \
    git+https://github.com/at-wat/rosdep.git@alpine-installer \
  && apk del .temp

RUN rosdep init \
  && sed -i -e 's/ros\/rosdistro\/master/at-wat\/rosdistro\/add-alpine-ros-core-deps/' /etc/ros/rosdep/sources.list.d/20-default.list \
  && rosdep update

ENV ROS_DISTRO kinetic
ENV ROS_PACKAGE_PATH /opt/ros/${ROS_DISTRO}/share

COPY sample_pkg /test_ws/src/
WORKDIR /test_ws
RUN rosdep install -y --from-paths src
