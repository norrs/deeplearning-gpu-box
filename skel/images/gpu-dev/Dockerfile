# Base image is Tensorflow with CUDA + cuDNN
FROM tensorflow/tensorflow:latest-devel-gpu-py3

# https://hub.docker.com/r/igorbb/gpu-dev/~/dockerfile/
LABEL maintainer "Igor Barros Barbosa"
LABEL maintainer "Roy Sindre Norangshol"

# Install LLVM dependencies and repo
RUN echo 'deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-4.0 main' \
    >/etc/apt/sources.list.d/llvm.list
RUN echo 'deb-src http://apt.llvm.org/xenial/ llvm-toolchain-xenial-4.0 main' \
    >>/etc/apt/sources.list.d/llvm.list
RUN curl http://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -


# Install basic programs and dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    htop \
    byobu \
    git \
    nano \
    vim \
    rsync \
    unzip \
    clang-4.0 \
    locales

# Set correct locale for locale-aware programs or libraries
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


# Setup Numba Env
ENV LLVM_CONFIG=/usr/bin/llvm-config-5.0
ENV NUMBAPRO_LIBDEVICE /usr/local/cuda-8.0/nvvm/libdevice
ENV NUMBAPRO_NVVM /usr/local/cuda-8.0/nvvm/lib64/libnvvm.so

# Install basic packages and miscellaneous dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    liblapack-dev \
    libopenblas-dev \
    python3-tk \
    libfreetype6-dev \
    liblcms2-dev \
    libwebp-dev \
    zlib1g-dev \
    libhdf5-dev

RUN DEBIAN_FRONTEND=noninteractive apt-get build-dep -y python-opencv

# Upgrade pip and setuptools
RUN pip3 install --upgrade \
    setuptools \
    pip \
    wheel

# Install basic Python packages (some of these may already be installed)
RUN pip3 install \
    six \
    ipython \
    jupyter \
    ipdb \
    ujson \
    numpy \
    Pillow \
    scipy \
    matplotlib \
    tqdm \
    seaborn \
    statsmodels \
    h5py \
    PyYAML \
    pandas \
    scikit-learn \
    opencv-python 
RUN pip3 install --upgrade \
    scikit-image \
    numba \
    git+git://github.com/Lasagne/Lasagne.git@$master \
    git+git://github.com/fchollet/keras.git@$master \
    git+git://github.com/vicolab/ml-pyxis.git@$master

# Prepare matplotlib font cache
RUN python3 -c "import matplotlib.pyplot"

# Set up directories in /root
RUN mkdir /root/shared && \
mkdir /root/data && \
mkdir /root/.misc && \
mkdir -p -m 700 /root/.local/share/jupyter

# Add alias to `.bash_aliases` so that `python` runs `python3`
RUN echo "alias python=python3"  >> /root/.bash_aliases
RUN echo "alias run_notebook='jupyter notebook --no-browser --allow-root'"  >> /root/.bash_aliases

# Expose port for IPython (8888)
EXPOSE 8888

# Expose port for TensorBoard (6006)
EXPOSE 6006

# Set default working directory and image startup command
WORKDIR "/root"
CMD ["/bin/bash"]

