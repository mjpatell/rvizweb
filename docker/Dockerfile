#FROM ros:kinetic
FROM ros:noetic

# Basic tools and dependencies and nodejs LTS PPA.
RUN rosdep update && apt update
RUN apt install -y curl git
#RUN curl -sL https://deb.nodesource.com/node_8.x | bash -
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y python3-cbor

# Install rvizweb.
WORKDIR /rvizweb_ws
ARG rvizweb_branch=master
RUN git clone https://github.com/osrf/rvizweb/ src/rvizweb -b ${rvizweb_branch}
RUN rosdep update
RUN rosdep install --from-paths src --ignore-src -r -y
RUN . /opt/ros/noetic/setup.sh && catkin_make install

# Clear apt cache.
RUN apt clean

ENTRYPOINT ["/bin/bash", "-c", "source /rvizweb_ws/install/setup.bash && /bin/bash"]
