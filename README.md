# LIO-SAM NVIDIA GPU Docker Support

**[LIO-SAM github link](https://github.com/TixiaoShan/LIO-SAM)**

This repository includes a modified Dockerfile and run commands to ensure LIO-SAM can run on systems with NVIDIA GPUs without encountering `libGL` errors in the Docker environment.

## Prerequisites
To use this Docker setup, you need to install the `nvidia-container-toolkit`. Follow the installation instructions provided by NVIDIA [here](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html).

## Modifications
- The Dockerfile has been adjusted to avoid `libGL` errors that may occur when running LIO-SAM in a Docker environment with an NVIDIA GPU.
- Run commands have been updated to ensure proper functionality on systems with NVIDIA GPUs.

## Testing Environment
- **OS**: Ubuntu 22.04
- **GPU**: NVIDIA GeForce RTX 4060 Ti

This setup has been tested on the above environment and confirmed to work correctly.


## Docker

```bash
docker build -t liosam-kinetic-xenial .
```

Once you have the image, start a container as follows:

```bash
docker run --init -it -d \
  --runtime=nvidia --gpus all \
  -v /etc/localtime:/etc/localtime:ro \
  -v /etc/timezone:/etc/timezone:ro \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -e DISPLAY=$DISPLAY \
  -e "QT_X11_NO_MITSHM=1" \
  liosam-kinetic-xenial
  bash
```