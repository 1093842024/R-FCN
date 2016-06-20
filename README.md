# *R-FCN*: Object Detection via Region-based Fully Convolutional Networks

By Jifeng Dai, Yi Li, Kaiming He, Jian Sun

### Introduction

**R-FCN** is a region-based object detection framework leveraging deep fully-convolutional networks, which is accurate and efficient. In contrast to previous region-based detectors such as Fast/Faster R-CNN that apply a costly per-region sub-network hundreds of times, our region-based detector is fully convolutional with almost all computation shared on the entire image. R-FCN can natually adopt powerful fully convolutional image classifier backbones, such as [ResNets](https://github.com/KaimingHe/deep-residual-networks), for object detection.

R-FCN was initially described in an [arxiv tech report](https://arxiv.org/abs/1605.06409).

This code has been tested on Windows 7/8 64 bit, Windows Server 2012 R2, and Ubuntu 14.04, with Matlab 2014a.

### License

R-FCN is released under the MIT License (refer to the LICENSE file for details).

### Citing R-FCN

If you find R-FCN useful in your research, please consider citing:

    @article{dai16rfcn,
        Author = {Jifeng Dai, Yi Li, Kaiming He, Jian Sun},
        Title = {{R-FCN}: Object Detection via Region-based Fully Convolutional Networks},
        Journal = {arXiv preprint arXiv:1605.06409},
        Year = {2016}
    }

### Main Results
                   | training data       | test data             | mAP   | time/img (K40) | time/img (Titian X)
-------------------|:-------------------:|:---------------------:|:-----:|:--------------:|:------------------:|
R-FCN, ResNet-50L  | VOC 07+12 trainval  | VOC 07 test           | 77.0% | 0.12sec        | 0.09sec            |
R-FCN, ResNet-101L | VOC 07+12 trainval  | VOC 07 test           | 79.5% | 0.17sec        | 0.12sec            |


### Requirements: software

0. `Caffe` build for R-FCN (included in this repository, see `external/caffe`)
    - If you are using Windows, you may download a compiled mex file by running `fetch_data/fetch_caffe_mex_windows_vs2013_cuda75.m`
    - If you are using Linux or you want to compile for Windows, please recompile [our Caffe branch](https://github.com/daijifeng001/caffe-rfcn).
0.	MATLAB 2014a or later
 
    
### Requirements: hardware

GPU: Titan, Titan X, K40, K80.

### Demo:
0.	Run `fetch_data/fetch_caffe_mex_windows_vs2013_cuda75.m` to download a compiled Caffe mex (for Windows only).
0.	Run `fetch_data/fetch_demo_model_ResNet101.m` to download a R-FCN model using ResNet-101L net (trained on VOC 07+12 trainval).
0.	Run `rfcn_build.m`.
0.	Run `startup.m`.
0.	Run `experiments/script_rfcn_demo.m` to apply the R-FCN model on demo images.

### Preparation for Training & Testing:
0.	Run `fetch_data/fetch_caffe_mex_windows_vs2013_cuda75.m` to download a compiled Caffe mex (for Windows only).
0.	Run `fetch_data/fetch_model_ResNet50.m` to download an ImageNet-pre-trained ResNet-50L net.
0.	Run `fetch_data/fetch_model_ResNet101.m` to download an ImageNet-pre-trained ResNet-101L net.
0.	Run `fetch_data/fetch_region_proposals.m` to download the pre-computed region proposals.
0.	Download VOC 2007 and 2012 data to ./datasets.
0.	Run `rfcn_build.m`.
0.	Run `startup.m`.


### Training & Testing:
0. Run `experiments/script_rfcn_VOC0712_ResNet50_OHEM_ss.m` to train a model using ResNet-50L net with online hard example mining (OHEM), leveraging selective search proposals. The accuracy should be ~75.4% in mAP.
    - **Note**: the training time is ~13 hours on Titian X.
0. Run `experiments/script_rfcn_VOC0712_ResNet50_OHEM_rpn.m` to train a model using ResNet-50L net with OHEM, leveraging RPN proposals (using ResNet-50L net). The accuracy should be ~77.0% in mAP.
    - **Note**: the training time is ~13 hours on Titian X.
0. Run `experiments/script_rfcn_VOC0712_ResNet101_OHEM_rpn.m` to train a model using ResNet-101L net with OHEM, leveraging RPN proposals (using ResNet-101L net). The accuracy should be ~79.5% in mAP.
    - **Note**: the training time is ~19 hours on Titian X.
0. Check other scripts in `./experiments` for more settings.

**Note:** In all the experiments, training is performed on VOC 07+12 trainval, and testing is performed on VOC 07 test. Running time is not recorded in the test log (which is slower), but instead in an optimized implementation.

### Resources

0. Experiment logs: [DropBox](https://www.dropbox.com/s/is2gatfdxs1tcls/experiment_log.zip?dl=0), [BaiduYun](http://pan.baidu.com/s/1mhFYejI)

If the automatic "fetch_data" fails, you may manually download resouces from:

0. Pre-complied caffe mex (Windows):
    - [DropBox](https://www.dropbox.com/s/n1x2bybd6d03s7c/caffe_mex.zip?dl=0), [BaiduYun](http://pan.baidu.com/s/1i4OlG7z)
0. Demo R-FCN model:
    - [DropBox](https://www.dropbox.com/s/1cvg8ke9nuo9vg3/demo_models_ResNet-101L.zip?dl=0), [BaiduYun](http://pan.baidu.com/s/1bpv8fgz)
0. ImageNet-pretrained networks:
    - ResNet-50L net [DropBox](https://www.dropbox.com/s/0uzh90f6jx9l0yf/models_ResNet-50L.zip?dl=0), [BaiduYun](http://pan.baidu.com/s/1kVm4ly3)
    - ResNet-101L net [DropBox](https://www.dropbox.com/s/ev91ss0pyd5h9ix/models_ResNet-101L.zip?dl=0), [BaiduYun](http://pan.baidu.com/s/1nvgu1pJ)
0. Pre-computed region proposals:
    - [DropBox](https://www.dropbox.com/s/gagkulgcif6k1dd/proposals.zip?dl=0), [BaiduYun](http://pan.baidu.com/s/1nv1tkH7)


