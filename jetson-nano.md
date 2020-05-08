## Jetson Nano 安裝及測試
* [jetpack SDK](https://developer.nvidia.com/embedded/jetpack)
* [Getting Start Guide](https://developer.download.nvidia.com/embedded/L4T/r32-3-1_Release_v1.0/Jetson_Nano_Developer_Kit_User_Guide.pdf?bIKjG7vqM-PvFhcQfHbtORlX2VZVqN1FQgBkeJ2XupnY4bkfepr3oUPUR5u7DuZ7IgS-qPPgHcpjY56u7basDlwQgEzGyHdrSwg4WKqUdjinj7mdfJBNRtYKbCVMc6gsneLoctJ73iGrX07OzqGkBdEJ2TEmYFwph-RmeHUiY__QgV0J6Gy5Cgs)
* [Getting started with the NVIDIA Jetson Nano](https://www.pyimagesearch.com/2019/05/06/getting-started-with-the-nvidia-jetson-nano/)
* [Building the Project from Source](https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md#downloading-models)
    * nvcc -V
 <pre>
 jumbo@jumbo-nano:~/jetsonUtilities$ nvcc -V
 nvcc: NVIDIA (R) Cuda compiler driver
 Copyright (c) 2005-2019 NVIDIA Corporation
 Built on Wed_Oct_23_21:14:42_PDT_2019
 Cuda compilation tools, release 10.2, V10.2.89
 </pre>
##
    * jumbo@jumbo-nano:~/jetsonUtilities$ python ./jetsonInfo.py 
 <pre>
 NVIDIA Jetson TX1
 L4T 32.4.2 [ JetPack UNKNOWN ]
 Ubuntu 18.04.4 LTS
 Kernel Version: 4.9.140-tegra
 CUDA 10.2.89
</pre>
* [OpenCV 4 + CUDA on Jetson Nano](https://www.jetsonhacks.com/2019/11/22/opencv-4-cuda-on-jetson-nano/)
* [Classifying Images with ImageNet](https://github.com/dusty-nv/jetson-inference/blob/master/docs/imagenet-console-2.md)
##
### 測試 tensorflow-yolov3
* [快如閃電的目標檢測YOLOv3算法，有了TensorFlow實現](https://kknews.cc/zh-tw/code/ab6qjm6.html)
* [YunYang1994/tensorflow-yolov3](https://github.com/YunYang1994/tensorflow-yolov3)
* [requirements for tensorflow-gpu @ jetson nano](https://github.com/jumbokh/yolo-class/blob/master/doc/jetson-requ.txt)
##
### 攝影機
<pre>
gst-launch-1.0 nvarguscamerasrc ! 'video/x-raw(memory:NVMM),width=3820, height=2464, framerate=21/1, format=NV12' ! nvvidconv flip-method=0 ! 'video/x-raw,width=960, height=616' ! nvvidconv ! nvegltransform ! nveglglessink -e
</pre>
##
### 參考
* [如何讓Jetson Nano順利執行OpenCV中CUDA函式](https://makerpro.cc/2019/06/how-to-make-jetson-nano-perform-cuda-in-opencv4-1-0-smoothly/)
* [TX2安裝教學(中文)](http://www.honghutech.com/nvidia-jeston-tx2/flashtx2)
* [Tensorflow-gpu 安裝](https://medium.com/aiot-taipei/jeston-nano-tensorflow-gpu-%E5%AE%89%E8%A3%9D-b26d42f7c3f3)
##
### Q & A
##
#### 1. 安裝 tensorflow-gpu 遇到問題時
<pre>
ERROR: Could not find a version that satisfies the requirement tensorflow-gpu==1.11 (from versions: 1.13.1+nv19.3, 1.13.1+nv19.4, 1.13.1+nv19.5, 1.14.0+nv19.7, 1.14.0+nv19.9, 1.14.0+nv19.10, 1.15.0+nv19.11, 2.0.0+nv19.11)
ERROR: No matching distribution found for tensorflow-gpu==1.11
</pre>
#### 選擇其中一種組合解決
<pre>
(cv) jumbo@jumbo-nano:~/tensorflow-yolov3$ pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v42 tensorflow-gpu==1.15.0+nv19.11
Looking in indexes: https://pypi.org/simple, https://developer.download.nvidia.com/compute/redist/jp/v42
Collecting tensorflow-gpu==1.15.0+nv19.11
</pre>
##
#### 2. numpy 相容問題
<pre>
ERROR: tensorflow-gpu 1.15.0+nv19.11.tf1 has requirement numpy<2.0,>=1.16.0, but you'll have numpy 1.15.1 which is incompatible.
</pre>
##
#### 安裝 numpy 1.16.0 解決
<pre>
pip install -U numpy==1.16.0
</pre>
##
#### 3. 轉檔 (weights) 時的問題
* easydict
    * pip install easydict
* no cv2
    * ln -fs ~/.virtualenvs/deep_learning/lib/python3.6/site-packages/cv2.so cv2.so
 * no libcudart.so.10.0
     * cd /usr/local/cuda/lib64
     * ln -fs /usr/local/cuda/lib64/libcudart.so.10.2 /usr/local/cuda/lib64/libcudart.so.10.0
  ##
  #### 4.  File ./checkpoint/yolov3_coco.ckpt.meta does not exist
  * [Converting YOLO* Models to the Intermediate Representation (IR)](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_tf_specific_Convert_YOLO_From_Tensorflow.html)
