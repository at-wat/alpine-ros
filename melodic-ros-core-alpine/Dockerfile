FROM alpine:edge

RUN apk add --no-cache \
    bash \
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
  && apk del .temp \
  && rm -rf /root/.cache/pip \
  && rm -rf /var/cache/apk/*

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

SHELL ["/bin/bash", "-c"]
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
RUN echo -e "import sys\nsys.setdefaultencoding('utf-8')" > /usr/lib/python2.7/site-packages/sitecustomize.py


RUN rosdep init \
  && sed -i -e 's/ros\/rosdistro\/master/at-wat\/rosdistro\/alpine/' /etc/ros/rosdep/sources.list.d/20-default.list \
  && rosdep update

ENV ROS_DISTRO melodic
ENV ROS_PACKAGE_PATH /opt/ros/${ROS_DISTRO}/share

RUN mkdir -p /tmp_ws/src/ \
  && cd /tmp_ws/ \
  && rosinstall_generator --rosdistro ${ROS_DISTRO} --deps --tar ros_core --exclude RPP > ros-core.rosinstall \
  && wstool init -j8 src ros-core.rosinstall \
  && rosdep install -y --from-paths src --ignore-src \
  && apk add --virtual=.build-dep g++ gcc musl-dev make cmake python-dev \
  && cd /tmp_ws/ \
  && src/catkin/bin/catkin_make_isolated --install --install-space /opt/ros/${ROS_DISTRO} -DCMAKE_BUILD_TYPE=Release -DCATKIN_ENABLE_TESTING=OFF \
  && apk del .build-dep \
  && apk del "*-dev" \
  && apk add boost \
  && cd / \
  && rm -rf /tmp_ws \
  && rm -rf /root/.cache/pip \
  && rm -rf /var/cache/apk/*

COPY ros-entrypoint.sh /
ENTRYPOINT ["/ros-entrypoint.sh"]
