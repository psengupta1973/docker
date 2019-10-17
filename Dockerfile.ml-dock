FROM ubuntu:18.04

# Adds metadata to the image as a key value pair example LABEL version="1.0"
LABEL maintainer="Partha Sarathi Sengupta <Partha.Sarathi.Sengupta@ericsson.com>"

# Set environment variables
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive

# Create empty directory to attach volume
RUN mkdir /home/work && \
    mkdir /home/work/code && \
    mkdir /home/work/model && \
    mkdir /home/work/input && \
    mkdir /home/work/output

# Install Ubuntu packages
RUN apt-get update && apt-get install -y \
    wget \
    bzip2 \
    ca-certificates \
    build-essential \
    curl \
    git-core \
    htop \
    pkg-config \
    unzip \
    unrar \
    tree \
#    openmpi-bin \
    freetds-dev \
    libprotobuf-dev \
    libleveldb-dev \
    libsnappy-dev \
    libhdf5-serial-dev \
    protobuf-compiler \
    libopencv-dev

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Anaconda3-4
RUN curl -sSL -o installer.sh https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh && \
    bash /installer.sh -b -f && \
    rm /installer.sh
    
ENV PATH "$PATH:/root/anaconda3/bin"
ENV PATH /opt/conda/bin:$PATH

# Update conda and install other utilities and ML frameworks
#RUN conda update -n base -c defaults conda
RUN conda clean -tipsy && \
    conda install ipykernel && \
    conda install ipython && \
    conda install jupyter_client && \
    conda install jupyter_core && \
    conda install traitlets && \
    conda install ipython_genutils && \
    conda install tensorflow && \
    conda install pytorch-cpu torchvision-cpu -c pytorch && \
    conda install keras
RUN pip install --upgrade pip
# install tensorflow 2.0
RUN pip install -U --pre tensorflow
RUN pip install mxnet
RUN pip install cntk
RUN pip install chainer

EXPOSE 8888
#VOLUME /home/work
WORKDIR /home/work/
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=*"]

#ENTRYPOINT ["/bin/bash"]
