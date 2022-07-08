---
title: 'Super Resolution Series II'
date: 2022-02-10
permalink: /blogs/VideoSuperRes
author_profile: false
tags:
  - hkust
---
By Hong

In my previous [post](https://hong-yc.github.io/blogs/superRes), I talk mainly about super-resolution(SR) for a single image. In this blog post, I will go further and talk about SR technique for video.

## Introduction
With the prevalence of video in our daily life, SR for low-resolution video is of high interest. Although single-image super-resolution (SISR) methods can be used to enhance the quality of video sequences, the highly correlated property of adjacent frames is neglected. On the other hand, video super-resolution methods process consecutive video frames at once, allowing the utilization of the information from neighboring frames to super-resolve the target frame.

## Video Super-Resolution
Video super-resolution is based on SISR while additionally gathering information across multiple highly related but misaligned video frames. A typical framework is to align neighboring frames with the target frames, aggregate the information and then upsample through techniques similar to SISR. In the following, we will discuss one state-of-the-art VSR model, BasicVSR [1].

### BasicVSR
BasicVSR considers essential components for VSR with the following functionalities: Propagation, Alignment, Aggregation, and Upsampling.
[pic]

#### Propagation
The propagation component determines how the model accumulates information from video frames. BasicVSR adopts a bidirectional propagation scheme, which allows features to be propagated in both directions in time. It is implemented by two independent RNNs, taking input frames forward and backward in time respectively. This architecture allows the model to leverage information from both directions in time. If there were only one direction, then the model will have much less information when processing the first few frames compares to later frames, undermining the output qualities.
[pic]

#### Alignment
Inside the RNN block, an alignment operation will be performed to align highly related but misaligned images. It is done using optical flow estimation, in particular, the SpyNet [4] is used for its cheap computation cost. Then, aligned images will be concatenated with the target image before performing convolution to extract useful features.
[pic]

#### Aggregation & Upsampling
For aggregation, the model simply concatenates the output features of both RNNs. Next, an upsampling operation will be performed using several convolution layers and pixel-shuffle layers [5].
[pic]

### Improvement
BasicVSR presents a generic framework for video super-resolution. Each component can be further improved upon for performance gain. For instance, BasicVSR++ [2] achieves SOTA results by incorporating deformable convolution [3] into frame alignment. The following image shows the result of BasicVSR++.
[pic]

---
In this blog post, I briefly introduce the technique for video super-resolution using BasicVSR as an example. In my next post, I will discuss more the limitations of current methods and some ongoing research work for solving those problems.

## Reference

[1] K. C. K. Chan, X. Wang, K. Yu, C. Dong, and C. C. Loy. Basicvsr: The
search for essential components in video super-resolution and beyond,
2021.

[2] K. C. K. Chan, S. Zhou, X. Xu, and C. C. Loy. Basicvsr++: Improving
video super-resolution with enhanced propagation and alignment, 2021.

[3] J. Dai, H. Qi, Y. Xiong, Y. Li, G. Zhang, H. Hu, and Y. Wei. Deformable
convolutional networks, 2017.

[4] A. Ranjan and M. J. Black. Optical flow estimation using a spatial
pyramid network, 2016

[5] W. Shi, J. Caballero, F. Husz´ar, J. Totz, A. P. Aitken, R. Bishop,
D. Rueckert, and Z. Wang. Real-time single image and video super-resolution using an efficient sub-pixel convolutional neural network,
2016.