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

RUN sudo apt install terminator -y

# RELASENSE ros 
RUN sudo apt-get install python3-rosdep python3-catkin-tools -y

RUN source /opt/ros/noetic/setup.bash

COPY arena_api-2.3.3-py3-none-any.zip arena_api-2.3.3-py3-none-any.zip   
COPY ArenaSDK_v0.1.84_Linux_x64.tar.gz ArenaSDK_v0.1.84_Linux_x64.tar.gz

RUN mkdir -p /home/smart/
RUN tar -xzvf ArenaSDK_v0.1.84_Linux_x64.tar.gz  && ls
RUN cp -r ./ArenaSDK_Linux_x64 /home/smart/ArenaSDK && ls
RUN cd /home/smart/ArenaSDK && sudo sh ./Arena_SDK_Linux_x64.conf
RUN unzip arena_api-2.3.3-py3-none-any.zip -d arena_python_temp
RUN cd arena_python_temp && pip install arena_api-2.3.3-py3-none-any.whl
RUN rm -rf /ArenaSDK_Linux_x64 
RUN rm -rf ArenaSDK_v0.1.84_Linux_x64.tar.gz
RUN rm -rf arena_python_temp

ENV ARENA_ROOT=/home/smart/ArenaSDK

ENTRYPOINT ["bash","-i","/ros_entrypoint.sh"]
##RUN source ros_entrypoint.sh && cd /home/neduchal/ros_ws/ && colcon build && . ./install/local_setup.bash

#RUN ls opt/uwb_ntis

#RUN ls $OPT_PATH/robot_system_core






