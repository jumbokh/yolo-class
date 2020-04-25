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
* [從頭開始](https://github.com/jumbokh/yolo-class/blob/master/sysinstall.md)
### 參考連結
* [目标检测|YOLOv2原理与实现(附YOLOv3)](https://zhuanlan.zhihu.com/p/35325884)
* [深度學習-物件偵測YOLOv1、YOLOv2和YOLOv3 cfg 檔解讀(一)](https://medium.com/@chih.sheng.huang821/%E6%B7%B1%E5%BA%A6%E5%AD%B8%E7%BF%92-%E7%89%A9%E4%BB%B6%E5%81%B5%E6%B8%ACyolov1-yolov2%E5%92%8Cyolov3-cfg-%E6%AA%94%E8%A7%A3%E8%AE%80-75793cd61a01) 
* [Using yolo v3 to detect direction of an object](https://github.com/jaskarannagi19/yolov3)
* [Is it possible to use yolo3 with yolo9000 weights for more classes?](https://stackoverflow.com/questions/57853707/is-it-possible-to-use-yolo3-with-yolo9000-weights-for-more-classes)
* [yoloV3的驚豔結果–比較yoloV2](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/625318/)
* [Yolo：基於深度學習的物件偵測 (含YoloV3)](https://mropengate.blogspot.com/2018/06/yolo-yolov3.html)
##
### 文件
* [YOLOv3.pdf](https://pjreddie.com/media/files/papers/YOLOv3.pdf)
* [YOLO9000: Better, Faster, Stronger](https://arxiv.org/abs/1612.08242)
