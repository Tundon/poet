# Dockerfile for PoET

## Setup Docker

1. Docker needs to have nvidia container toolkit [setup](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)
2. Set the default container runtime to be `nvidia`, file "/etc/docker/daemon.json"
    ```json
    {
      "runtimes": {
        "nvidia": {
          "args": [],
          "path": "nvidia-container-runtime"
        }
      },
      "default-runtime": "nvidia"
    }
    ```
## Build

`DOCKER_BUILDKIT=0 docker build -t teabots/poet -f docker/Dockerfile .`

## ==> DEPRECATED

This directory contains the Dockerfile for PoET. As the Deformable Attention module is by default not part of Pytorch, the module needs to be downloaded and build from scratch within the Docker container. Therefore, download the [module from the Deformable-DETR repository](https://github.com/fundamentalvision/Deformable-DETR/tree/main/models/ops).

## Docker Setup
```
# Build the Docker image
docker build -t aaucns/poet:base .

# Run the container
docker run -it --rm --name poet --gpus all aaucns/poet:base

# From a different terminal copy the previously downloaded deform_attn into the Docker container
docker cp /path/to/deform_attn poet:/deform_attn

# Inside the Docker container switch to the directory and install the module
cd /deform_attn
sh ./make.sh

# Test if the installation worked
python test.py

# Alternatively
python -c 'import deformable_attention; print(True)'

# Store the current Dokcer container as new image from a different terminal

docker commit poet aaucns/poet:latest
```

Following these steps results in the same docker image as provided with the following download command:

```
docker pull aaucns/poet:latest
```