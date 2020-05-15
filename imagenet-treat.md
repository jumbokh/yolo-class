## imagenet data treatment
### [ImageNet数据集下载与处理](https://zhuanlan.zhihu.com/p/42696535)
* Training images (Task 1 & 2). 138GB.
* Validation images (all tasks). 6.3GB.
* Training bounding box annotations (Task 1 & 2 only). 20MB.
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
### 連結
* [ImageNet数据集下载与处理](https://zhuanlan.zhihu.com/p/42696535)
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

