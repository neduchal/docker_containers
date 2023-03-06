FROM osrf/ros:foxy-desktop

# Zkusit https://robots.uc3m.es/installation-guides/install-realsense2.html instalaci z buildu.

ARG OPT_PATH=/opt/uwb_ntis

ENV DEBIAN_FRONTEND noninteractive


RUN echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections

RUN apt -q -qq update && \
    DEBIAN_FRONTEND=noninteractive apt install -y \
    software-properties-common \
    wget \
    apt-transport-https

RUN sudo apt-get install -y -q

RUN sudo apt -y install fakeroot libfakeroot

RUN sudo apt-get -y update &&  sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo apt-get -y install git

RUN sudo apt-get -y install software-properties-common

RUN sudo apt-get -y install curl zip unzip tar

RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE \
    && sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u

RUN sudo apt-get -y update && sudo apt-get -y install librealsense2-dkms librealsense2-utils librealsense2-dev  --allow-unauthenticated 

RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/neduchal/robot_system_core.git $OPT_PATH/robot_system_core

RUN ls opt/uwb_ntis

RUN ls $OPT_PATH/robot_system_core






