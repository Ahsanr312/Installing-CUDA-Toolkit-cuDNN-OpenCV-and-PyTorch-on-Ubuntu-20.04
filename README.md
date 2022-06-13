# Installing-CUDA-Toolkit-cuDNN-OpenCV-and-PyTorch-on-Ubuntu-20.04
This repository is tested with NVIDIA GeForce GTX 1080 and NVIDIA RTX 3060 Ti on Ubuntu 20.04 LTS. 
The CUDA toolkit with your NVIDIA GPU can be a great tool that can harness the power of GPU to produce fast applications. Though, it is always challenging to install a CUDA toolkit and other libraries that needs to interact with your NVIDIA GPU on an Ubuntu machine. This repository will help you install and test the GPU processing. 


### INSTALLATION PROCEDURE

#### 01. CONFIGURATION
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

#### 02. NVIDIA Setup (Driver, CUDA, cuDNN)
##### A. Install NVIDIA Driver
- Remove existing Nvidia drivers if any
```
sudo apt-get purge nvidia*
```
- Add Graphic Drivers PPA
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```
- Search available drivers
```
ubuntu-drivers devices
```
- Install the driver with the best version
```
sudo apt-get install nvidia-driver-470
```
- Reboot your computer
```
reboot
```
- Check and verify GPU info
```
nvidia-smi
```

##### B. Install CUDA Toolkit 11.4.0
- Choose your CUDA Toolkit version from the link. Click the version you want to install and select your Target platform in terms of Operating System, 
Architecture, Distribution, Version and Installer Type. In my case "Linux -> x86_64 -> Ubuntu -> 20.04 -> deb (local)
```
https://developer.nvidia.com/cuda-toolkit-archive
```
- Installation Instructions:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.4.0/local_installers/cuda-repo-ubuntu2004-11-4-local_11.4.0-470.42.01-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-4-local_11.4.0-470.42.01-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu2004-11-4-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```
- Now set environment variables in the `~/.bashrc`.
```
sudo nano ~/.bashrc
```
- Add the following at the end of `~/.bashrc`
```
export PATH=/usr/local/cuda-11.4/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-11.4/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export CUDA_HOME=/usr/local/cuda
```

##### C. Install cuDNN
- Choose your cuDNN version from the link and make sure it is compatible with the CUDA version that you installed above. In my case cuDNN v8.2.2 is the one to download. Click the version you want to install it will drop down the menu.
```
https://developer.nvidia.com/rdp/cudnn-archive
```
- Select the following, it will redirect you to NVIDIA account registration (which is free and must to download cuDNN). 
```
cuDNN Runtime Library for Ubuntu20.04 x86_64 (Deb)
cuDNN Developer Library for Ubuntu20.04 x86_64 (Deb)
cuDNN Code Samples and User Guide for Ubuntu20.04 x86_64 (Deb)
```
- After downloading, you should have the following three .deb files
```
libcudnn8_8.2.2.26–1+cuda11.4_amd64.deb
libcudnn8-dev_8.2.2.26–1+cuda11.4_amd64.deb
libcudnn8-samples_8.2.2.26–1+cuda11.4_amd64.deb
```
- Install using dpkg commands
```
sudo dpkg -i libcudnn8_8.2.2.26–1+cuda11.4_amd64.deb
sudo dpkg -i libcudnn8-dev_8.2.2.26–1+cuda11.4_amd64.deb
sudo dpkg -i libcudnn8-samples_8.2.2.26–1+cuda11.4_amd64.deb
```
- Reboot your computer
```
reboot
```
- To verify the installation
```
nvidia-smi
nvcc --version
```

