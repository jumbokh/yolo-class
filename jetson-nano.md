### 使用 usb serial console 連接 jetson nano
* 以micro-usb線 連接電腦
![serial](https://github.com/jumbokh/yolo-class/blob/master/images/48576.jpg)
* 安裝下載 putty
![putty](https://github.com/jumbokh/yolo-class/blob/master/images/putty.JPG)
* 開啟串列埠連結
![putty1](https://github.com/jumbokh/yolo-class/blob/master/images/putty1.JPG)
#### Add wifi connection by command line
* ex: ssid: myid, key: 12345678
* nmcli device status # check all connect setting
<pre>
DEVICE  TYPE      STATE      CONNECTION
eth0    ethernet  connected  Wired connection 1
l4tbr0  bridge    connected  l4tbr0
dummy0  dummy     unmanaged  --
rndis0  ethernet  unmanaged  --
usb0    ethernet  unmanaged  --
lo      loopback  unmanaged  --
</pre>
* nmcli con add con-name myid ifname wlan0 type wifi ssid myid ip4 192.168.43.55/24 gw4 192.168.43.254
* nmcli con modify myid wifi-sec.key-mgmt wpa-psk
* nmcli con modify myid wifi-sec.psk 12345678
* nmcli radio wifi on
* nmcli con up myid
* nmcli device status
<pre>
# nmcli device status
DEVICE  TYPE      STATE      CONNECTION
eth0    ethernet  connected  Wired connection 1
l4tbr0  bridge    connected  l4tbr0
wlan0   wifi      connected  informatics
dummy0  dummy     unmanaged  --
rndis0  ethernet  unmanaged  --
usb0    ethernet  unmanaged  --
lo      loopback  unmanaged  --
</pre>
* ifconfig
#### Find your IP
* sudo nmap -sP $(echo $(hostname -I)|cut -d'.' -f 1-3).*
* ping 192.168.43.255
* arp -a
## Jetson Nano 安裝及測試
* [NVIDIA® Jetson Nano 初體驗（一）安裝與測試](https://blog.cavedu.com/2019/06/17/nvida-jetson-nano-setup/)
* [jetpack SDK](https://developer.nvidia.com/embedded/jetpack)
* [Getting Start Guide](https://developer.download.nvidia.com/embedded/L4T/r32-3-1_Release_v1.0/Jetson_Nano_Developer_Kit_User_Guide.pdf?bIKjG7vqM-PvFhcQfHbtORlX2VZVqN1FQgBkeJ2XupnY4bkfepr3oUPUR5u7DuZ7IgS-qPPgHcpjY56u7basDlwQgEzGyHdrSwg4WKqUdjinj7mdfJBNRtYKbCVMc6gsneLoctJ73iGrX07OzqGkBdEJ2TEmYFwph-RmeHUiY__QgV0J6Gy5Cgs)
* [Getting started with the NVIDIA Jetson Nano](https://www.pyimagesearch.com/2019/05/06/getting-started-with-the-nvidia-jetson-nano/)
* [NVIDIA Jetson Nano 如何執行深度學習範例？分類模型辨識北極熊與即時影像人臉辨識](https://blog.cavedu.com/2019/04/30/nvidia-jetson-nano-example/)
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
### jtop
<pre>
sudo apt-get install python-pip python-dev build-essential 
sudo pip install --upgrade pip
sudo -H pip install jetson-stats
sudo jtop
</pre>
##
* ![jtop](https://github.com/jumbokh/yolo-class/blob/master/images/jtop.jpg)
### [Jetson nano](https://medium.com/@jackycsie/jetson-nano-9d89cbf2fc18)
##
<pre>
切換高低功率
當訓練的時候，有可能因為你的電力無法負荷而馬上跳電，nvidia 在這裡算是很親民的提供兩種方式讓你轉換，5w, 10w，降成 5w 後許多 model 就跑得動了如: Resnet50，下面是轉換低功率與正常功率的指令。
# 知道目前是哪一個 mode
sudo nvpmodel -q
# 將目前的瓦數 降為5瓦
sudo nvpmodel -m1
# 將目前的瓦數 改為 max 瓦，max 最大為(10w)
sudo nvpmodel -m0
改成 5w 後，會自動的將兩個 cpu 關閉，只使用 cpu 1, 2。
</pre>
#### Test by console command [~/jetson-inference/build-release/aarch64/bin]
*   ./imagenet-console img/golf4.jpg golf4-j.jpg
    * output: ![golf4-j.jpg](https://github.com/jumbokh/yolo-class/blob/master/images/golf4-j.jpg)
*  ./detectnet-console img/golf4.jpg ~/golf4-face.jpg facenet
    * output: ![golf4-face.jpg](https://github.com/jumbokh/yolo-class/blob/master/images/golf4-face.jpg)
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
  * [install darkflow](https://github.com/thtrieu/darkflow/blob/master/README.md#getting-started)
      * pip install Cython
      * follow the instructions in: [Converting YOLO* Models to the Intermediate Representation (IR)](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_tf_specific_Convert_YOLO_From_Tensorflow.html#install-darkflow)
      * python3 ./flow --model <path_to_model>/<model_name>.cfg --load <path_to_model>/<model_name>.weights --savepb
