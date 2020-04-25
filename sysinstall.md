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

## 參考
[darkflow test github](https://github.com/inhail/darkflow)
         
