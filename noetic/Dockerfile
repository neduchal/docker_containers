FROM osrf/ros:noetic-desktop
SHELL ["/bin/bash", "-c"]
ARG OPT_PATH=/opt/uwb_ntis

RUN echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections

RUN sudo apt-get install -y -q

RUN sudo apt-get -y update &&  sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo apt-get -y install git

RUN sudo apt-get -y install software-properties-common

RUN sudo apt-get -y install curl zip unzip tar wget mc htop

RUN sudo apt install -y dbus-x11

RUN sudo apt install python3-pip -y

RUN pip3 install pyrealsense2

#  PackageKit-gtk3-module libcanberra-gtk2

# LIB REALSENSE 2.51.1
#RUN sudo apt-get -y install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
#RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/IntelRealSense/librealsense.git $OPT_PATH/librealsense
#RUN cd $OPT_PATH/librealsense && git checkout v2.51.1 &&  bash ./scripts/setup_udev_rules.sh 
#RUN cd $OPT_PATH/librealsense && git checkout v2.53.1 && bash ./scripts/patch-realsense-ubuntu-lts-hwe.sh
#RUN cd $OPT_PATH/librealsense && git checkout v2.51.1 && mkdir build && cd build && cmake ../ && sudo make uninstall && make clean && make && sudo make install

#RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/Microsoft/vcpkg.git $OPT_PATH/vcpkg

#RUN cd $OPT_PATH/vcpkg && ./bootstrap-vcpkg.sh && ./vcpkg integrate install && ./vcpkg install realsense2


#RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE \
#    && sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u

#RUN sudo apt-get -y update && sudo apt-get install -y librealsense2-dkms librealsense2-utils librealsense2-dev

# RELASENSE ros 
RUN sudo apt-get install python3-rosdep -y
#RUN mkdir -p /home/neduchal/ros_ws/src && cd /home/neduchal/ros_ws/src && git clone https://github.com/IntelRealSense/realsense-ros.git -b ros-development
#RUN cd /home/neduchal/ros_ws/ && rosdep update && rosdep install -i --from-path src --rosdistro $ROS_DISTRO --skip-keys=librealsense2 -y
#sudo rosdep init && noetic

#RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/neduchal/robot_system_core.git $OPT_PATH/robot_system_core
#RUN git clone https://github.com/neduchal/home_navigation.git /home/neduchal/ros_ws/src/home_navigation

#RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc && . .bashrc


RUN source /opt/ros/noetic/setup.bash

ENTRYPOINT ["bash","-i","/ros_entrypoint.sh"]
##RUN source ros_entrypoint.sh && cd /home/neduchal/ros_ws/ && colcon build && . ./install/local_setup.bash

#RUN ls opt/uwb_ntis

#RUN ls $OPT_PATH/robot_system_core






