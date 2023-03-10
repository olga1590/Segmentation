# Classification and segmentation of defective parts

## What is image segmentation?
- The goal of image segmentation is to understand and extract information from images at the pixel-level.
- Image Segmentation can be used for object recognition and localization which offers tremendous value in many applications such as medical imaging and self-driving cars and etc.
- The goal of image segmentation is to train a neural network to produce pixel-wise mask of the image. 


In this notebook I've used ResUnet.
In case of Unet we convert(encode) the image into a vector followed by a sampling(decode) it back again into an image.
The input and output have the same size so the size of image is preserved.

<img width="758" alt="Снимок экрана 2023-03-10 в 8 41 53 PM" src="https://user-images.githubusercontent.com/102851931/224307280-4ef5b475-4667-4377-a5a7-e0491affad79.png">

ResUNet architecture combines UNet backbone architecture with residual blocks to overcome the vanishing gradients problems present in deep architectures.

U-Net consists of Convolution Operation, Max Pooling, ReLU Activation, Concatenation and Up Sampling Layers and three sections: 
1) encoder of contracting path, 
2) bottleneck, and 
3) decoder or expansive path. 

The contractions section has 4 contraction blocks. Every contraction block gets an input, applies two 3X3 convolution ReLu layers and then a 2X2 max pooling. The number of feature maps gets double at each pooling layer. 

The bottleneck layer uses two 3X3 Conv layers and 2X2 up convolution layer. 

The expansion section consists of several expansion blocks with each block passing the input to two 3X3 Conv layers and a 2X2 upsampling layer that halves the number of feature channels. It also includes a concatenation with the correspondingly cropped feature map from the contracting path. In the end, 1X1 Conv layer is used to make the number of feature maps as same as the number of segments which are desired in the output. U-net uses a loss function for each pixel of the image. 

This helps in easy identification of individual cells within the segmentation map. Softmax is applied to each pixel followed by a loss function. This converts the segmentation problem into a classification problem where we need to classify each pixel to one of the classes.

source: https://medium.com/@aditi-mittal/introduction-to-u-net-and-res-net-for-image-segmentation-9afcb432ee2f

