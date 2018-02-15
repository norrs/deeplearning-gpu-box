
```python
# Installing latest Nvidia drivers and running awesome CUDA / CUD DNN (deep neural network) using Docker
```

# Pre-requeistostinsonticies

apt install curl

# Nvidia driver

sudo add-apt-repository ppa:graphics-drivers/ppa
apt install nvidia-390-dev

(nvidia-xconfig / nvidia-settings)
cool-bits=1 enables the possibility of overclocking
cool-bits=4 includes the ability to manually control the fan
cool-bits=5 includes both

Verify by issuing

nvidia-smi    

Nvidia SMI is like the GPU's varaint of ps. 

# Install docker

https://docs.docker.com/install/linux/docker-ce/ubuntu/

apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
    
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo apt-key fingerprint 0EBFCD88

pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22


$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
   
apt update

apt install docker-ce

# Nvidia docker 

https://github.com/NVIDIA/nvidia-docker install notes below copied from this webpage. If you are keen enough and don't want to bother with nvidia docker, read notes on https://hub.docker.com/r/gw000/debian-cuda/ which explains and shows what exactly nvidia-docker is doing by mounting nvidia drivers and hardware devices (/dev) into the container. 


# # If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU containers
docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
sudo apt-get purge -y nvidia-docker

## Add the package repositories
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/ubuntu16.04/amd64/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update

## Install nvidia-docker2 and reload the Docker daemon configuration
sudo apt-get install -y nvidia-docker2
sudo pkill -SIGHUP dockerd

## Test nvidia-smi with the latest official CUDA image
docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi



apt install nvidia-390-dev



