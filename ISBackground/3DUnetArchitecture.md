
# OPTIMIZATION OF TENSORFLOW FOR CPU IN IMAGE SEGMENTATION WITH 3D U-NET CNN WITH KERAS

## 3D Unet ARCHITECTURE

3D Unet structure consists of a contracting encoder section that analyses images to capture context and an expanding decoder section, producing full-resolution segmentations for precise localizations. It is end-to-end and trainable from few images, and consumes 3D volumes as inputs and processes them with 3D convolutions, max pooling, and op-convolutional.

Fig 2 is a representation of the U-net architecture, with the contracting section on the left and expanding on the right. Each box represents a multi-channel feature map with the number of channels shown above each box and the x-to-y numbers on their lower-left. Arrows indicate different operations. The contracting section’s architecture is typical of a convolutional network with the repeated application of two 3x3 unpadded convolutions, each of them followed by a ReLU and a 2x2 max pooling operation with stride 2 for downsampling. At each downsampling step, we double the number of feature channels. The expansive path contains an upsampling of the feature map, a 2x2 convolution that divides the number of feature channels in two, a concatenation (with the correspondingly cropped feature map from the contracting path), and two 3x3 convolutions, each followed by a ReLU. The cropping is necessary because of the loss of border pixels at every convolution. At the final layer, a 1x1 convolution maps each 64-component feature vector to the desired number of classes. In total, the model contains 23 convolutional layers. It is essential to select the input tile size such that all 2x2 max-pooling operations are applied to a layer with an even x- and y-size to allow a seamless tiling of the output segmentation.


![Architecture](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/ISBacground.PNG)
