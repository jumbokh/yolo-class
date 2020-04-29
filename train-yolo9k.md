## Trainning YOLO9000 using COCO dataset
### Descp
<pre>
You should have your own 6 files, as described here: https://github.com/AlexeyAB/darknet#using-yolo9000
For example, for 2 classes (aircraft, birds) - you should have these files
data.zip (https://github.com/pjreddie/darknet/files/1689246/data.zip)

Then you should download weights file: http://pjreddie.com/media/files/yolo9000.weights
And you should get pre-trained file: darknet.exe partial yolo9000.cfg yolo9000.weights yolo9000.conv.22 22

Then you should start to train yolo9000:
darknet detector train data/air9k.data yolo9000_air.cfg yolo9000.conv.22

All other steps are the same as when training a regular model of Yolo v2.
</pre>
### Get Started
<pre>
git clone --recursive https://github.com/philipperemy/yolo-9000.git
cd yolo-9000
cat yolo9000-weights/x* > yolo9000-weights/yolo9000.weights # it was generated from split -b 95m yolo9000.weights
cd darknet 
make # Will run on CPU. For GPU support, scroll down!
./darknet detector test cfg/combine9k.data cfg/yolo9000.cfg ../yolo9000-weights/yolo9000.weights data/horses.jpg
</pre>
### Instruction
<pre>
同時檢測和分類9000個對象：

yolo9000.weights-（186 MB Yolo9000型號）需要4 GB GPU-RAM：http：//pjreddie.com/media/files/yolo9000.weights

yolo9000.cfg-Yolo9000的cfg文件，也有指向9k.tree和https://github.com/AlexeyAB/darknet/blob/617cf313ccb1fe005db3f7d88dec04a04bd97cc2/cfg/yolo9000.cfg#L217-L218的路徑coco9k.map

9k.tree- WordTree的9418範疇- <label> <parent_it>如果parent_id == -1然後該標籤還沒有父：https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.tree

coco9k.map-將80種類別從MSCOCO映射到WordTree 9k.tree：https : //raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/coco9k.map

combine9k.data-數據文件，也有路徑：9k.labels，9k.names，inet9k.map，（改變路徑到你combine9k.train.list）：https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/combine9k.data

9k.labels-9418個對象的標籤：https ://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.labels

9k.names-9418個對象的名稱：https ://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.names

inet9k.map-將200個類別從ImageNet映射到WordTree 9k.tree：https : //raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/inet9k.map

</pre>
### Download COCO dataset
<pre>
You can train YOLO from scratch if you want to play with different training regimes, hyper-parameters, or datasets. Here's how to get it working on the COCO dataset.

Get The COCO Data
To train YOLO you will need all of the COCO data and labels. 
The script scripts/get_coco_dataset.sh will do this for you. 
Figure out where you want to put the COCO data and download it, 
for example:

cp scripts/get_coco_dataset.sh data
cd data
bash get_coco_dataset.sh
</pre>
### Modify cfg for COCO
* Now go to your Darknet directory. We have to change the cfg/coco.data config file to point to your data:
<pre>
 1 classes= 80
  2 train  = <path-to-coco>/trainvalno5k.txt
  3 valid  = <path-to-coco>/5k.txt
  4 names = data/coco.names
  5 backup = backup
</pre>
*You should replace <path-to-coco> with the directory where you put the COCO data.
* You should also modify your model cfg for training instead of testing. cfg/yolo.cfg should look like this:
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
### Train The Model (for darknet53)
* Now we can train! Run the command:
    * ./darknet detector train cfg/coco.data cfg/yolov3.cfg darknet53.conv.74
 * using GPU:
    * ./darknet detector train cfg/coco.data cfg/yolov3.cfg darknet53.conv.74 -gpus 0,1,2,3
    * ./darknet detector train cfg/coco.data cfg/yolov3.cfg darknet53.conv.74 -i 0
 * stop and continue: (CTRL-C to stop)
     * ./darknet detector train cfg/coco.data cfg/yolov3.cfg backup/yolov3.backup -gpus 0,1,2,3
 ##
 #### The files need for train YOLO9000
 * ![y9k](https://github.com/jumbokh/yolo-class/blob/master/images/y9kfiles.jpg)
 <pre>
 
 </pre>
 
