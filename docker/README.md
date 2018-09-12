# Docker containers for TensorFlow Object-Detection
[![Docker Pulls](https://img.shields.io/docker/pulls/jacobpeddk/tensorflow-improved.svg)](https://hub.docker.com/r/jacobpeddk/tensorflow-improved)
[![Docker Stars](https://img.shields.io/docker/stars/jacobpeddk/tensorflow-improved.svg)](https://hub.docker.com/r/jacobpeddk/tensorflow-improved)

TensorFlow Docker containers with Improvements and fixes for training Objekt Detection models.  
Can also be used to train models for classification of entire images.


Prebuilt containers can be retrieved from here:  
https://hub.docker.com/r/jacobpeddk/tensorflow-improved/

Information abut the TensorFlow containers, which these containers is based on, can be seen at the following location:  
https://hub.docker.com/r/tensorflow/tensorflow/  
https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/docker/README.md

## Usage
I'd recommend mapping a directory into the containers, so you can have the training data and results saved on the host machine.  
This and related documents will expect the host folder with the data to be mapped to: `/root/sharedfolder`  

### CPU container
[![](https://images.microbadger.com/badges/image/jacobpeddk/tensorflow-improved.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Container Image size and layers")
[![](https://images.microbadger.com/badges/commit/jacobpeddk/tensorflow-improved.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Current commit that the container is build from")
[![](https://images.microbadger.com/badges/version/jacobpeddk/tensorflow-improved.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Container version")

For launching the container that uses the CPU for training, use the following command:
```
docker run --rm -it -p 8888:8888 -p 6006:6006 -v <host path>:/root/sharedfolder:Z tensorflow-improved:latest
```

**Remember to replace \<host path\> with the actual path on your host machine!**  
Example:
```
docker run --rm -it -p 8888:8888 -p 6006:6006 -v /home/jacob/andet/training/docker-training-shared:/root/sharedfolder:Z tensorflow-improved:latest
```

### GPU container
[![](https://images.microbadger.com/badges/image/jacobpeddk/tensorflow-improved:latest-gpu.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Container Image size and layers")
[![](https://images.microbadger.com/badges/commit/jacobpeddk/tensorflow-improved:latest-gpu.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Current commit that the container is build from")
[![](https://images.microbadger.com/badges/version/jacobpeddk/tensorflow-improved:latest-gpu.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Container version")

For launching the container that uses the GPU for training, use the following command:
```
nvidia-docker run --rm -it -p 8888:8888 -p 6006:6006 -v <host path>:/root/sharedfolder:Z tensorflow-improved:latest-gpu
```
For an Optimus laptop that's using Bumblebee, you can use above command after optirun. Example:
```
optirun nvidia-docker run --rm -it -p 8888:8888 -p 6006:6006 -v <host path>:/root/sharedfolder:Z tensorflow-improved:latest-gpu
```

**Remember to replace \<host path> with the actual path on your host machine!**  
Example:
```
nvidia-docker run --rm -it -p 8888:8888 -p 6006:6006 -v /home/jacob/andet/training/docker-training-shared:/root/sharedfolder:Z tensorflow-improved:latest-gpu
```

**Be aware!** GPU training is a lot faster than CPU, but it requires a Nvidia GPU and *Nvidia Cuda* to be installed and working on the host machine.
It also requires the host to have *NVIDIA Container Runtime for Docker* installed.  
You can read more about it here: https://github.com/NVIDIA/nvidia-docker  
You can test if it's working by running the following test container with the command below. If it doesn't throw an error, you're golden.
```
nvidia-docker run --rm nvidia/cuda nvidia-smi
```

### Ports
Port 8888 is used for jupyter notebook, which is a fairly cool web based teaching tool that's part of the TensorFlow containers.
Port 6006is used for TensorFlow Tensorboard websitet, where one can evaluate the training process.

## Build containers

### CPU
```
docker build -t tensorflow-improved -f Dockerfile .
```

### GPU
```
docker build -t tensorflow-improved-gpu -f Dockerfile.gpu .
```
