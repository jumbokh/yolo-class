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
### 參考
* [如何讓Jetson Nano順利執行OpenCV中CUDA函式](https://makerpro.cc/2019/06/how-to-make-jetson-nano-perform-cuda-in-opencv4-1-0-smoothly/)
* [TX2安裝教學(中文)](http://www.honghutech.com/nvidia-jeston-tx2/flashtx2)
* [Tensorflow-gpu 安裝](https://medium.com/aiot-taipei/jeston-nano-tensorflow-gpu-%E5%AE%89%E8%A3%9D-b26d42f7c3f3)

