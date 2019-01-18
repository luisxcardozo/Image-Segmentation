# HOW TO OPTIMIZE IMAGE SEGMENTATION WITH 3D U-NET 
IN TENSORFLOW* FOR CPU

Yiqiang Li1, Wenxi Zhu1, Shankar Ratneshwaran2, Kevin Bryan2, Luis Cardozo2

1 Developer Product Division Machine Learning Translator - Shangai, Intel
2 Artificial Intelligence Center For Excellence at Intel – Santa Clara, TCS

GOAL
This tutorial will introduce you to CPU performance optimizations for image segmentation with 3d-UNet and Intel’s TensorFlow* optimizations.
This guide will provide performance improvements by:
1.	Means to optimize Tensorflow* to run faster on CPU;
2.	Ways to eliminate technology driven bottlenecks.


ABSTRACT  
Tensorflow* CPU optimization for volumetric segmentation in medical imaging with 3D Unet with Keras, on Intel® Xeon® processor-based platforms. 5.4x improvement in performance for training on Intel 8180 against an unoptimized run by solving bottlenecks within the network architecture. 
Models’ performance are optimized by leveraging Intel’s highly optimized math routines for deep learning. This primitives library is called Intel Math Kernel Library for Deep Neural Networks (Intel MKL-DNN) and includes convolution, normalization, activation and inner product, and other primi-tives and by reviewing bottleneck opportunities within the model’s sections. These steps are high-ly relevant as recent academic articles predict the development of non-static neural networks that increase memory and computational requirements, especially where accuracy minimization is paramount, like in the bio-med industry.
KEYWORDS. Convolutional Neural Networks, Biomedical Volumetric Image Segmentation, Ten-sorflow Optimization,

BACKGROUND
ARCHITECTURE

Evaluation Environment
HW / SW Configuration
HW	Xeon Platinum 8180, @2.5G Turbo on, HT on, NUMA
OS	CentOS Linux 7 (Core)  kernel 3.10.0-693.el7.x86_64
Tensorflow	v1.8rc1, commit id: 2dc7357
Keras	v2.1.5
MKLDNN	v0.13
Model	3D-UNet (https://github.com/ellisdg/3DUnetCNN )

Dataset	BraTS (http://www.med.upenn.edu/sbia/brats2017.html)

CMD (inference)	$python predict.py
BS	1

