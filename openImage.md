## 使用 open image 資料集, 以 YOLOv4 訓練
#### [參考影片](https://www.youtube.com/watch?v=zJDUhGL26iU&t=1175s)
#### 下載資料集: Boy, Woman, Man, Girl
* [Github: EscVM/OIDv4_ToolKit](https://github.com/EscVM/OIDv4_ToolKit)
    * 環境設定, [套件安裝 requirements](https://github.com/EscVM/OIDv4_ToolKit/blob/master/requirements.txt)
    * opencv-python 可以另外處理(不安裝)
    * 下載: 
        * $ mkvirtualenv oid -p python3
        * $ workon oid
        * (oid)$ ln -fs ~/.virtualenvs/cv/lib/python3.6/site-packages/cv2/cv2.so ~/.virtualenvs/oid/lib/python3.6/site-packages/cv2.so   # (連結 cv2.so 至library)
        * (oid)$ git clone https://github.com/EscVM/OIDv4_ToolKit
        * (oid)$ cd OIDv4_ToolKit
        * (oid)$ python main.py downloader --classes Boy Woman Man Girl --type_csv train --limit 1000 --multiclasses 1
        * (oid)$ mkdir ~/AlexeyAB/darknet/data/oid -p
        * (oid)$ cp OID/Dataset/* ~/AlexeyAB/darknet/data/oid
        * (oid)$ cd ~/AlexeyAB/darknet
        * (oid)$ find data/oid -name "*.jpg" -print > train.txt
        * (oid)$ mv train.txt data
    * convert annotation:
        * 修改 classes.txt
##
<pre>
Boy
Woman
Man
Girl
</pre>
##
* (oid)$ python convert_annotations.py 
* [program](https://github.com/Jahidur1414/OIDv4_ToolKit-For-Custom-Data-Set-Create-/blob/master/convert_annotations.py)
##
### related configurations:
* [data/oid.data](https://github.com/jumbokh/yolo-class/blob/master/oid/cfg/obj.data)
* [cfg/yolov4-oid.cfg](https://github.com/jumbokh/yolo-class/blob/master/oid/cfg/yolov4-oid.cfg)
* [data/oid.names](https://github.com/jumbokh/yolo-class/blob/master/oid/cfg/obj.names)
### [YOLOv4 pretrained Partial weights from AlexeyAB: yolov4.conv.173](https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137)
##
### Train:
* copy images files to : darknet/data/obj
* mkdir backup
* (oid)$ ./darknet detector train data/obj.data cfg/yolov4-oid.cfg w/yolov4.conv.173 -i 0
* [trained-weights](https://drive.google.com/open?id=1cDuyHnDQZcABnVBFtM1f0Zvmbsw0IP3e)
##
### predict:
* (oid)$ ./darknet detector test data/obj.data cfg/yolov4-oid.cfg w/yolov4-oid_last.weights -i 0
* ![child5](https://github.com/jumbokh/yolo-class/blob/master/oid/out-oid/child5-oid.jpg)
##
### result (Man, Woman, Boy, Girl)
* [Boy_Woman_Man predict result](https://github.com/jumbokh/yolo-class/blob/master/oid/out-oid/oid-predict-Man_Woman_Boy.odt)
##
### 參考連結
* [手把手的深度學習實務](https://github.com/jumbokh/hands-on-DL/blob/master/slides_181202.pdf)
