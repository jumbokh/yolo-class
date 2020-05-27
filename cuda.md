## Install CUDA related stuff
* [在UBUNTU 18.04 下安裝NVIDIA 顯示卡驅動程式以及 PGSTROM / INSTALL NVIDIA DRIVER CUDA PGSTROM IN UBUNTU 1804](https://gitpress.io/@chchang/install-nvidia-driver-cuda-pgstrom-in-ubuntu-1804)
* lsmod|grep nvidia 
* ubuntu-drivers devices
* deviceQuery
<pre>
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget http://developer.download.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda-repo-ubuntu1804-10-1-local-10.1.243-418.87.00_1.0-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-10-1-local-10.1.243-418.87.00_1.0-1_amd64.deb
sudo apt-key add /var/cuda-repo-10-1-local-10.1.243-418.87.00/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
</pre>
##
### [Opencv with CUDA](https://gist.github.com/raulqf/f42c718a658cddc16f9df07ecc627be7)
<pre>
cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_C_COMPILER=/usr/bin/gcc-7 \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D INSTALL_C_EXAMPLES=OFF \
-D WITH_TBB=ON \
-D WITH_CUDA=ON \
-D BUILD_opencv_cudacodec=OFF \
-D ENABLE_FAST_MATH=1 \
-D CUDA_FAST_MATH=1 \
-D CUDA_ARCH_BIN="5.3 6.0 6.1 7.0 7.5" \
-D WITH_CUBLAS=1 \
-D WITH_V4L=ON \
-D WITH_QT=OFF \
-D WITH_OPENGL=ON \
-D WITH_GSTREAMER=ON \
-D OPENCV_GENERATE_PKGCONFIG=ON \
-D OPENCV_PC_FILE_NAME=opencv.pc \
-D OPENCV_ENABLE_NONFREE=ON \
-D OPENCV_PYTHON3_INSTALL_PATH=~/.virtualenvs/cv4/lib/python3.6/site-packages \
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-4.2.0/modules \
-D PYTHON_EXECUTABLE=~/.virtualenvs/cv4/bin/python \
-D BUILD_EXAMPLES=ON ..
</pre>
##
### Enable cuda4dnn on hardware without support for __half #16218
####  ran my CMAKE with CUDA_ARCH_BIN="5.3 6.0 6.1 7.0 7.5"
