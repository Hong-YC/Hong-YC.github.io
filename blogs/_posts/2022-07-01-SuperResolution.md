---
title: 'Super Resolution Series I'
date: 2022-02-04
permalink: /blogs/superRes
author_profile: false
tags:
  - hkust
---
By Hong

This summer, I have a chance to work on a research project under the supervision of [Professor Gary](https://www.cse.ust.hk/~gchan/) in HKUST. My task is to improve the image quality of surveillance cameras in different settings (streets, parking lot, etc). Thus, I start to self-study super-resolution techniques. I would like to share what I have learned along the way in this series of blog posts. 

## Introduction

Super-resolution aims at reconstructing sharp and high-resolution (HR) images from corresponding blurry and low-resolution counterparts. The ability to enhance perceptual quality of images has many practical usages, such as security, surveillance, and medical images. In addition, SR also helps to improve other computer vision tasks, such as object detection, face recognition, and image classification. The rest of this article I will first describe the general problem setting of SR. Next, several state-of-the-art SR methods and their limitation will be introduced. 

[//]: # pic

## Problem Setting

Single image super-resolution(SISR) aims at recovering the corresponding high-resolution image from a low-resolution image. Generally, the low-resolution image I<sub>low</sub> is modeled as the output of the degradation process:

[//]: # pic

where D is the degradation function and δ denotes the parameters of D. In practice, the degradation process is often modeled as:

[//]: # pic

where I<sub>high</sub> ⊗ κ represents the convolution between a blur kernel κ and highresolution image I<sub>high</sub>, and n is some Gaussian noise. 

We want to recover a high-resolution approximation I<sub>sr</sub> of the ground truth I<sub>high</sub> from the I<sub>low</sub>:

[//]: # pic

where SR is the super-resolution model and θ denotes the parameters of SR.