FROM osrf/ros:foxy-desktop

# Zkusit https://robots.uc3m.es/installation-guides/install-realsense2.html instalaci z buildu.

ARG OPT_PATH=/home/neduchal/

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






