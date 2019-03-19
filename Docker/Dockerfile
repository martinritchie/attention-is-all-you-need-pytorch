# get docker ubuntu image that has GPU access
FROM nvidia/cuda:9.2-cudnn7-runtime-ubuntu16.04

# Install basic utilities
RUN apt-get update && \
    apt-get install -y --no-install-recommends git wget ffmpeg unzip bzip2 sudo build-essential && \
    apt-get install -y python3-pip locales && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set encoding environment.
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# args for miniconda setup
ARG PYTHON_VERSION=3.6
ARG CONDA_PYTHON_VERSION=3
ARG CONDA_DIR=/opt/conda

# Install miniconda
ENV PATH $CONDA_DIR/bin:$PATH
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.5.12-Linux-x86_64.sh -O /tmp/miniconda.sh && \
    echo 'export PATH=$CONDA_DIR/bin:$PATH' > /etc/profile.d/conda.sh && \
    /bin/bash /tmp/miniconda.sh -b -p $CONDA_DIR && \
    rm -rf /tmp/* && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*


# RUN conda info tensorflow-gpu
RUN conda install pip && conda install -c anaconda tensorflow-gpu=1.12.0
RUN conda install pytorch torchvision cuda92 -c pytorch
ADD requirements.txt /usr/local/requirements.txt
RUN pip install -r /usr/local/requirements.txt
