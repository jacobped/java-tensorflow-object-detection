############################################################
# Dockerfile for improved TensorFlow container for Object Detection
# Makes the training process easier with all dependencies already applied
############################################################

#FROM tensorflow/tensorflow:latest-devel
#FROM tensorflow/tensorflow:1.9.0-rc1-devel
FROM tensorflow/tensorflow:1.8.0-devel

ARG BUILD_DATE
ARG VCS_REF

MAINTAINER jacobpeddk
LABEL maintainer="jacobpeddk"
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-url="https://github.com/jacobped/java-tensorflow-object-detection"
LABEL org.label-schema.vcs-ref=$VCS_REF

ENV DEBIAN_FRONTEND noninteractive
ENV RUNLEVEL 1

# Retrieve TensorFlow Research projects
WORKDIR /setup/tensorflow-research
RUN git clone --branch=master https://github.com/tensorflow/models.git . && \ 
    git reset --hard bc0edaf8ec635c2a493a9303071e3d2fe97f3b7b && \
    mkdir -p /tensorflow/tensorflow/models && \
    cp -r research /tensorflow/tensorflow/models/ && \
    cd .. && \
    rm -fr tensorflow-research

# Add Repo with newer protobuf packages
RUN add-apt-repository -y ppa:maarten-fonville/protobuf

# Update packagelist and install dependencies
#RUN apt-get update -y && apt-get install -y apt-utils
RUN apt-get update -y && apt-get install -y \
    protobuf-compiler \
    python-pil \
    python-lxml \
    python-tk \
    cython \
    vim \
    less && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install extra python dependencies with pip
RUN pip --no-cache-dir install \
        Cython \
        pillow \
        lxml \
        jupyter \
        matplotlib

# Fix COCO API and dependencies
WORKDIR /setup/coco
COPY scripts/coco-fix.sh coco-fix.sh
RUN chown root:root coco-fix.sh
RUN chmod -f 555 coco-fix.sh
RUN ./coco-fix.sh

# export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim
ENV PYTHONPATH $PYTHONPATH:`pwd`:`pwd`/slim

# Setting up TensorFlow Research projekt
WORKDIR /tensorflow/tensorflow/models/research
RUN python setup.py build && \
    python setup.py install

WORKDIR slim
RUN pip install -e .

# Validate setup
WORKDIR /tensorflow/tensorflow/models/research/object_detection/builders
RUN python model_builder_test.py

# Clean up APT
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /root/sharedfolder

# Jupyter notebook
EXPOSE 8888/tcp
# TensorBoard
EXPOSE 6006/tcp
