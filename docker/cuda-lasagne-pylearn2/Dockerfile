# Start with CUDA Lasagne + OpenCV base image
FROM animoid/cuda-lasagne-opencv:latest
MAINTAINER David Jung <david@egomachines.com>

## PyLearn2

RUN apt-get update && apt-get install -y \
  curl \
  cython \
  python-imaging \
  python-yaml \
  python-PIL
#  python-matplotlib \

# Install matplotlib via pip to use our /usr/local/lib version of 
#  numpy rather than pulling in older distro python-numpy into /usr/lib

RUN pip install matplotlib


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
