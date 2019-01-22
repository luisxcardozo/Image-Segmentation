#                             HOW TO OPTIMIZE IMAGE SEGMENTATION WITH 3D U-NET IN TENSORFLOW* FOR CPU

Yiqiang Li1, Wenxi Zhu1, Shankar Ratneshwaran2, Kevin Bryan2, Luis Cardozo2

- 1 Developer Product Division Machine Learning Translator - Shangai, Intel
- 2 Artificial Intelligence Center For Excellence at Intel – Santa Clara, TCS

### GOAL
This tutorial will introduce you to CPU performance optimizations for image segmentation with 3d-UNet and Intel’s TensorFlow* optimizations.
This guide will provide performance improvements by:
1.	Means to optimize Tensorflow* to run faster on CPU;
2.	Ways to eliminate technology driven bottlenecks.


### ABSTRACT  
Tensorflow* CPU optimization for volumetric segmentation in medical imaging with 3D Unet with Keras, on Intel® Xeon® processor-based platforms. 5.4x improvement in performance for training on Intel 8180 against an unoptimized run by solving bottlenecks within the network architecture. 
Models’ performance are optimized by leveraging Intel’s highly optimized math routines for deep learning. This primitives library is called Intel Math Kernel Library for Deep Neural Networks (Intel MKL-DNN) and includes convolution, normalization, activation and inner product, and other primi-tives and by reviewing bottleneck opportunities within the model’s sections. These steps are high-ly relevant as recent academic articles predict the development of non-static neural networks that increase memory and computational requirements, especially where accuracy minimization is paramount, like in the bio-med industry.
KEYWORDS. Convolutional Neural Networks, Biomedical Volumetric Image Segmentation, Ten-sorflow Optimization,

### [BACKGROUND](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/ISBackground.md)         
### [ARCHITECTURE](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/3DUnetArchitecture.md)

#### Evaluation Environment

- HW	          Xeon Platinum 8180, @2.5G Turbo on, HT on, NUMA
- OS	          CentOS Linux 7 (Core)  kernel 3.10.0-693.el7.x86_64
- Tensorflow	  v1.8rc1, commit id: 2dc7357
- Keras	        v2.1.5
- MKLDNN	      v0.13
- Model	3D-UNet (https://github.com/ellisdg/3DUnetCNN )
- Dataset	BraTS (http://www.med.upenn.edu/sbia/brats2017.html)
- CMD (inference)	$python predict.py
- BS	1


## 1. Getting started.
Follow the guide to access and download the BRATS dataset, and prepare the data for training.
- Guide: [3D U-Net Convolution Neural Network with Keras](http://github.com/nervanasystem/tensorflow-3dunet) (*needs to be opened*)

## 2. Determining benchmark.
Step 6 of the guide recommends to run the improved UNet model

```
$ python train_isensee2017.py
```

If you encounter memory issues during training try setting   config['patch_shape`] = (64, 64, 64).

<img align="right" width="370" height="75" src="https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/Step_two.PNG"> 
The first run determines a benchmark that would allow measuring optimization attempts. Results represented in the following table.  


![Step_Two](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/Step_two.PNG)

# Step 3. Optimizing TensorFlow* for CPU.  
(*PERFORMANCE OPTIMIZATION*)
Intel developed specialized primitives libraries that increase Deep Neural Network model per-formance. This performance boost can be installed from Anaconda or from the Intel channel and run on Linux*, and on Windows* or OS*. 

- [Guide: Intel® Optimization for TensorFlow* Installation Guide](https://software.intel.com/en-us/articles/intel-optimization-for-tensorflow-installation-guide)

![Step Three](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/Step_three.PNG)

## Step 4. Bottleneck analysis.
Performing an inference time breakdown provided the following results:

![Inference Time breakdown](https://github.com/luisxcardozo/Image-Segmentation/blob/master/Inference%20Time%20Breakdown.PNG)

Indicating that transpose operations create an overhead that corresponds to 34% of total infer-ence execution time caused by Keras’ structure.

KERAS BACKGROUND (*include link*)

The Keras driven overhead was eliminated by following these steps:

1 A) ...  (ip)

# RESULTS
Our engineers designed the elimination of inefficiencies in stages. Results for single-socket are shown in the following table.

![Results](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/Results.PNG)

# CONCLUSION
The optimization of TensorFlow* allows for deep-learning models built for this common framework to run several magnitudes faster on Intel* processors to increase scaling and analytical flexibility. The Intel Xeon* processor is designed to scale comfortably to reduce training time of machine learning models. The collaboration between Intel and Google engineers to optimize TensorFlow* for higher performance on Intel* CPUs is part of ongoing efforts to increase the flexibility of AI ap-plications by running on multiple mediums. Intel* believes the expansion of this accessibility is critical in the development of the next generation of AI models, and our efforts shed light into this by obtaining a projected 5.4x performance improvement with Intel Xeon Platinum 8180* CPU. 





