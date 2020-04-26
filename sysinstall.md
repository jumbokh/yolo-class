## install ubuntu system
## 
### install opencv3
* [opencv3 install](https://www.learnopencv.com/install-opencv3-on-ubuntu/)
* Need install: [libjasper-dev](https://blog.csdn.net/CAU_Ayao/article/details/83990246)
* libpng12-dev ==> libpng-dev [see here](https://askubuntu.com/questions/991706/e-package-libpng12-dev-has-no-installation-candidate)
    * sudo apt-get install libtiff4-dev ==> error [see here](https://hant-kb.kutu66.com/others/post_12889923)
    *  sudo apt-get install libtiff5-dev
* libgstreamer0.10-dev ==> [error, see here](https://mlog.club/article/2282932)
    * sudo apt -y install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
### workon facecourse-py3
### pip install imutils
### requirements.txt
<pre>
numpy==1.17.3
matplotlib==3.1.1
Cython==0.29.13
#opencv-contrib-python==4.1.1.26
#opencv-python==4.1.1.26
h5py==2.10.0
jupyter==1.0.0
pandas==0.25.2
scikit-learn==0.21.3
scipy==1.3.1
seaborn==0.9.0
tensorflow==2.0.0
Keras==2.3.1
</pre>
##
### install cuDNN
* [NVIDIA](https://developer.nvidia.com/cuda-downloads)
* install cuda driver for ubuntu 18.04 [check yuour version](https://blog.csdn.net/ZJU_QZH/article/details/85062258)
* [**Ubuntu 16.04 安裝CUDA 10.0 + cuDNN 7.3](https://medium.com/@zihansyu/ubuntu-16-04-%E5%AE%89%E8%A3%9Dcuda-10-0-cudnn-7-3-8254cb642e70)
* [cuDNN Download](https://developer.nvidia.com/rdp/cudnn-download)
* install for ubuntu procedure
<pre>
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb
sudo apt-key add /var/cuda-repo-10-2-local-10.2.89-440.33.01/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
</pre>
##
### Installing Darknet
* update ~/.bashrc, 在檔案最末一行, 添加兩行
</pre>
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64:/usr/local/cuda/64:/usr/local/lib:$LD_LIBRARY_PATH
</pre>
* $ source ~/.bashrc
* [Installing Darknet](https://pjreddie.com/darknet/install/#cuda)
* 修改 Darknet 的 Makefile
<pre>
GPU=1
CUDNN=1
OPENCV=1
OPENMP=0
DEBUG=0
</pre>
### recompile darknet to GPU version
* ./darknet imtest data/eagle.jpg
* [解决nvcc找不到的问题](https://blog.csdn.net/rtygbwwwerr/article/details/73656876)
<pre>
1.使用sudo apt-get autoremove nvidia-cuda-toolkit 卸载7.5版本

2.查看/usr/local/cuda/bin下是否有nvcc可执行程序，如果没有说明cuda没有正常安装，需要重新安装，如果有，进入下一步

3.添加环境变量，打开~/.bashrc ，添加环境变量export PATH=$PATH:/usr/local/cuda/bin

4.再在terminal中输入nvcc --version可以看到已经可以显示为8.0版本了

原文链接：https://blog.csdn.net/rtygbwwwerr/java/article/details/73656876
</pre>
## 參考
[darkflow test github](https://github.com/inhail/darkflow)
         
