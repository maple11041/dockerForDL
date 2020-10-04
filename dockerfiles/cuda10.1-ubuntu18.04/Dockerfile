FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04
ENV LANG C.UTF-8
RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    rm -rf /var/lib/apt/lists/* \
           /etc/apt/sources.list.d/cuda.list \
           /etc/apt/sources.list.d/nvidia-ml.list && \

    apt-get update && \
    $APT_INSTALL \
    build-essential \
    apt-utils \
    ca-certificates \
    wget \
    git \
    vim \
    libssl-dev \
    curl \
    unzip \
    unrar \
    tmux \
    htop \
    && \

    git clone --depth 10 https://github.com/Kitware/CMake ~/cmake && \
    cd ~/cmake && \
    ./bootstrap && \
    make -j"$(nproc)" install && \
# python

    $APT_INSTALL \
    software-properties-common && \ 
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    $APT_INSTALL \
    python3.7 \
    python3.7-dev \
    python3-distutils-extra \
    && \
    wget -O ~/get-pip.py \
        https://bootstrap.pypa.io/get-pip.py && \
    python3.7 ~/get-pip.py && \
    ln -s /usr/bin/python3.7 /usr/local/bin/python3 && \
    ln -s /usr/bin/python3.7 /usr/local/bin/python && \
    $PIP_INSTALL \
        setuptools \
        && \
    $PIP_INSTALL \
        numpy \
        scipy \
        pandas \
        cloudpickle \
        scikit-image \
        scikit-learn \
        matplotlib \
        Cython \
        tqdm \
        && \

# pytorch

    $PIP_INSTALL \
    torch==1.6.0 \
    torchvision==0.7.0 && \

# tensorflow
    $PIP_INSTALL \
    tensorflow-gpu && \

# keras
    $PIP_INSTALL \
    keras && \

# jupyter
    $PIP_INSTALL \
    jupyterlab

# clean up
    ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/*
