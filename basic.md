## 基本測試
* 檔案目錄
<pre>
yolo-
          cfg
          data
          w
</pre>
## image net download
* [image net](http://image-net.org/download-images)
##
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
* ./darknet detector train cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74
##
