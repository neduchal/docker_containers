FROM nvcr.io/nvidia/l4t-pytorch:r32.7.1-pth1.10-py3
#FROM nvcr.io/nvidia/l4t-cuda:12.2.12-runtime
# RUN echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections

RUN wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | tee /usr/share/keyrings/kitware-archive-keyring.gpg >/dev/null \
    && echo 'deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ bionic main' | tee /etc/apt/sources.list.d/kitware.list >/dev/null

RUN apt-get install -y -q

RUN apt-get -y update && apt-get -y upgrade && apt-get -y dist-upgrade && apt-get -y install git


#RUN pip3 install bson

#WORKDIR /home/exon/

#RUN pip3 install Pillow==7.1

#RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
#    dpkg-reconfigure --frontend=noninteractive locales && \
#    update-locale LANG=en_US.UTF-8
#ENV LANG en_US.UTF-8
#RUN pip3 install scikit-image==0.17.1 -vv

#RUN git clone --branch v0.6 https://github.com/facebookresearch/detectron2.git
#RUN python3 -m pip install -e detectron2

#RUN pip3 uninstall -y bson
#RUN pip3 install pymongo

#RUN pip3 install psutil
#RUN pip3 install gputil

# RUN mkdir /home/exon && cd /home/exon && git clone -b v0.11.1 https://github.com/pytorch/vision.git

# RUN sudo apt-get -y install curl zip unzip tar

# RUN sudo apt install -y dbus-x11
