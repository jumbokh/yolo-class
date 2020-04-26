## 基本測試
* 檔案目錄
<pre>
yolo-
          cfg
          data
          w
          scripts
          backup
</pre>
## image net download
* [image net](http://image-net.org/download-images)
##
### Using yolov2 predict
* ./darknet-gpu detector test cfg/coco.data cfg/yolov2.cfg w/yolov2.weights data/dog.jpg
<pre>
mask_scale: Using default '1.000000'
Loading weights from w/yolov2.weights...Done!
data/kite.jpg: Predicted in 0.137217 seconds.
kite: 80%
kite: 67%
person: 74%
person: 67%
</pre>
* ![dog](https://github.com/jumbokh/yolo-class/blob/master/images/predictions.jpg)
* ![kite](https://github.com/jumbokh/yolo-class/blob/master/images/yolov2-kite.jpg)
##
### Using yolov3 predict
* ./darknet-gpu detector test cfg/coco.data cfg/yolov3.cfg w/yolov3.weights data/kite.jpg
<pre>
Loading weights from w/yolov3.weights...Done!
data/kite.jpg: Predicted in 0.166759 seconds.
kite: 99%
kite: 84%
kite: 80%
kite: 73%
person: 100%
person: 100%
person: 97%
person: 96%
person: 95%
person: 91%
person: 88%
person: 85%
person: 52%
</pre>
* ![kite](https://github.com/jumbokh/yolo-class/blob/master/images/yolov3-kite.jpg)
### VOC Train
* [Training YOLO on VOC](https://pjreddie.com/darknet/yolo/)
* [VOC paper](https://github.com/jumbokh/yolo-class/blob/master/doc/ijcv_voc09.pdf)
#### Get VOC data
<pre>
wget https://pjreddie.com/media/files/VOCtrainval_11-May-2012.tar
wget https://pjreddie.com/media/files/VOCtrainval_06-Nov-2007.tar
wget https://pjreddie.com/media/files/VOCtest_06-Nov-2007.tar
tar xf VOCtrainval_11-May-2012.tar
tar xf VOCtrainval_06-Nov-2007.tar
tar xf VOCtest_06-Nov-2007.tar
</pre>
####  run the voc_label.py
* wget https://pjreddie.com/media/files/voc_label.py
* python voc_label.py
* Output List
<pre>
ls
2007_test.txt   VOCdevkit
2007_train.txt  voc_label.py
2007_val.txt    VOCtest_06-Nov-2007.tar
2012_train.txt  VOCtrainval_06-Nov-2007.tar
2012_val.txt    VOCtrainval_11-May-2012.tar
</pre>
#### Generate Train List
* cat 2007_train.txt 2007_val.txt 2012_*.txt > train.txt
#### change the cfg/voc.data
<pre>
  1 classes= 20
  2 train  = <path-to-voc>/train.txt
  3 valid  = <path-to-voc>2007_test.txt
  4 names = data/voc.names
  5 backup = backup
</pre>
#### Download Pretrained Convolutional Weights
* wget https://pjreddie.com/media/files/darknet53.conv.74
#### Train The Model
* mkdir ~/yolo/backup
* ./darknet detector train cfg/voc.data cfg/yolov3-voc.cfg w/darknet53.conv.74
* ./darknet detector train cfg/coco.data cfg/yolov3.cfg backup/yolov3.backup -i 0
##
#### Validate the weights
<pre>
在訓練期間，您會看到各種錯誤指示，並且當不再減少0.XXXXXXX avg時，您應該停止操作：

區域平均IOU：0.798363，類：0.893232，對象：0.700808，無對象：0.004567，平均調用率：1.000000，計數：8區域平均IOU：0.800677，類：0.892181，對象：0.701590，無對象：0.004574，平均調用率：1.000000 ，數：8

9002：0.211667，0.060730 平均，0.001000速率，3.868000秒，576128圖像加載：0.000000秒

9002-迭代編號（批處理數量）
0.060730平均 -平均損失（錯誤）- 越低越好
當您發現平均損失0.xxxxxx平均不再在許多次迭代中減少時，您應該停止訓練。

訓練停止後，您應該.weights從中提取一些最後的文件，darknet\build\darknet\x64\backup並從中選擇最好的文件：

例如，您在9000次迭代後停止了訓練，但最佳結果可以給出以前的權重之一（7000、8000、9000）。可能由於過度擬合而發生。過度擬合 -這種情況是您可以從訓練數據集中檢測圖像上的對象，但無法檢測其他圖像上的對象。您應該從Early Stopping Point獲得權重：
</pre>
* ![Early Stoping](https://hsto.org/files/5dc/7ae/7fa/5dc7ae7fad9d4e3eb3a484c58bfc1ff5.png)
<pre>
2.1。首先，obj.data您必須在文件中指定驗證數據集的路徑valid = valid.txt（格式valid.txt為中的train.txt），如果您沒有驗證圖片，則只需複製data\train.txt到即可data\valid.txt。

2.2如果在9000次迭代後停止訓練，要驗證以前的權重，請使用以下命令：

（如果您使用另一個GitHub存儲庫，請使用darknet.exe detector recall...而不是darknet.exe detector map...）

darknet.exe detector recall data/obj.data yolo-obj.cfg backup\yolo-obj_7000.weights
darknet.exe detector recall data/obj.data yolo-obj.cfg backup\yolo-obj_8000.weights
darknet.exe detector recall data/obj.data yolo-obj.cfg backup\yolo-obj_9000.weights
每個權重（7000、8000、9000）的comapre最後輸出線：

選擇具有最高 IoU（聯合的相交）和mAP（平均平均精度）的權重文件

例如，較大的IOU會賦予權重yolo-obj_8000.weights-然後使用此權重進行檢測。

自定義對象檢測的示例： darknet.exe detector test data/obj.data yolo-obj.cfg yolo-obj_8000.weights
</pre>
#### Screen for GPU monitor:  nvidia-smi -l
* ![running darknet](https://github.com/jumbokh/yolo-class/blob/master/images/gpu0.jpg)
### 文件
* [NVIDIA - Deep Learning SDK Documentation](https://docs.nvidia.com/deeplearning/sdk/tensorrt-developer-guide/index.html)
