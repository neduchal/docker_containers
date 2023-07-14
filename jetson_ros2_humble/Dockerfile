FROM arm64v8/ros:humble-ros-base

ARG OPT_PATH=/home/lampone

RUN echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections

RUN sudo apt-get install -y -q

RUN lsb_release -a

RUN sudo apt-get -y update && sudo apt-get -y install git

RUN mkdir -p $OPT_PATH/ws/src 

RUN ls

RUN cd $OPT_PATH/ws/src && git clone https://github.com/neduchal/lampone23_server.git lampone23_server

RUN /bin/bash ./opt/ros/humble/setup.bash  && cd $OPT_PATH/ws && colcon build

RUN apt install nano

RUN cp ros_entrypoint.sh ros_entrypoint.sh.txt && sed '$ d' /ros_entrypoint.sh.txt > /ros_entrypoint.sh && rm -f /ros_entrypoint.sh.txt 

RUN echo "source \"/home/lampone/ws/install/setup.bash\" --" >> /ros_entrypoint.sh

RUN echo "exec \"\$@\"" >> /ros_entrypoint.sh


