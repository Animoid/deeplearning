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

RUN apt-get update && apt-get install -y \
  curl \
  cython \
  python-imaging \
  python-matplotlib \
  python-yaml \
  python-PIL

# Upgrade six
RUN pip install --upgrade six

# Clone Pylearn2 repo and move into it
RUN cd /root && git clone https://github.com/lisa-lab/pylearn2.git && cd pylearn2 && \
  # Install
  python setup.py develop

# Make and set data directory
RUN mkdir /data
ENV PYLEARN2_DATA_PATH=/data
VOLUME /data
