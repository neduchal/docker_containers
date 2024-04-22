FROM osrf/ros:humble-desktop

ARG OPT_PATH=/opt/uwb_ntis

RUN echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections

RUN sudo apt-get install -y -q

RUN sudo apt-get -y update &&  sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo apt-get -y install git

RUN sudo apt-get -y install software-properties-common

RUN sudo apt-get -y install curl zip unzip tar

RUN sudo apt install -y dbus-x11

#  PackageKit-gtk3-module libcanberra-gtk2



#RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/Microsoft/vcpkg.git $OPT_PATH/vcpkg

#RUN cd $OPT_PATH/vcpkg && ./bootstrap-vcpkg.sh && ./vcpkg integrate install && ./vcpkg install realsense2


#RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE \
#    && sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u

##RUN sudo apt-get -y update && sudo apt-get install librealsense2-dkms librealsense2-utils ibrealsense2-dev

#RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/neduchal/robot_system_core.git $OPT_PATH/robot_system_core

#RUN ls opt/uwb_ntis

#RUN ls $OPT_PATH/robot_system_core






