ARG PYTORCH="1.13.0"
ARG CUDA="11.6"
ARG CUDNN="8"

FROM pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel

ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0 7.5 8.0 8.6+PTX" \
    TORCH_NVCC_FLAGS="-Xfatbin -compress-all" \
    CMAKE_PREFIX_PATH="$(dirname $(which conda))/../" \
    FORCE_CUDA="1"

# Avoid Public GPG key error
# https://github.com/NVIDIA/nvidia-docker/issues/1631
RUN rm /etc/apt/sources.list.d/cuda.list \
    #&& rm /etc/apt/sources.list.d/nvidia-ml.list \
    && apt-key del 7fa2af80 \
    && apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub \
    && apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/7fa2af80.pub

# (Optional, use Mirror to speed up downloads)
# RUN sed -i 's/http:\/\/archive.ubuntu.com\/ubuntu\//http:\/\/mirrors.aliyun.com\/ubuntu\//g' /etc/apt/sources.list && \
#    pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# Install the required packages
RUN apt-get update \
    && apt-get install -y ffmpeg libsm6 libxext6 git ninja-build libglib2.0-0 libsm6 libxrender-dev libxext6 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install MMEngine and MMCV
RUN pip install openmim && \
    mim install "mmengine==0.8.4" "mmcv-full==1.7.0"

# Install MMDetection
RUN conda clean --all \
    && git clone https://github.com/open-mmlab/mmdetection.git /mmdetection && cd /mmdetection && git checkout v2.26.0 \
    && cd /mmdetection \
    && pip install --no-cache-dir -e .

RUN pip install onnx onnxruntime-gpu==1.15.0

RUN apt-get update && apt-get install -y mc htop nano

RUN mkdir -p /home/jetson/

WORKDIR /home/jetson/

# RUN mkdir ./miniconda3
# RUN wget https://repo.anaconda.com/miniconda/Miniconda3-py39_23.5.2-0-Linux-x86_64.sh -O ./miniconda3/miniconda.sh
# RUN bash ./miniconda3/miniconda.sh -b -u -p /home/jetson/miniconda3
# RUN rm -rf ./miniconda3/miniconda.sh
# RUN ./miniconda3/bin/conda bash
# RUN conda create -n mmdeploy python=3.9 -y
RUN pip install openmim
RUN apt install -y wget
RUN wget https://github.com/microsoft/onnxruntime/releases/download/v1.15.0/onnxruntime-linux-x64-1.15.0.tgz
RUN tar -zxvf onnxruntime-linux-x64-1.15.0.tgz
RUN cd onnxruntime-linux-x64-1.15.0 && export ONNXRUNTIME_DIR=$(pwd)

RUN git clone https://github.com/open-mmlab/mmdeploy.git
WORKDIR /home/jetson/mmdeploy
RUN git checkout v0.14.0
RUN export MMDEPLOY_DIR=/home/jetson/mmdeploy
RUN export LD_LIBRARY_PATH=/home/jetson/onnxruntime-linux-x64-1.16.0/lib:$LD_LIBRARY_PATH && export MMDEPLOY_DIR=/home/jetson/mmdeploy && mkdir -p build && cd build && cmake -DCMAKE_CXX_COMPILER=g++-7 -DMMDEPLOY_TARGET_BACKENDS=ort -DONNXRUNTIME_DIR=/home/jetson/onnxruntime-linux-x64-1.15.0/ .. && make -j12 && make install
RUN mim install -e .

WORKDIR /home/jetson
RUN wget https://developer.nvidia.com/downloads/compute/machine-learning/tensorrt/secure/8.6.0/tars/TensorRT-8.6.0.12.Linux.x86_64-gnu.cuda-11.8.tar.gz
RUN tar -zxvf TensorRT-8.6.0.12.Linux.x86_64-gnu.cuda-11.8.tar.gz
RUN cd TensorRT-8.6.0.12/python && ls -la
RUN export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/jetson/TensorRT-8.6.0.12/lib && cd TensorRT-8.6.0.12/python && ls -la && python3 -m pip install tensorrt-8.6.0-cp39-none-linux_x86_64.whl
RUN export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/jetson/TensorRT-8.6.0.12/lib && cd TensorRT-8.6.0.12/graphsurgeon && python3 -m pip install graphsurgeon-0.4.6-py2.py3-none-any.whl 
RUN export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/jetson/TensorRT-8.6.0.12/lib && cd TensorRT-8.6.0.12/onnx_graphsurgeon && python3 -m pip install onnx_graphsurgeon-0.3.12-py2.py3-none-any.whl

WORKDIR /home/jetson

