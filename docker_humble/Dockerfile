FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

# ---------------------------------------------------------
# Pacotes básicos que existem no Ubuntu puro
# ---------------------------------------------------------
RUN apt-get update && apt-get install -y \
    locales \
    curl \
    gnupg \
    lsb-release \
    software-properties-common \
    ca-certificates \
    git \
    wget \
    build-essential \
    cmake \
    python3 \
    python3-pip \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

# ---------------------------------------------------------
# Repositório ROS 2
# ---------------------------------------------------------
RUN curl -sSL \
    https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \
    -o /usr/share/keyrings/ros-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] \
    http://packages.ros.org/ros2/ubuntu jammy main" \
    > /etc/apt/sources.list.d/ros2.list

# ---------------------------------------------------------
# Repositório Gazebo / OSRF
# ---------------------------------------------------------
RUN curl -sSL \
    https://packages.osrfoundation.org/gazebo.gpg \
    -o /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] \
    https://packages.osrfoundation.org/gazebo/ubuntu-stable jammy main" \
    > /etc/apt/sources.list.d/gazebo-stable.list

# ---------------------------------------------------------
# ROS 2 Humble + ferramentas
# ---------------------------------------------------------
RUN apt-get update && apt-get install -y \
    ros-humble-desktop \
    python3-colcon-common-extensions \
    python3-rosdep \
    ros-humble-teleop-twist-keyboard \
    ros-humble-xacro \
    ros-humble-depth-image-proc \
    libeigen3-dev \
    mesa-utils \
    && rm -rf /var/lib/apt/lists/*

# ---------------------------------------------------------
# Gazebo Harmonic + ros_gz específico Humble/Harmonic
# ---------------------------------------------------------
RUN apt-get update && apt-get install -y \
    gz-harmonic \
    ros-humble-ros-gzharmonic \
    && rm -rf /var/lib/apt/lists/*

RUN rosdep init || true

RUN echo "source /opt/ros/humble/setup.bash" >> /root/.bashrc
RUN echo "export GZ_VERSION=harmonic" >> /root/.bashrc

WORKDIR /workspace

CMD ["/bin/bash"]
