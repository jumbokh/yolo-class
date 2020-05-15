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

