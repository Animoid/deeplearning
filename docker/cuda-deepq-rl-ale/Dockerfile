# Start with CUDA Lasagne base image
FROM animoid/cuda-lasagne-pylearn2:latest
MAINTAINER David Jung <david@egomachines.com>

# Arcade Learning Environment (ALE)

RUN sudo apt-get update && apt-get install -y libsdl1.2-dev libsdl-gfx1.2-dev libsdl-image1.2-dev cmake

RUN cd ~ && git clone https://github.com/mgbellemare/Arcade-Learning-Environment ALE \
 && cd ~/ALE \
 && cmake -DUSE_SDL=ON -DUSE_RLGLUE=OFF . \
 && make -j2

RUN cd ~/ALE && pip install .


# deepq-rl

RUN cd ~ && git clone https://github.com/spragunr/deep_q_rl.git

