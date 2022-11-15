# Cell Nuclei Segmentation from Breast Histopathology images using cGAN
## Overview
With improvements in computer vision techniques and hardware, some of the problems of manual assessment of histology images, such as inter and intra-observer variability, inability to assess subtle visual features, and the time
taken to examine whole slides are being alleviated by computational pathology.

### Data
The database consists of 50 large [512*512] image pairs and was split into 43 and 7 train and test sets. In order to feed the model with input images and the ground truth masks together, the histology images and corresponding segmentation maps are merged as shown below.
![alt text](https://github.com/babajide07/Cell-Nuclei-Segmentation-from-Histology-images-using-Conditional-Generative-Adversarial-Network-/blob/master/Results/Slide_11_11_2.png)

## Baseline
The baseline architecture was U-Net: [Convolutional Networks for Biomedical Image Segmentation](https://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/). The model was trained for 200 epochs using binary crossentropy loss. The dice similarity coefficient was 0.637. Since the database is relatively small for training a deep neural network model, I tried on-the-fly data augmentation by randomly rotating and flipping both input image and the segmentation map during training. The performance improved by 9% as a result of this augmentation.

## cGAN-based Segmentation (Res-UNet++)
In order to improve the performance, I designed a custom conditional Generative Adversarial Network (cGAN) shown below. The generator design follows the encoder-decoder structure with skip-connections and residual blocks. I adapted the
Res-UNet++ architecture as a basis for my work.
![alt text](https://github.com/jainaviral898/Cell-Nuclei-Segmentation-using-cGAN/blob/master/images/resunet++_image.jpg)
The discriminator on the other hand uses patch information to resolve details in the prediction map. With cGAN, the dice similarity coefficient increases to 0.723.
## Results
Several metric functions like Dice, Jaccard, Haussdorf Distance were used to benchmark the performance. Values can be found out in [this document](https://github.com/jainaviral898/Cell-Nuclei-Segmentation-using-cGAN/blob/master/final%20results.pdf).

## Dependencies
 - [x] Pytorch >= 0.4.0
 - [x] Python >= 3.5
 - [x] Numpy
