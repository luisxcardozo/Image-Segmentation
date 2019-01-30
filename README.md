# <p align="center">HOW TO OPTIMIZE IMAGE SEGMENTATION WITH 3D U-NET IN TENSORFLOW* FOR CPU

<p align="center">Yiqiang Li<sup>1</sup>, Wenxi Zhu<sup>1</sup>, Shankar Ratneshwaran<sup>2</sup>, Kevin Bryan<sup>2</sup>, Luis Cardozo<sup>2</sup>

- 1 - Developer Product Division Machine Learning Translator - Shangai, Intel
- 2 - Artificial Intelligence Center For Excellence at Intel – Santa Clara, TCS

### GOAL
Learn CPU performance optimizations for image segmentation with 3d-UNet optimizations by:
1.	Optimizing Tensorflow* to run faster on CPU;
2.	Eliminating technology driven bottlenecks.




### ABSTRACT  
5.4x improvement on inference performance on Intel® 8180 by solving architecture bottlenecks by leveraging Intel®’s highly optimized math routines for deep learning and Tensorflow* CPU optimization. For volumetric segmentation in medical imaging with 3D Unet with Keras*, on Intel® Xeon® processor-based platforms. 

Intel®’s primitives library is called Intel® Math Kernel Library for Deep Neural Networks (MKL-DNN) and includes convolution, normalization, activation and inner product, and other primitives, and by reviewing bottleneck opportunities within the model’s sections. These steps are highly relevant as recent academic articles predict the development of non-static neural networks that increase memory and computational requirements, especially where accuracy minimization is paramount, like in the bio-med industry.


KEYWORDS. Convolutional Neural Networks, Biomedical Volumetric Image Segmentation, Ten-sorflow Optimization,

### [BACKGROUND](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/ISBackground.md)         
### [ARCHITECTURE](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/3DUnetArchitecture.md)

#### Evaluation Environment

|  |  | 
| :---         | :---        | 
|HW   | Xeon Platinum 8180, @2.5G Turbo on, HT on, NUMA     |
| OS    | CentOS Linux 7 (Core)  kernel 3.10.0-693.el7.x86_64       |
| Tensorflow   | v1.8rc1, commit id: 2dc7357    |
| Keras  | v2.1.5      |
| MKLDNN   | v0.13  |
| Model	3D-UNet | (https://github.com/ellisdg/3DUnetCNN ) |
| Dataset | BraTS (http://www.med.upenn.edu/sbia/brats2017.html) |
| CMD (inference)| $python predict.py|
| BS | 1 |
|Python| [3.6](https://www.python.org/downloads/)|




## Step 1. Getting started and determining baseline.

Download CPU optimized Tensorflow from:
- [Guide](https://software.intel.com/en-us/articles/intel-optimization-for-tensorflow-installation-guide), or 
- [Build](https://github.com/tensorflow/tensorflow/#community-supported-builds) *(Linux CPU with Intel® MKL-DNN Nightly)*
/  



[Guide to 3D U-Net Convolution Neural Network with Keras](https://github.com/ellisdg/3DUnetCNN) *(includes pre-trained models)*

Note: when installing ANTs ([ANTs version 2.1.0](https://github.com/ANTsX/ANTs/releases/tag/v2.1.0)), download the Linux_Debbien_jessie_x64_tar.bz2 package

also, instructions to install pytable and nipype dependencies.
- pytable: $pip install tables
- nipype:  $pip install nipype 

<img align="right" width="359" height="82" src="https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/3DUNET%20Throughput%20Baseline.PNG"> 
The first run determines a benchmark that would allow measuring optimization attempts. Results represented in the following table.  




## Step 2. Bottleneck analysis.
Performing an inference time breakdown indicates that transpose operations create an overhead that corresponds to 34% of total inference execution time caused by Keras* structure.

[Profiling code for 3D-Unet bottleneck diagnosis](https://github.com/NervanaSystems/tensorflow-3DUNet/blob/master/brats/predict.py#L29) and [Profiler (*with demo and tutorials*)](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/core/profiler/README.md#features)

![Inference Time breakdown](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/Inference%20Time%20Breakdown.PNG)



The Keras* driven overhead was eliminated by following this [step-by-step guide (with background)](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/Keras_background.md)

# RESULTS
Our engineers designed the elimination of inefficiencies in stages. Results shown in the following table.


| Optimization Step | Throughput (Image/sec) | Performance Improvement |
| :---         |     :---:      |    :---:      |
|Baseline   | (ip)     |     |
| Optimized TensorFlow*     | .035       | tbd     |
| Integrate Conv3D    | .050      | 1.43X      |
| Integrate Deconv3D  | .068       | 1.94X     |
| Overhead Removal   | **.189**      | **5.4X**      |

# CONCLUSION
The optimization of TensorFlow* allows for deep-learning models built for this common framework to run several magnitudes faster on Intel® processors to increase scaling and analytical flexibility. The Xeon® processor is designed to scale comfortably to reduce training time of machine learning models. The collaboration between Intel® and Google* engineers to optimize TensorFlow* for higher performance on CPUs is part of ongoing efforts to increase the flexibility of AI applications by running on multiple mediums. Intel® believes the expansion of this accessibility is critical in the development of the next generation of AI models, and our efforts shed light into this by obtaining a 5.4x performance improvement with Intel® Xeon® Platinum 8180®. 





