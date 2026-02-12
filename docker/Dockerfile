FROM nvidia/cuda:12.6.3-devel-ubuntu22.04

RUN mkdir -p /root/miniconda3

RUN apt-get update && apt-get install -y wget libxml2-dev libgl1-mesa-dev libglu1-mesa libxt-dev
# For IsaacLab
RUN apt-get install -y cmake build-essential curl git
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /root/miniconda3/miniconda.sh
RUN bash /root/miniconda3/miniconda.sh -b -u -p /root/miniconda3
RUN rm /root/miniconda3/miniconda.sh

RUN /root/miniconda3/bin/conda init --all
RUN /root/miniconda3/bin/conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
RUN /root/miniconda3/bin/conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r
RUN /root/miniconda3/bin/conda create -n unitree_lab python=3.11

SHELL ["/bin/bash", "-i", "-c"]

RUN <<EOF
set -xe
conda activate unitree_lab
pip install --upgrade pip
pip install "isaacsim[all,extscache]==5.1.0" --extra-index-url https://pypi.nvidia.com
pip install -U torch==2.7.0 torchvision==0.22.0 --index-url https://download.pytorch.org/whl/cu128

curl https://raw.githubusercontent.com/isaac-sim/IsaacLab/refs/heads/main/isaaclab.sh -o isaaclab.sh
/bin/sh isaaclab.sh --install

conda deactivate
EOF

COPY docker/.bash_history /root/.bash_history

WORKDIR /root/rl_ws
