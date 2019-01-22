
# OPTIMIZATION OF TENSORFLOW FOR CPU IN IMAGE SEGMENTATION WITH 3D U-NET CNN WITH KERAS

## IMAGE SEGMENTATION BACKGROUND

Image Segmentation is the process of partitioning digital images into many segments by clustering pixels into particular image sections in such a way that it simplifies analyses. This process allows identification of defined objects and their boundaries and facilitates classification exercises. Uses include Object Detection (like identification of objects from satellite imagery), Recognition (such as facial recognition), Video Surveillance, and Medical Imaging. 

Today, CNN compete in image segmentation with human Subject Matter Experts, leading to the development of neural nets applied to 3D imaging. The development of 3D CNN has varied approaches. The work performed by Milletari et al., although limited to compact structures and not requiring a pre-trained network, utilizes a CNN combined with the Hough Voting approach. Kleesiak et al.’s approach, while it is end-to-end, it is not a deep network and unable to analyze structures at multiple scales. Our intent is the optimization of Tensorflow to run a 3D U-net architecture on an Intel 8180.

Although in many Bio-med cases a small number of images are sufficient to train a neural network, today’s greater need of granularity makes preprocessing complex. It is common to see images greater than 300 MB, and feeding a file this size to a neural net is engrossed and memory inefficient. So preprocessing on common databases, like LIDC-IDRI, may take up to, or exceed, 24 hrs, depending on the platform.

Fig 1 represents how the volumetric segmentation process with a 3D U-net architecture works. In the first step, the analyst annotates the volumes for segmentation (a), and then the network performs a fully-automated segmentation based pm a representative training set (b).

![Image Segmentation Process](https://github.com/luisxcardozo/Image-Segmentation/blob/master/ISBackground/ISBacground.PNG)
