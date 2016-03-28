# Start with official NVidia CUDA base image
FROM nvidia/cuda:latest
MAINTAINER David Jung <david@egomachines.com>
#  based on Dockerfiles by Kai Arulkumaran - https://github.com/Kaixhin/dockerfiles

RUN apt-get update
RUN apt-get install -y wget

# Install CUDA repo (needed for cuDNN)
ENV CUDA_REPO_PKG=cuda-repo-ubuntu1404_7.5-18_amd64.deb
RUN wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1404/x86_64/$CUDA_REPO_PKG && \
  dpkg -i $CUDA_REPO_PKG

# Install cuDNN v4
ENV ML_REPO_PKG=nvidia-machine-learning-repo_4.0-2_amd64.deb
RUN wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1404/x86_64/$ML_REPO_PKG && \
  dpkg -i $ML_REPO_PKG && \
  apt-get update && apt-get install -y libcudnn4 libcudnn4-dev
