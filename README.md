# Object Detection with TensorFlow and Java
[![Docker Pulls](https://img.shields.io/docker/pulls/jacobpeddk/tensorflow-improved.svg)](https://hub.docker.com/r/jacobpeddk/tensorflow-improved)
[![Docker Stars](https://img.shields.io/docker/stars/jacobpeddk/tensorflow-improved.svg)](https://hub.docker.com/r/jacobpeddk/tensorflow-improved)

I've gone trough a lot of trouble for figuring out how to both prepare a dataset, train a model with TensorFlow, and how to use it from a Java program.  
So from all my effort, this repository contains somewhat detailed guides on how you can train your own model.

With this I've located and modified a few scripts to make th training simpler. I've also created customized Docker containers that is based on the official TensorFlow containers, but comes with a bunch of fixes and the needed research project files.
Without these, it simply not possible to get any of this stuff to work properly.  
I've also created an easy to use java library, that you can use from your own applications.

By packing it all into new Docker containers, everything works the same every time, and it's a lot easier to train the models this way.

I've also created an easy to use java library, that you can use from your own applications.

This entire project was done to make it possible to detect and locate the exact positions of subtitles in videos.

## [Object Detection Guide](training/training-object-detection.md)
You can find the fairly detailed guide on how to prepare a dataset and train a model for Object Detection in [the training folder.](training)

## [Docker containers](docker)
Information about the customized containers, can be found in [the folder named docker.](docker)

### CPU Container
[![](https://images.microbadger.com/badges/image/jacobpeddk/tensorflow-improved.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Container Image size and layers")
[![](https://images.microbadger.com/badges/commit/jacobpeddk/tensorflow-improved.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Current commit that the container is build from")
[![](https://images.microbadger.com/badges/version/jacobpeddk/tensorflow-improved.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Container version")

### GPU Container
[![](https://images.microbadger.com/badges/image/jacobpeddk/tensorflow-improved:latest-gpu.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Container Image size and layers")
[![](https://images.microbadger.com/badges/commit/jacobpeddk/tensorflow-improved:latest-gpu.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Current commit that the container is build from")
[![](https://images.microbadger.com/badges/version/jacobpeddk/tensorflow-improved:latest-gpu.svg)](https://microbadger.com/images/jacobpeddk/tensorflow-improved "Container version")
