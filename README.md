# yolo-project: 
## Project Schedule: 4/27~5/10
## Objective: 
* 就是要用v3架構，因為他的架構比v2快，但是v3原始僅能辨識80種物品，而v2架構下有一個yolo9000，可辨識9000種物品，但是跟v3架構不同
* 需求就是用v3架構，載入的是9000的權重跟類別名稱
* 就是可以用yolov3模型，辨識9K種物品
##
## YOLO archi
* ![Archi](https://github.com/jumbokh/yolo-class/blob/master/images/YOLO-Archi.png)
##
[philipperemy/yolo-9000](https://github.com/philipperemy/yolo-9000)
<pre>
YOLOv2是Joseph Redmon提出的针对YOLO算法不足的改进版本，
作者使用了一系列的方法对原来的YOLO多目标检测框架进行了改进，
在保持原有速度的优势之下，精度上得以提升，此外作者提出了一种目标分类与检测的联合训练方法，
通过这种方法YOLO9000可以同时在COCO和ImageNet数据集中进行训练，训练后的模型可以实现多达9000种物体的实时检测。
第一种：为darknet添加Python接口
Github：https://github.com/SidHard/py-yolo2

第二种：使用keras
Github：https://github.com/allanzelener/YAD2K
</pre>
## 硬體需求及檔案
<pre>
Simultaneous detection and classification of 9000 objects:

yolo9000.weights - (186 MB Yolo9000 Model) requires 4 GB GPU-RAM: http://pjreddie.com/media/files/yolo9000.weights

yolo9000.cfg - cfg-file of the Yolo9000, also there are paths to the 9k.tree and coco9k.map https://github.com/AlexeyAB/darknet/blob/617cf313ccb1fe005db3f7d88dec04a04bd97cc2/cfg/yolo9000.cfg#L217-L218

9k.tree - WordTree of 9418 categories - <label> <parent_it>, if parent_id == -1 then this label hasn't parent: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.tree

coco9k.map - map 80 categories from MSCOCO to WordTree 9k.tree: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/coco9k.map

combine9k.data - data file, there are paths to: 9k.labels, 9k.names, inet9k.map, (change path to your combine9k.train.list): https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/combine9k.data

9k.labels - 9418 labels of objects: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.labels

9k.names - 9418 names of objects: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.names

inet9k.map - map 200 categories from ImageNet to WordTree 9k.tree: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/inet9k.map
</pre>
## weights:
* [darknet site](https://github.com/pjreddie/darknet)
* [yolo9000.weights](http://pjreddie.com/media/files/yolo9000.weights)
##
## 系統安裝
* [從O.S.開始](https://github.com/jumbokh/yolo-class/blob/master/sysinstall.md)
##
## 下載 Dataset
### ImageNet
* [imagenet](http://www.image-net.org/challenges/LSVRC/2012/downloads)
    * Training images (Task 1 & 2). 138GB.
    * Validation images (all tasks). 6.3GB.
    * Training bounding box annotations (Task 1 & 2 only). 20MB.
* [ImageNet数据集下载与处理](https://zhuanlan.zhihu.com/p/42696535)
##
### VOC
<pre>
wget https://pjreddie.com/media/files/VOCtrainval_11-May-2012.tar
wget https://pjreddie.com/media/files/VOCtrainval_06-Nov-2007.tar
wget https://pjreddie.com/media/files/VOCtest_06-Nov-2007.tar
tar xf VOCtrainval_11-May-2012.tar
tar xf VOCtrainval_06-Nov-2007.tar
tar xf VOCtest_06-Nov-2007.tar
</pre>
* Generate Labels for VOC
    * wget https://pjreddie.com/media/files/voc_label.py
    * python voc_label.py
    * cat 2007_train.txt 2007_val.txt 2012_*.txt > train.txt
    * edit cfg/voc.data
        <pre>
         1 classes= 20
  2 train  = <path-to-voc>/train.txt
  3 valid  = <path-to-voc>2007_test.txt
  4 names = data/voc.names
  5 backup = backup
        </pre>
   * Download Pretrained Convolutional Weights
       * wget https://pjreddie.com/media/files/darknet53.conv.74
   * mkdir backup
   * Train the model
       * ./darknet detector train cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74
 ##
 ### COCO dataset
 #### Get The COCO Data
 <pre>
 cp scripts/get_coco_dataset.sh data
cd data
bash get_coco_dataset.sh
 </pre>
 #### Modify cfg for COCO
 * cfg/coco.data
 <pre>
 1 classes= 80
  2 train  = <path-to-coco>/trainvalno5k.txt
  3 valid  = <path-to-coco>/5k.txt
  4 names = data/coco.names
  5 backup = backup
  </pre>
  #### Look at cfg/yolo.cfg
  <pre>
  [net]
# Testing
# batch=1
# subdivisions=1
# Training
batch=64
subdivisions=8
....
  </pre>
#### Train the Model
* w/o GPU
    * ./darknet detector train cfg/coco.data cfg/yolov3.cfg darknet53.conv.74
 * w GPU
     * ./darknet detector train cfg/coco.data cfg/yolov3.cfg darknet53.conv.74 -gpus 0
     * or
     * ./darknet detector train cfg/coco.data cfg/yolov3.cfg darknet53.conv.74 -i 0
     * stop & restart
     * ./darknet detector train cfg/coco.data cfg/yolov3.cfg backup/yolov3.backup -gpus 0,1,2,3
##
## 測試步驟
* [測試](https://github.com/jumbokh/yolo-class/blob/master/basic.md)
### 參考連結
* [目标检测|YOLOv2原理与实现(附YOLOv3)](https://zhuanlan.zhihu.com/p/35325884)
* [深度學習-物件偵測YOLOv1、YOLOv2和YOLOv3 cfg 檔解讀(一)](https://medium.com/@chih.sheng.huang821/%E6%B7%B1%E5%BA%A6%E5%AD%B8%E7%BF%92-%E7%89%A9%E4%BB%B6%E5%81%B5%E6%B8%ACyolov1-yolov2%E5%92%8Cyolov3-cfg-%E6%AA%94%E8%A7%A3%E8%AE%80-75793cd61a01) 
* [Using yolo v3 to detect direction of an object](https://github.com/jaskarannagi19/yolov3)
* [Is it possible to use yolo3 with yolo9000 weights for more classes?](https://stackoverflow.com/questions/57853707/is-it-possible-to-use-yolo3-with-yolo9000-weights-for-more-classes)
* [yoloV3的驚豔結果–比較yoloV2](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/625318/)
* [Yolo：基於深度學習的物件偵測 (含YoloV3)](https://mropengate.blogspot.com/2018/06/yolo-yolov3.html)
##
### 官網
* [Darknet/yolo官網](https://pjreddie.com/darknet/yolo/)
### News
<pre>
YOLO Darknet 的維護者俄羅斯人 Alexey Bochkovskiy 發現中研院資科所博後王建堯及所長廖弘源研發的 CSPNet detector 又快又好，
於是邀請中研院資科所以此為 backbone 發展 YOLOv4 ，速度及正確率比上一代 YOLOv3 都要好。

YOLOv4 英文論文： https://arxiv.org/abs/2004.10934
YOLOv4 開放原始碼： https://github.com/AlexeyAB/darknet
YOLOv4 繁體中文介紹： https://bangqu.com/Y47n33.html
CSPNet 英文論文： https://arxiv.org/pdf/1911.11929.pdf
CSPNet 開放原始碼： https://github.com/WongKinYiu/CrossStagePartialNetworks

由於 YOLOv4 演算法實在是太厲害了，又是台灣之光， ORAI 人工智慧軟體會盡快整合好 YOLOv4 演算法，
並提供教學影片： https://tw.openrobot.org/product/index?sn=11239
</pre>
### 文件
* [YOLOv3.pdf](https://pjreddie.com/media/files/papers/YOLOv3.pdf)
* [YOLO9000: Better, Faster, Stronger](https://arxiv.org/abs/1612.08242)
* [YOLO v4 說明](https://github.com/jumbokh/yolo-class/blob/master/doc/YOLO%20v4%E5%AE%83%E4%BE%86%E4%BA%86%EF%BC%9A%E6%8E%A5%E6%A3%92%E8%80%85%E5%87%BA%E7%8F%BE%EF%BC%8C%E9%80%9F%E5%BA%A6%E6%95%88%E6%9E%9C%E9%9B%99%E6%8F%90%E5%8D%87%20-%20%E5%B9%AB%E8%B6%A3.pdf)
