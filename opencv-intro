### [Ubuntu 18.04 安裝 OpenCV 與建置 C++ 編譯環境](https://wenyuangg.github.io/posts/opencv/opencv-installation.html)
### with CUDA
#### cmake: reinstall to most recent released version
#### param
<pre>
cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON -DCUDA_ARCH_BIN="3.0 3.5 3.7 5.0 5.2 6.0 6.1" -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -DCMAKE_CXX_FLAGS=-isystem\ /opt/nvidia-video-codec/include -DWITH_CUDA=ON  -DBUILD_opencv_cudacodec=OFF -DWITH_OPENCL=OFF -DWITH_OPENCLAMDBLAS=OFF -DWITH_OPENCLAMDFFT=OFF -DCUDA_NVCC_FLAGS="--expt-relaxed-constexpr" -DOPENCV_ENABLE_NONFREE=ON -DBUILD_opencv_cnn_3dobj=OFF -DBUILD_opencv_dnn=OFF -DBUILD_opencv_dnn_modern=OFF -DWITH_NVCUVID_opencv_cudacodec=ON -DWITH_GTK_2_X=ON ..
</pre>
##
#### with some notes
* CUDA
<pre>
alealv commented on 28 Dec 2018
Be careful, because the solution that I posted is for:

OpenCV ==> master branch
CUDA ==> v10.0 (the older version of CUDA still contains the video decoder)

The option that should be activated is:
cmake -DWITH_NVCUVID=ON -DBUILD_opencv_cudacodec=ON ..
</pre>
