# DSOD: Learning Deeply Supervised Object Detectors from Scratch


This repository contains the code for the following paper 

[DSOD: Learning Deeply Supervised Object Detectors from Scratch](http://openaccess.thecvf.com/content_ICCV_2017/papers/Shen_DSOD_Learning_Deeply_ICCV_2017_paper.pdf) (ICCV 2017).

[Zhiqiang Shen](http://www.zhiqiangshen.com)\*, [Zhuang Liu](https://liuzhuang13.github.io/)\*, [Jianguo Li](https://sites.google.com/site/leeplus/), [Yu-Gang Jiang](http://www.yugangjiang.info/), [Yurong chen](https://scholar.google.com/citations?user=MKRyHXsAAAAJ&hl=en), [Xiangyang Xue](https://scholar.google.com/citations?user=DTbhX6oAAAAJ&hl=en). (\*Equal Contribution)

The code is based on the [SSD](https://github.com/weiliu89/caffe/tree/ssd) framework. 

Other Implementations:
[[Pytorch]](https://github.com/chenyuntc/dsod.pytorch) by Yun Chen, [[Pytorch]](https://github.com/uoip/SSD-variants) by uoip, [[Pytorch]](https://github.com/qqadssp/DSOD-Pytorch) by qqadssp, [[Pytorch]](https://github.com/Ellinier/DSOD-Pytorch-Implementation) by Ellinier , [[Mxnet]](https://github.com/leocvml/DSOD-gluon-mxnet) by Leo Cheng, [[Mxnet]](https://github.com/eureka7mt/mxnet-dsod) by eureka7mt, [[Tensorflow]](https://github.com/Windaway/DSOD-Tensorflow) by Windaway.


If you find this helps your research, please cite:

	@inproceedings{Shen2017DSOD,
		title = {DSOD: Learning Deeply Supervised Object Detectors from Scratch},
		author = {Shen, Zhiqiang and Liu, Zhuang and Li, Jianguo and Jiang, Yu-Gang and Chen, Yurong and Xue, Xiangyang},
		booktitle = {ICCV},
		year = {2017}
	}

## Introduction

DSOD focuses on the problem of training object detector from scratch (without pretrained models on ImageNet). 
To the best of our knowledge, this is the first work that trains neural object detectors from scratch with state-of-the-art performance. 
In this work, we contribute a set of design principles for this purpose. One of the key findings is the deeply supervised structure enabled by [dense layer-wise connections](https://github.com/liuzhuang13/DenseNet), plays a critical role in learning a good detection model. Please see our paper for more details.

<div align=center>
<img src="https://user-images.githubusercontent.com/3794909/47568639-3d1bf700-d964-11e8-824e-f46026c665c6.png" width="740">
</div>

<div align=center>
Figure 1: DSOD prediction layers with plain and dense structures (for 300×300 input).
</div> 

## Visualization

0. Visualizations of network structures (tools from [ethereon](http://ethereon.github.io/netscope/quickstart.html), ignore the warning messages):
	- [DSOD300] (http://ethereon.github.io/netscope/#/gist/b17d01f3131e2a60f9057b5d3eb9e04d)

## Results & Models

The tables below show the results on PASCAL VOC 2007, 2012 and MS COCO.

PASCAL VOC test results:

| Method | VOC 2007 test *mAP* | fps (Titan X) | # parameters | Models 
|:-------|:-----:|:-------:|:-------:|:-------:|
| DSOD300_smallest (07+12) | 73.6 | - | 5.9M | [Download (23.5M)](https://drive.google.com/open?id=0B4cvsEOB5eUCNXZ3eWNRNHZTdFk) |
| DSOD300_lite (07+12) | 76.7 | 25.8 | 10.4M | [Download (41.8M)](https://drive.google.com/open?id=0B4cvsEOB5eUCQVozLVhONS1EX2s) |
| DSOD300 (07+12) | 77.7 | 17.4 | 14.8M | [Download (59.2M)](https://drive.google.com/open?id=0B4cvsEOB5eUCaGU3MkRkOENRWWc) |
| DSOD300 (07+12+COCO) | 81.7 | 17.4 | 14.8M | [Download (59.2M)](https://drive.google.com/open?id=0B4cvsEOB5eUCa3lDWTNIa1BfMUU)|

| Method | VOC 2012 test *mAP* | fps | # parameters| Models 
|:-------|:-----:|:-----:|:-------:|:-------:|
| DSOD300 (07++12) | 76.3 | 17.4 | 14.8M | [Download (59.2M)](https://drive.google.com/open?id=0B4cvsEOB5eUCV2cyeU9qZVlhSEk) |
| DSOD300 (07++12+COCO) | 79.3 | 17.4 | 14.8M | [Download (59.2M)](https://drive.google.com/open?id=0B4cvsEOB5eUCLXhGdlUtT3B2cDQ) |

COCO test-dev 2015 result (COCO has more object categories than VOC dataset, so the model size is slightly bigger.):

| Method | COCO test-dev 2015 *mAP* (IoU 0.5:0.95) | Models
|:-------|:-----:|:-----:|
| DSOD300 (COCO trainval) | 29.3 | [Download (87.2M)](https://drive.google.com/open?id=0B4cvsEOB5eUCYXoxcGRCbVFMNms) |

## Preparation 

0. Install SSD (https://github.com/weiliu89/caffe/tree/ssd) following the instructions there, including: (1) Install SSD caffe; (2) Download PASCAL VOC 2007 and 2012 datasets; and (3) Create LMDB file. Make sure you can run it without any errors.

	Our PASCAL VOC LMDB files:
	
	| Method | LMDBs
	|:-------|:-----:|
	| Train on VOC07+12 and test on VOC07  | [Download](https://drive.google.com/open?id=1u6ngM9hEZabT2HyvzPdWpGgVTofD6jQ3) |
	| Train on VOC07++12 and test on VOC12 (Comp4)  | [Download](https://drive.google.com/open?id=1J2epI4zDFptw1RdpHAl0Z_Sphs14OtIE) |
	| Train on VOC12 and test on VOC12 (Comp3)  | [Download](https://drive.google.com/open?id=1r5DI3tVGXPYyKGAmBawKGkgROJQyh5i-) |

1. Create a subfolder `dsod` under `example/`, add files `DSOD300_pascal.py`, `DSOD300_pascal++.py`, `DSOD300_coco.py`, `score_DSOD300_pascal.py` and `DSOD300_detection_demo.py` to the folder `example/dsod/`.
2. Create a subfolder `grp_dsod` under `example/`, add files `GRP_DSOD320_pascal.py` and `score_GRP_DSOD320_pascal.py` to the folder `example/grp_dsod/`.
3. Replace the file `model_libs.py` in the folder `python/caffe/` with ours.

## Training & Testing

- Train a DSOD model on VOC 07+12:

  ```shell
  python examples/dsod/DSOD300_pascal.py
  ```

- Train a DSOD model on VOC 07++12:

  ```shell
  python examples/dsod/DSOD300_pascal++.py
  ```
  
- Train a DSOD model on COCO trainval:

  ```shell
  python examples/dsod/DSOD300_coco.py
  ```
  
- Evaluate the model (DSOD):

  ```shell
  python examples/dsod/score_DSOD300_pascal.py
  ```
  
- Run a demo (DSOD):

  ```shell
  python examples/dsod/DSOD300_detection_demo.py
  ```
  
- Train a GRP_DSOD model on VOC 07+12:

  ```shell
  python examples/grp_dsod/GRP_DSOD320_pascal.py
  ```
  
- Evaluate the model (GRP_DSOD):

  ```shell
  python examples/dsod/score_GRP_DSOD320_pascal.py
  ```
  
 **Note**: You can modify the file `model_lib.py` to design your own network structure as you like.

## Examples

<div align=center>
<img src="https://cloud.githubusercontent.com/assets/3794909/25331405/92d88c36-2915-11e7-93f3-3eb43963f5ac.jpg" width="780">
</div>

## Contact

Zhiqiang Shen (zhiqiangshen0214 at gmail.com) 

Zhuang Liu (liuzhuangthu at gmail.com)

Any comments or suggestions are welcome!
