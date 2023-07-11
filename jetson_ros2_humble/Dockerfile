FROM arm64v8/ros:humble-ros-base

ARG OPT_PATH=/opt/uwb_ntis

RUN echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections

RUN sudo apt-get install -y -q

RUN lsb_release -a

RUN sudo apt-get -y update && sudo apt-get -y install git

RUN mkdir -p $OPT_PATH && cd $OPT_PATH && git clone https://github.com/neduchal/robot_system_core.git $OPT_PATH/robot_system_core

RUN ls opt/uwb_ntis

RUN ls $OPT_PATH/robot_system_core
