# A Minimal Docker Environment for Unitree RL Lab

This repository provides a virtual environment to train Unitree's robots with IsaacLab.

The container `unitree_rl_u22_cuda12_6_3` involves:

- Ubuntu 22.04
- CUDA 12.6.3
- Python 3.11
- PyTorch 2.7.0 (compatible with NVIDIA Blackwell architecture)
- IsaacSim 5.1.0
- IsaacLab 2.3.2 (latest)

To fix Python and pip dependencies, the virtual environment utilises miniconda inside the Docker image. If you know a smarter way, please let the maintainer know!

## Prerequisites

### nvidia-driver

> [!NOTE]
> The `nvidia-driver` version recommended by `ubuntu-drivers devices` is a good choice.
> 
> In addition, the version **580.65.06 or later** is recommended for IsaacLab at this time.

- Docker

Follow [the official document](https://docs.docker.com/engine/install/ubuntu/).

> [!NOTE]
> As Docker installed from snap may not be compatible with GPU, we recommend using docker from apt.

- Docker Compose

Follow [the official documents](https://docs.docker.com/compose/install/linux/).


- NVIDIA Container Toolkit

Follow [the official documents](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html).

## Installation

### Clone (Host)

```bash
git clone https://github.com/ssr-yuki/docker_unitree_rl_lab.git
```

```bash
mkdir -p rl_ws/src

git clone https://github.com/isaac-sim/IsaacLab.git
git clone https://github.com/unitreerobotics/unitree_rl_lab.git
git clone https://github.com/unitreerobotics/unitree_ros.git
```

## Start Container (Host)

> [!NOTE]
> For the first time, it will take some time to build the container.


```bash
docker compose up -d
```

For build only:

```bash
docker compose build
```

## Development

### Enter Container (Host)

```bash
xhost +local:
docker exec -it unitree_rl_u22_cuda12_6_3 bash
```

### Run (Container)

```bash
conda activate unitree_lab
cd src/unitree_rl_lab/
```

and start your training with [unitree_rl_lab](https://github.com/unitreerobotics/unitree_rl_lab)!

## Acknowledgement

- The base of this repository is [choreonoid_ros2_dev_env](https://github.com/choreonoid/choreonoid_ros2_dev_env) developed by [HansRobo](https://github.com/HansRobo).
- Activation of the miniconda environment in `docker compose build` is realised by [this post](https://www8281uo.sakura.ne.jp/blog/?p=890).
