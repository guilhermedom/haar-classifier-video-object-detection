# Haar Classifier Video Object Detection

Haar cascade classifiers detecting cars and persons in videos with OpenCV.

---

## Problem Overview

One of the main challenges in the [computer vision] field has been working with videos. Essentially being methods of processing sequences of images, video processing demands a lot more resources than regular image processing. A video of just one second may contain more than 100 images in sequence, depending on the frame rate. Long before the computer vision field was dominated by [convolutional neural networks] (CNNs), other image processing mechanisms were already developed trying to reduce the amount of resources needed to detect objects in images. One relevant example is the Haar cascade classifier.

A [Haar cascade classifier] is composed of a sequence of haar filters that aim to identify patterns in images. These filters go through the image as sliding windows, in a similar operation to the one performed by the convolutions of CNNs. They summarize variations in pixel color intensity on different image regions. With this summary, it is possible to efficiently compare any region of an image with any other summaries that represent a desired pattern. If the region has a particular pattern of intensity variation, this region goes through a series of haar filters to check if that pattern is indeed the searched pattern. Since we are talking about classifiers, they need to be trained to learn the pattern of interest. Usually, thousands of small variations of filters are put in sequence to form the cascade. The next figure has an illustration on the Haar classifier process. It shows some of these filters, basically matrices, where the black and white portions are being compared against each other to check for changes in pixel intensity:

![facial_feature_haar_detection_haar_features](https://user-images.githubusercontent.com/33037020/202063850-62ed2da9-1ac1-471b-a006-fa932b5c29a6.PNG)

## Analysis Introduction

Being highly optimized, Haar cascade classifiers were the way to go for many years since [its proposal in 2001]. Many camera algorithms used to adjust focus were based on this solution, since the camera hardware needed a fast method to find faces, the object of interest in the image. In this analysis, we work with two pretrained Haar cascade classifiers, on a [transfer learning] fashion, where we load the pretrained classifiers using OpenCV's [CascadeClassifier class]. One classifier looks for persons on a video. The other looks for cars on another video. [OpenCV] is the backbone of this project as we use many of its functions to handle the videos during the whole process.

While struggling with false positives, we were able to fine tune our method's parameters to detect almost all persons and cars, in their respective videos. The training process of the Haar classifiers are not discussed in the notebook for this repository, only their usage and tuning. Therefore, the parameters we fit are not training parameters but rather image processing parameters, namely the image scale factor and the minimum number of candidate neighbors every candidate region needs to have. A candidate is a region of the image that was classified as having the object.

In the end, the classifiers were able to achieve reasonable success not only detecting the objects in the videos but also tracking them as they move in the scene. In the notebook, we briefly discuss some challenges, such as image quality, artifacts on the images and object scales. These issues were mostly worked around using just parameter adjustments. This highlights the quality of this classical image processing algorithm that was a standard for many years.

![haar_classifier_video_object_detection_car_traffic](https://user-images.githubusercontent.com/33037020/202064173-70b090ed-95ed-45b2-bb9c-fd7a1be08c55.gif)

[//]: #

[computer vision]: <https://www.ibm.com/topics/computer-vision>
[haar cascade classifier]: <https://docs.opencv.org/3.4/db/d28/tutorial_cascade_classifier.html>
[transfer learning]: <https://en.wikipedia.org/wiki/Transfer_learning>
[convolutional neural networks]: <https://www.ibm.com/cloud/learn/convolutional-neural-networks>
[its proposal in 2001]: <https://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/viola-cvpr-01.pdf>
[CascadeClassifier class]: <https://docs.opencv.org/3.4/db/d28/tutorial_cascade_classifier.html>
[OpenCV]: <https://opencv.org>
