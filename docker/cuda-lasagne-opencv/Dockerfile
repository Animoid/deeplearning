# Start with CUDA Lasagne base image
FROM animoid/cuda-lasagne:latest
MAINTAINER David Jung <david@egomachines.com>

## OpenCV 3.1

RUN sudo apt-get update && apt-get install -y build-essential \
    cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev \
    libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev libgtk2.0-dev \
    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
    libtbb2 libtbb-dev libatlas-base-dev gfortran \
    python-dev libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev unzip \
&& sudo apt-get clean

# install cmake 3.2.x (work around issue in opencv install)
#  see: http://stackoverflow.com/questions/24174394/cmake-is-not-able-to-find-python-libraries
RUN sudo apt-get remove -y cmake \
    && apt-get install -y software-properties-common \
    && sudo add-apt-repository ppa:george-edison55/cmake-3.x \
    && sudo apt-get update -y \
    && sudo apt-get install -y cmake \
    && sudo apt-get clean


# Notes:
#  Numpy path assume it was installed into /usr/local/lib rather than the distribution path /usr/lib
#  Assumes Python 2.7

#RUN cd ~ && wget https://github.com/Itseez/opencv/archive/3.1.0.zip -O opencv-3.1.0.zip \
# && unzip opencv-3.1.0.zip \
# && cd opencv-3.1.0 \
# && mkdir build 

RUN cd ~ && git clone https://github.com/Itseez/opencv.git \
 && cd opencv \
 && git checkout 3.1.0

RUN cd ~ && git clone https://github.com/Itseez/opencv_contrib.git \
 && cd opencv_contrib \
 && git checkout 3.1.0

RUN cd ~/opencv \
 && mkdir build && cd build \
 && cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local -D PYTHON2_EXECUTABLE=`which python` \
    -D PYTHON_INCLUDE_DIR=/usr/include/python2.7 -D PYTHON_INCLUDE_DIR2=/usr/include/x86_64-linux-gnu/python2.7 \
    -D PYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython2.7.so -D PYTHON2_NUMPY_INCLUDE_DIRS=/usr/local/lib/python2.7/dist-packages/numpy/core/include \ 
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
    -D BUILD_opencv_world=OFF \
    -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=OFF .. \
 && make -j$((`expr \`nproc\`-1`))
# && make -j7

# unsure if these need to be redefined or not (seems to re-run configure step)
ENV PYTHON_LIBRARY /usr/lib/x86_64-linux-gnu/libpython2.7.so 
ENV PYTHON_INCLUDE_DIRS /usr/include/python2.7 
ENV PYTHON_INCLUDE_DIR /usr/include/python2.7 
ENV PYTHON_INCLUDE_DIR2 /usr/include/x86_64-linux-gnu/python2.7 
ENV PYTHON2_NUMPY_INCLUDE_DIRS /usr/local/lib/python2.7/dist-packages/numpy/core/include 
ENV OPENCV_EXTRA_MODULES_PATH ~/opencv_contrib/modules 
ENV INSTALL_PYTHON_EXAMPLES ON 
ENV BUILD_EXAMPLES OFF 
ENV BUILD_opencv_world OFF

RUN cd ~/opencv/build \
  && sudo make BUILD_opencv_world=OFF install

RUN sudo ldconfig

# cleanup
RUN cd ~/opencv/build \
  && make clean \
  && sudo apt-get autoclean
RUN rm -rf ~/opencv \
  && rm -rf ~/opencv_contrib


# Fix issue with libdc1394 error
#  see: http://stackoverflow.com/questions/12689304/ctypes-error-libdc1394-error-failed-to-initialize-libdc1394
CMD sh -c 'ln -s /dev/null /dev/raw1394'; /bin/bash
