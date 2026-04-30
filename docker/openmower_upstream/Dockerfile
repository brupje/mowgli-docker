## Build from the official upstream OpenMower repository image
FROM ghcr.io/brupje/open_mower_ros:sha-d9a0f38@sha256:664e48f0bbd309b0b7927a7af6eea60576a5ec79e7ececcce95ee7b37a1800c2
# Upstream image runs as non-root, switch to root for setup
USER root

# Set timezone
ENV TZ=Europe/Paris
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install rosserial
RUN mkdir -p /home/ubuntu/rosserial/src && cd /home/ubuntu/rosserial/src && git clone https://github.com/tongtybj/rosserial && cd rosserial && git checkout rosservice_server
RUN bash -c 'source /opt/ros/noetic/setup.bash && cd /home/ubuntu/rosserial && catkin_make -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic install --only-pkg-with-deps rosserial_server'

ADD scripts /home/ubuntu/scripts
RUN chmod +x /home/ubuntu/scripts/*.sh

CMD [ "/home/ubuntu/scripts/start_mowgli.sh" ]
