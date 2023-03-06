FROM osrf/ros:humble-desktop

ARG OPT_PATH=/opt/uwb_ntis

RUN echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections

RUN sudo apt-get install -y -q

RUN sudo apt-get -y update &&  sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo apt-get -y install git

RUN sudo apt-get -y install software-properties-common

RUN sudo apt-get -y install curl zip unzip tar

RUN sudo apt install -y dbus-x11

#  PackageKit-gtk3-module libcanberra-gtk2

# LIB REALSENSE 2.51.1
RUN sudo apt-get -y install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/IntelRealSense/librealsense.git $OPT_PATH/librealsense
RUN cd $OPT_PATH/librealsense && git checkout v2.51.1 &&  bash ./scripts/setup_udev_rules.sh 
# && bash ./scripts/patch-realsense-ubuntu-lts.sh 
RUN cd $OPT_PATH/librealsense && mkdir build && cd build && cmake ../ && sudo make uninstall && make clean && make && sudo make install
# RELASENSE ROS2 
RUN sudo apt-get install python3-rosdep -y
RUN mkdir -p /home/neduchal/ros2_ws/src && d /home/neduchal/ros2_ws/src && git clone https://github.com/IntelRealSense/realsense-ros.git -b ros2-development
RUN cd /home/neduchal/ros2_ws/ && sudo rosdep init && rosdep update && rosdep install -i --from-path src --rosdistro $ROS_DISTRO --skip-keys=librealsense2 -y
RUN cd /home/neduchal/ros2_ws/ && colcon build && source /opt/ros/humble/setup.bash && . install/local_setup.bash

#RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/Microsoft/vcpkg.git $OPT_PATH/vcpkg

#RUN cd $OPT_PATH/vcpkg && ./bootstrap-vcpkg.sh && ./vcpkg integrate install && ./vcpkg install realsense2


#RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE \
#    && sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u

##RUN sudo apt-get -y update && sudo apt-get install librealsense2-dkms librealsense2-utils ibrealsense2-dev

RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/neduchal/robot_system_core.git $OPT_PATH/robot_system_core

RUN ls opt/uwb_ntis

RUN ls $OPT_PATH/robot_system_core






