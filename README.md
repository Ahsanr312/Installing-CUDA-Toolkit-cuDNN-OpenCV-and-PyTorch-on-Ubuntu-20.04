# Installing CUDA-Toolkit 11.4, cuDNN v8.2.2, OpenCV 4.5.2 and PyTorch 1.8 on Ubuntu-20.04
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

#### 03. OpenCV 4.5.2 Installation
- Install and Update the system
```
sudo apt update
sudo apt upgrade
```
- Install required libraries and tools like Video/Audio Libs - FFMPEG, GSTREAMER, x264 etc. 
```
sudo apt install build-essential cmake pkg-config unzip yasm git checkinstall
sudo apt install libjpeg-dev libpng-dev libtiff-dev
sudo apt install libavcodec-dev libavformat-dev libswscale-dev libavresample-dev
sudo apt install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
sudo apt install libxvidcore-dev x264 libx264-dev libfaac-dev libmp3lame-dev libtheora-dev
sudo apt install libfaac-dev libmp3lame-dev libvorbis-dev
sudo apt install libopencore-amrnb-dev libopencore-amrwb-dev
```
- Cameras programming interface libs
```
sudo apt-get install libdc1394-22 libdc1394-22-dev libxine2-dev libv4l-dev v4l-utils
cd /usr/include/linux
sudo ln -s -f ../libv4l1-videodev.h videodev.h
cd ~
```
- GTK lib for the graphical user functionalites coming from OpenCV highghui module
```
sudo apt-get install libgtk-3-dev
```
- Python Libraries for Python3
```
sudo apt-get install python3-dev python3-pip
sudo -H pip3 install -U pip numpy
sudo apt install python3-testresources
```
- Parallelism library C++ for CPU
```
sudo apt-get install libtbb-dev
```
- Optimization libraries for OpenCV
```
sudo apt-get install libprotobuf-dev protobuf-compiler
sudo apt-get install libgoogle-glog-dev libgflags-dev
sudo apt-get install libgphoto2-dev libeigen3-dev libhdf5-dev doxygen
```
- Proceed with the installation by downloading and unzipping OpenCV and OpenCV_Contrib
```
cd ~/Downloads
wget -O opencv.zip https://github.com/opencv/opencv/archive/refs/tags/4.5.2.zip
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/refs/tags/4.5.2.zip
unzip opencv.zip
unzip opencv_contrib.zip
```
- Instal virutalenvwrapper and create a virtual envirnoment for the OpenCV installation
```
sudo pip install virtualenv virtualenvwrapper
sudo rm -rf ~/.cache/pip
echo "Edit ~/.bashrc"
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
mkvirtualenv cv -p python3
pip install numpy
```
- Direct to OpenCV folder and make a build directory for further installations
```
cd opencv-4.5.2
mkdir build
cd build
```
- Under cmake command paths are important as well as "CUDA_ARCH_BIN" that must be set according to the GPU as I have tested the process on both NVIDIA GeForce GTX 1080 and NVIDIA RTX 3060 Ti both have different value. One can find the respective GPU value from the mentioned link: https://developer.nvidia.com/cuda-gpus
```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D WITH_TBB=ON \
-D ENABLE_FAST_MATH=1 \
-D CUDA_FAST_MATH=1 \
-D WITH_CUBLAS=1 \
-D WITH_CUDA=ON \
-D BUILD_opencv_cudacodec=OFF \
-D WITH_CUDNN=ON \
-D OPENCV_DNN_CUDA=ON \
-D CUDA_ARCH_BIN=8.6 \
-D WITH_V4L=ON \
-D WITH_QT=OFF \
-D WITH_OPENGL=ON \
-D WITH_GSTREAMER=ON \
-D OPENCV_GENERATE_PKGCONFIG=ON \
-D OPENCV_PC_FILE_NAME=opencv.pc \
-D OPENCV_ENABLE_NONFREE=ON \
-D OPENCV_PYTHON3_INSTALL_PATH=~/.virtualenvs/cv/lib/python3.8/site-packages \
-D PYTHON_EXECUTABLE=~/.virtualenvs/cv/bin/python \
-D OPENCV_EXTRA_MODULES_PATH=~/Downloads/opencv_contrib-4.5.2/modules \
-D INSTALL_PYTHON_EXAMPLES=OFF \
-D INSTALL_C_EXAMPLES=OFF \
-D BUILD_EXAMPLES=OFF ..
```
- If it is fine proceed with the compilation (Use nproc to know the number of cpu cores and use that number with -j):
```
nproc
make -j20
sudo make install
```
- Include the libs in your environment
```
sudo /bin/bash -c 'echo "/usr/local/lib" >> /etc/ld.so.conf.d/opencv.conf'
sudo ldconfig
```
- If you want to have available opencv python bindings in the system environment you should copy the created folder during the installation of OpenCV (* -D OPENCV_PYTHON3_INSTALL_PATH=~/.virtualenvs/cv/lib/python3.8/site-packages *) into the dist-packages folder of the target python interpreter:






