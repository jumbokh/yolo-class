## imagenet data treatment
### [小白train自己的YOLO v4](https://mc.ai/%E5%B0%8F%E7%99%BDtrain%E8%87%AA%E5%B7%B1%E7%9A%84yolo-v4/)
### [ImageNet数据集下载与处理](https://zhuanlan.zhihu.com/p/42696535)
* Training images (Task 1 & 2). 138GB.
* Validation images (all tasks). 6.3GB.
* Training bounding box annotations (Task 1 & 2 only). 20MB.
* [Pretrained Convolutional Weights from darknet53](https://github.com/ultralytics/yolov3/issues/6)
* [ImageNet 中的Top-1与Top-5](https://blog.csdn.net/v1_vivian/article/details/73251187)
<pre>
一些神经网络中会提到ImageNet Top-5 或者Top-1，这是一种图片检测准确率的标准，介绍这个之前，先介绍一下ImageNet。

【ImageNet】

ImageNet 项目是一个用于物体对象识别检索大型视觉数据库。截止2016年，ImageNet 已经对超过一千万个图像进行手动注释，标记图像的类别。在至少一百万张图像中还提供了边界框。

自2010年以来，ImageNet 举办一年一度的软件竞赛，叫做（ImageNet Large Scale Visual Recognition Challenge,ILSVRC)。主要内容是通过算法程序实现正确分类和探测识别物体与场景，评价标准就是Top-5 错误率。

Top-5错误率

即对一个图片，如果概率前五中包含正确答案，即认为正确。

Top-1错误率

即对一个图片，如果概率最大的是正确答案，才认为正确。
————————————————
版权声明：本文为CSDN博主「v1_vivian」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/v1_vivian/article/details/73251187
</pre>
##

### How to change filter size of Final layer?
<pre>
In YoloV3 you have to change each filters= in 3 convolutional layers before [yolo] layer and classes in [yolo] layer
Formula is filters = (classes+5)*3 in yoloV3 (3 masks only)
</pre>
##
### 提取訓練好的權重
#### [yolo partial提取已经训练好的网络中的部分权重](https://blog.csdn.net/BlackLion_zhou/article/details/103564595)
* command: ./darknet partial yolov3-tiny.cfg yolov3-tiny_370000.weights tiny-voc-good.conv.5 5
    * ./darknet partial cfg文件　权重文件　输出名字　层数
### Error Message
<pre>
Error: l.outputs == params.inputs 
filters= in the [convolutional]-layer doesn't correspond to classes= or mask= in [yolo]-layer
</pre>
### Train 1
#### 使用 Alex 的 Darknet [AlexeyAB/darknet](https://github.com/AlexeyAB/darknet)
#### Download yolov4 partial weights: [yolov4.conv.137](https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137)
* sudo ./darknet detector train data/imagenet1k.data cfg/yolo-obj.cfg w/yolov4.conv.137 
    * [yolo-obj.cfg](https://github.com/jumbokh/yolo-class/blob/master/cfg/yolo-obj.cfg)
    * [imagenet.shortnames.list](https://github.com/AlexeyAB/darknet/blob/master/cfg/imagenet.shortnames.list)
    * [imagenet1k.data](https://github.com/jumbokh/yolo-class/blob/master/cfg/imagenet1k.data)
    * [imagenet.labels.list](https://github.com/jumbokh/yolo-class/blob/master/cfg/imagenet.labels.list)
##
### Validate
* yolo-obj_last.weights
    * ./darknet classifier valid cfg/imagenet1k.data cfg/yolo-obj.cfg ~/backup/yolo-obj_last.weights
<pre>
49990: top 1: 0.001020, top 5: 0.005481
49991: top 1: 0.001020, top 5: 0.005481
49992: top 1: 0.001020, top 5: 0.005481
49993: top 1: 0.001020, top 5: 0.005481
49994: top 1: 0.001020, top 5: 0.005481
49995: top 1: 0.001020, top 5: 0.005480
49996: top 1: 0.001020, top 5: 0.005480
49997: top 1: 0.001020, top 5: 0.005480
49998: top 1: 0.001020, top 5: 0.005480
49999: top 1: 0.001020, top 5: 0.005480
</pre>
### Train 2
#### 使用 Alex 的 Darknet [AlexeyAB/darknet](https://github.com/AlexeyAB/darknet)
#### Download yolov4 weights: [yolov4.weights](https://drive.google.com/open?id=1cewMfusmPjYWbrnuJRuKhPMwRe_b9PaT)
* sudo ./darknet detector train data/imagenet1k.data cfg/yolo-obj.cfg w/yolov4.weights
##
### Validate
* yolo-obj_last.weights
    * ./darknet classifier valid cfg/imagenet1k.data cfg/yolov4.cfg ~/backup/yolo-obj_final.weights
<pre>
49990: top 1: 0.001160, top 5: 0.005081
49991: top 1: 0.001160, top 5: 0.005081
49992: top 1: 0.001160, top 5: 0.005081
49993: top 1: 0.001160, top 5: 0.005081
49994: top 1: 0.001160, top 5: 0.005081
49995: top 1: 0.001160, top 5: 0.005080
49996: top 1: 0.001160, top 5: 0.005080
49997: top 1: 0.001160, top 5: 0.005080
49998: top 1: 0.001160, top 5: 0.005080
49999: top 1: 0.001160, top 5: 0.005080
</pre>
##
### Train 3: 22k
#### Out of memory
<pre>
 CUDA-version: 10010 (10020), cuDNN: 7.6.5, GPU count: 1  
 OpenCV version: 3.3.1
yolov4-22k
 0 : compute_capability = 610, cudnn_half = 0, GPU: GeForce GTX 1080 
net.optimized_memory = 0 
mini_batch = 2, batch = 64, time_steps = 1, train = 1 
   layer   filters  size/strd(dil)      input                output
   0  Try to set subdivisions=64 in your cfg-file. 
CUDA status Error: file: /home/jumbo/hd/AlexeyAB/darknet/src/dark_cuda.c : () : line: 373 : build time: May 16 2020 - 16:51:27 

 CUDA Error: out of memory
CUDA Error: out of memory: File exists
</pre>
####
* in cfg - convolutional layer
    * filters=65541 ?
##
### Train 4: yolo9000
### IOU = -nan  see [Alex answer](https://github.com/AlexeyAB/darknet/issues/636#issuecomment-381400954)
##
###  tensorflow的models/models/inception/inception/data
<pre>
mkdir -p ILSVRC2012
mkdir -p ILSVRC2012/raw-data
mkdir -p ILSVRC2012/raw-data/imagenet-data
mkdir -p ILSVRC2012/raw-data/imagenet-data/bounding_boxes
mv ILSVRC2012_bbox_train_v2.tar.gz ILSVRC2012/raw-data/imagenet-data/bounding_boxes/
tar xvf ILSVRC2012/raw-data/imagenet-data/bounding_boxes/ILSVRC2012_bbox_train_v2.tar.gz -C ILSVRC2012/raw-data/imagenet-data/bounding_boxes/
NUM_XML=$(ls -1 ILSVRC2012/raw-data/imagenet-data/bounding_boxes/* | wc -l)
echo "Identified ${NUM_XML} bounding box annotations."
mkdir -p ILSVRC2012/raw-data/imagenet-data/validation/
tar xf ILSVRC2012_img_val.tar -C ILSVRC2012/raw-data/imagenet-data/validation/
mkdir -p ILSVRC2012/raw-data/imagenet-data/train/
mv ILSVRC2012_img_train.tar ILSVRC2012/raw-data/imagenet-data/train/ && cd ILSVRC2012/raw-data/imagenet-data/train/
tar -xvf ILSVRC2012_img_train.tar && rm -f ILSVRC2012_img_train.tar 
find . -name "*.tar" | while read NAE ; do mkdir -p "${NAE%.tar}"; tar -xvf "${NAE}" -C "${NAE%.tar}"; rm -f "${NAE}"; done 
cd .. && cd .. && cd .. && cd ..
 
python preprocess_imagenet_validation_data.py ILSVRC2012/raw-data/imagenet-data/validation/ imagenet_2012_validation_synset_labels.txt
#这一步应将preprocess_imagenet_validation_data.py里面的JPEG改为jpeg
python process_bounding_boxes.py ILSVRC2012/raw-data/imagenet-data/bounding_boxes/ imagenet_lsvrc_2015_synsets.txt | sort > ILSVRC2012/raw-data/imagenet_2012_bounding_boxes.csv
#这一步应将process_bounding_boxes.py里面的JPEG改为jpeg
python build_imagenet_data.py --train_directory=ILSVRC2012/raw-data/imagenet-data/train/ --validation_directory=ILSVRC2012/raw-data/imagenet-data/validation/ --output_directory=ILSVRC2012/ --imagenet_metadata_file=imagenet_metadata.txt --labels_file=imagenet_lsvrc_2015_synsets.txt --bounding_box_file=ILSVRC2012/raw-data/imagenet_2012_bounding_boxes.csv
#这一步应将build_imagenet_data.py里面的JPEG改为jpeg
</pre>
##
### ImageNet : [ImageNet Classification](https://pjreddie.com/darknet/imagenet/)
* 使用 darknet: ./darknet classifier predict cfg/imagenet1k.data cfg/darknet19.cfg darknet19.weights data/dog.jpg
    * 產出結果：
 <pre>
 Loading weights from darknet19.weights...Done!
data/dog.jpg: Predicted in 0.003655 seconds.
42.58%: malamute
22.89%: Eskimo dog
12.70%: Siberian husky
 2.70%: bicycle-built-for-two
 1.20%: mountain bike
 </pre>
 * ./darknet classifier predict cfg/imagenet1k.data cfg/darknet19.cfg darknet19.weights data/eagle.jpg
<pre>
Loading weights from darknet19.weights...Done!
data/eagle.jpg: Predicted in 0.005066 seconds.
85.00%: bald eagle
11.57%: kite
 2.64%: vulture
 0.08%: great grey owl
 0.07%: hen
</pre>
### 連結
* [ImageNet数据集下载与处理](https://zhuanlan.zhihu.com/p/42696535)
* [2012 torrent](https://www.cnblogs.com/luruiyuan/p/12373328.html)
* [用tensorflow训练imagenet数据准备](https://blog.csdn.net/hustlx/article/details/76585843)
* [Tensorflow实现Alexnet对Imagenet的训练与评测](https://blog.csdn.net/gzroy/article/details/87652291?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-21.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-21.nonecase)
* [ImageNet训练完整流程](https://blog.csdn.net/SrdLaplace/article/details/82194366?ops_request_misc=&request_id=&biz_id=102&utm_term=imagenet&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-4-82194366)
* [How to prepare Imagenet dataset for Image Classification](http://www.adeveloperdiary.com/data-science/computer-vision/how-to-prepare-imagenet-dataset-for-image-classification/)
* [Working with ImageNet (ILSVRC2012) Dataset in NVIDIA DIGITS](https://jkjung-avt.github.io/ilsvrc2012-in-digits/)
* [下载imagenet2012数据集，以及label说明](https://www.cnblogs.com/zjutzz/p/6083201.html)
* [建立自己的YOLO辨識模型 – 以柑橘辨識為例](https://chtseng.wordpress.com/2018/09/01/%E5%BB%BA%E7%AB%8B%E8%87%AA%E5%B7%B1%E7%9A%84yolo%E8%BE%A8%E8%AD%98%E6%A8%A1%E5%9E%8B-%E4%BB%A5%E6%9F%91%E6%A9%98%E8%BE%A8%E8%AD%98%E7%82%BA%E4%BE%8B/)
* [qqwweee/keras-yolo3](https://github.com/qqwweee/keras-yolo3)
* [使用faster rcnn训练imageNet上的部分数据集](https://www.itdaan.com/blog/2016/04/27/1fd1634f0fb40c788c50ff048f9cd723.html)
* [目标检测|YOLOv2原理与实现(附YOLOv3)](https://zhuanlan.zhihu.com/p/35325884)
* [标签："ImageNet"相关文章](https://www.codeleading.com/tag/ImageNet/)
* [How to reproduce ImageNet validation results](https://github.com/calebrob6/imagenet_validation)
