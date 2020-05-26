## 使用 open image 資料集, 以 YOLOv4 訓練
#### [參考影片](https://www.youtube.com/watch?v=zJDUhGL26iU&t=1175s)
#### 下載資料集: Boy, Woman, Man, Girl
* [Github: EscVM/OIDv4_ToolKit](https://github.com/EscVM/OIDv4_ToolKit)
    * 環境設定, [套件安裝](https://github.com/EscVM/OIDv4_ToolKit/blob/master/requirements.txt)
    * opencv-python 可以另外處理(不安裝)
    * 下載: 
        * $ mkvirtualenv oid -p python3
        * $ workon oid
        * (連結 cv2.so 至library)
        * $ git clone https://github.com/EscVM/OIDv4_ToolKit
        * (oid)$ cd OIDv4_ToolKit
        * (oid)$ python main.py downloader --classes Boy Woman Man Girl --type_csv train --limit 1000 --multiclasses 1
    * convert annotation:
        * 修改 classes.txt
##
<pre>
Boy
Woman
Man
Girl
</pre>
        * (oid)$ python convert_annotations.py [program](https://github.com/Jahidur1414/OIDv4_ToolKit-For-Custom-Data-Set-Create-/blob/master/convert_annotations.py)
##
### relative configurations:
* [data/oid.data]()
* [cfg/yolov4-oid.cfg]()
* [data/oid.names]()
### [yolov4.conv.173]()
##
### Train:
* copy images files to : darknet/data/obj
* mkdir backup
* (oid)$ ./darknet detector train data/obj.data cfg/yolov4-oid.cfg w/yolov4.conv.173 -i 0
##
### predict:
* ()oid)$ ./darknet detector test data/obj.data cfg/yolov4-oid.cfg w/yolov4.conv.173 -i 0
##
### result (Man, Woman, Boy, Girl)
* [predict result]()
