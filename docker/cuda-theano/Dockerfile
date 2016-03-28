# Start with cuDNN base image
FROM animoid/cudnn:latest
MAINTAINER David Jung <david@egomachines.com>
#  based on Dockerfiles by Kai Arulkumaran

# Install git, python-dev, pip and other dependencies
RUN apt-get update && apt-get install -y \
  git \
  libopenblas-dev \
  python-dev \
  python-pip \
  python-nose \
  python-numpy \
  python-scipy

# Set CUDA_ROOT
ENV CUDA_ROOT /usr/local/cuda/bin
# Install bleeding-edge Theano
RUN pip install --upgrade --no-deps git+git://github.com/Theano/Theano.git
# Set up .theanorc for CUDA
RUN echo "[global]\ndevice=gpu\nfloatX=float32\noptimizer_including=cudnn[lib]\ncnmem=1\n[nvcc]\nfastmath=True" > /root/.theanorc