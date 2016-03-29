# Start with CUDA Lasagne base image
FROM animoid/cuda-lasagne:latest
MAINTAINER David Jung <david@egomachines.com>

## OpenCV 3.1

RUN sudo apt-get update && apt-get install -y build-essential \
    cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev \
    python-dev libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev unzip \
&& apt-get clean

RUN wget https://github.com/Itseez/opencv/archive/3.1.0.zip -O opencv-3.1.0.zip \
 && unzip opencv-3.1.0.zip \
 && cd opencv-3.1.0 \
 && mkdir build \
 && cd build \
 && cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local .. \
 && make -j$((`expr \`nproc\`-1`))
# && make -j7

## PyLearn2

RUN sudo apt-get update && apt-get install -y python-PIL
RUN sudo pip install Pillow six

RUN git clone git://github.com/lisa-lab/pylearn2.git \
 && cd pylearn2 \
 && sudo python setup.py develop \
 && cat "export PYLEARN2_DATA_PATH=/data/lisa/data" >> ~/.bashrc
