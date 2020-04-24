## install ubuntu system
## flow :
### install opencv3
[opencv3 install](https://www.learnopencv.com/install-opencv3-on-ubuntu/)
      * Need install: [libjasper-dev](https://blog.csdn.net/CAU_Ayao/article/details/83990246)
      * libpng12-dev ==> libpng-dev [see here](https://askubuntu.com/questions/991706/e-package-libpng12-dev-has-no-installation-candidate)
      * sudo apt-get install libtiff4-dev ==> error [see here](https://hant-kb.kutu66.com/others/post_12889923)
          *  sudo apt-get install libtiff5-dev
       * libgstreamer0.10-dev ==> [error, see here](https://mlog.club/article/2282932)
           * sudo apt -y install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
         
