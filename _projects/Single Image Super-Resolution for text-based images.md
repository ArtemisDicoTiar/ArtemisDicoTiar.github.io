---
title: "Single Image Super-Resolution for text-based images"
image: 
  path: /assets/images/SISR.jpg
  caption: "Photo from project thesis presentation."
categories: 
  - Bachelor Degree Project
tags:
  - Done
last_modified_at: 2021-04-30 12:00:00 +0100
---

[**Thesis paper**](/assets/SISR_Thesis.pdf)
[**Thesis presentation PDF**](/assets/SISR_Presentation.pdf)

## Abstract

​	Reading texts on low-resolution images is difficult. The low-resolution text-based images are usually produced due to the bad performance of the old camera or the target object captured on the image is far from the camera. A various number of methods to improve low-resolution image to high-resolution have been proposed. This problem is also known as Single-Image Super-Resolution (SISR). The SISR methods have been developed from mathematical and statistical methods to machine learning and deep-learning-based methods. The tool to general users trying to use SISR methods, especially targets to up-sample text-based images, is the project's main objective. Therefore, 12 SISR methods are assessed, and the Graphical User Interface is built in this project. The SISR methods up-sample four image sets with scaling factor of 2, 3, 4 and 8. The up-sampled images are compared with ground-truth images by using four image quality assessment methods. The benchmark emphasis that 'ICBI' is the dominating method to up-sample the low- resolution image in the experimenting condition with scaling factor of 2, 4 and 8. For the experiment setting with a scaling factor of 3, as 'ICBI' was not available to process, 'EDSR' and 'ESPCN' showed the best performing. The GUI is then developed by taking the code used for benchmark as backend, and the codes are wired into front-end code and user interface. Although the benchmark result showed that 'ICBI' is the best performing SISR method, the up-sampled image had some artefacts and wiggly lines compare to other methods. The reason for this issue and the limitation of image quality assessment methods are dealt on the discussion. Finally, this project is concluded by addressing future research related to the limitation and problems.

## Table of Contents

1. INTRODUCTION 
2. Single-Image Super-Resolution Methods
   1. Interpolation methods
   2. Deep-learning methods
   3. Edge-preserving methods
3. Image Quality Assessment
   1. Subjective Image Quality Assessments
   2. Objective Image Quality Assessments
4. Benchmark Setting and Implementation
   1. Image Datasets
   2. Color channel
   3. Benchmark availability by scaling factor
   4. Benchmark implementation (codes)
5. ExperimentResults
6. Discussions
7. Conclusions/Future Works
8. Appendix
