# Installing-CUDA-Toolkit-cuDNN-OpenCV-and-PyTorch-on-Ubuntu-20.04
This repository is tested with NVIDIA GeForce GTX 1080 and NVIDIA RTX 3060 Ti on Ubuntu 20.04 LTS. 
The CUDA toolkit with your NVIDIA GPU can be a great tool that can harness the power of GPU to produce fast applications. Though, it is always challenging to install a CUDA toolkit and other libraries that needs to interact with your NVIDIA GPU on an Ubuntu machine. This repository will help you install and test the GPU processing. 


### INSTALLATION PROCEDURE

#### 1. CONFIGURATION
- Running the following commands to setup Ubuntu.
```
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get install -y build-essential cmake unzip pkg-config
sudo apt-get install -y libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev
sudo apt-get install -y libjpeg-dev libpng-dev libtiff-dev
sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install -y libxvidcore-dev libx264-dev
sudo apt-get install -y libgtk-3-dev
sudo apt-get install -y libopenblas-dev libatlas-base-dev liblapack-dev gfortran
sudo apt-get install -y libhdf5-serial-dev graphviz
sudo apt-get install -y python3-dev python3-tk python-imaging-tk
sudo apt-get install -y linux-image-generic linux-image-extra-virtual
sudo apt-get install -y linux-source linux-headers-generic
```
