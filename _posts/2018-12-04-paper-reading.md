---
layout: post
title:  "Paper Reading Lists"
date:   2018-12-04 22:00:00
categories: Research
permalink: /archivers/papers
---

This article lists important research papers about 3D Face Reconstruction.

<!--more-->

<!-- # Paper Reading -->
# 1. 3D Face From Image
- 3D Face Reconstruction from a Single Image Using a Single Reference Face Shape 
  (PAMI 2011, Ira Kemelmacher-Shlizerman)

  `给定Reference Face模型之后，以深度为优化对象，进行SFS(正则项基于深度差和Albedo差的LoG)；具体而言，先算光照L，再深度，最后Albedo.`

- Unconstrained 3D Face Reconstruction (CVPR 2015, Joseph Roth, Xiaoming Liu)
  [[Code](http://cvlab.cse.msu.edu/project-face-recon.html)]
  
  Adaptive 3D Face Reconstruction from Unconstrained Photo Collections(CVPR 2016)

  `Laplacian Driven，多图Potometric。`

- A Multiresolution 3D Morphable Face Model and Fitting Framework (VISAPP 2016, Patrik Huber1)[[Code](https://github.com/patrikhuber/eos)]

  `Github EOS, 可以对照Code一读，待读。。。`

- Large Pose 3D Face Reconstruction from a Single Image via Direct Volumetric
CNN Regression (ICCV 2017, Aaron Jackson)[[Code](https://github.com/AaronJackson/vrn)]

  `体素CNN，待细读。。。`

- Learning Detailed Face Reconstruction from a Single Image (CVPR 2017, Elad Richardson, Roy Or-El)
  
  `后半部分网络化SFS`

- **SfSNet: Learning Shape, Reflectance and Illuminance of Faces in the Wild** (CVPR 2018, Soumyadip Sengupta)[[Code](https://senguptaumd.github.io/SfSNet/)]
  
  `To Be Reading...`

- Joint 3D Face Reconstruction and Dense Alignment with Position Map Regression Network (ECCV 2018, Yao Feng)[[Code](https://github.com/YadiraF/PRNet)]
  
  `UV-Position, Code...`
- **UV-GAN: Adversarial Facial UV Map Completion for Pose-invariant Face
Recognition** (CVPR 2018, Jiankang Deng)

  `UV map...`

- 3D Face Reconstruction with Geometry Details from a Single Image (TIP 2018, Luo Jiang)

  `Coarse-to-fine 3 steps，待细看landmark更新，第二步使用了流形Laplacian Eigenvalue降维。`

- **State of the Art on Monocular 3D Face Reconstruction, Tracking, and Applications** (EG 2018, M. Zollhöfer) [[Talks]](http://web.stanford.edu/~zollhoef/papers/EG18_FaceSTAR/page.html)

  `综述Paper，Focus在优化方法，约束分为Dense(像素Color和3D点), Sparse(特征点), 正则项。`

# 2. Face Alignment
- Joint Face Alignment and 3D Face Reconstruction (ECCV 2016, Feng Liu, Xiaoming Liu)
  
    `基础背景：SDM牛顿步； 训练从特征算子到偏移量的回归器，多层回归，逐步从平均脸特征点移动至最终结果。`

- Face Alignment Across Large Poses: A 3D Solution (CVPR 2016, Xiangyu Zhu, Xiaoming Liu)
  
  `3DDFA, Dataset, Code...`

- Adaptive Cascade Regression Model for Robust Face Alignment (TIP 2017, Qingshan Liu)
  
  `Landmark Regression...`
- How far are we from solving the 2D & 3D Face Alignment problem? (ICCV 2017, Adrian Bulat)
  
  `Learning and Release a Dataset...`
- Synthesizing Normalized Faces from Facial Identity Features (CVPR 2017, Forrester Cole)

  `生成正面照。。。`

- Pose-Guided Photorealistic Face Rotation (CVPR 2018, Yibo Hu)
  
  `旋转正面照。。。`

# 3. 3D Face Video App
- Dynamic 3D Avatar Creation from Hand-held Video Input (SIGGRAPH 2015, Alexandru Eugen Ichim)
  
  `UV albedo... 高光补偿项；Blendshape, Frame Optical Flow`

- Face2Face: Real-time Face Capture and Reenactment of RGB Videos （CVPR 2016, Justus Thies, M. Zollhöfer）
  
    `Face2Face Video...`
- Reconstruction of Personalized 3D Face Rigs from Monocular Video (TOG 2016, P. GARRIDO and M. Zollhöfer)

  `Coarse-to-fine, 3D Rig Control...`

# 4. Face Intrinsic Lighting
- An Efficient Representation for Irradiance Environment Maps (SIGGRAPH 2001, Ravi Ramamoorthi)

  `证明 SH Lighting 低通，对朗伯体2阶即可表征Shading.`
- Intrinsic Face Image Decomposition with Human Face Priors (ECCV 2014, Chen Li)

  `分区域高斯混叠GMM约束Albedo，使用MERL数据集肤色等，后半部分较复杂。`

- Fast and High Quality Highlight Removal From a Single Image (TIP 2016, Jinli Suo, Qionghai Dai)
  
  `多物体场景高光分解，投影到两个轴`

- Specular Highlight Removal in Facial Images (CVPR 2017, Chen Li)
  
  `肤色由ICA得到两个基底，SH Lighting两次运用，一次是Diffuse Shaidng，另一次是反射的高光近似。`
- Occlusion-aware 3D Morphable Models and an Illumination Prior for Face Image Analysis (IJCV 2018, Bernhard Egger)
  
  `Light Priors.`
- Label Denoising Adversarial Network (LDAN) for Inverse Lighting of Face Images (CVPR 2018, Hao Sun)

  `GAN回归人脸SH Lighting，待读。。。`



# 5. General RGB-D Fusion SFS
- Real-time Shading-based Refinement for Consumer Depth Cameras (TOG 2014, Chenglei Wu)
  
  `RGB-D input, refine Depth through SFS, using SH Lighting and Frame Temporal Constraints.`

- Shading-based Refinement on Volumetric Signed Distance Functions (TOG 2015, M. Zollhöfer)
  
  `VSDF, GPU-based Gauss-Newton solver...`

- RGBD-Fusion Real-Time High Precision Depth Recovery (CVPR 2015, Roy Or-El)
    
  `RGB-D, SFS...`

# 6. 3D Body Model
- SCAPE: Shape Completion and Animation of People (TOG 2005, Dragomir Anguelov)

  `训练得到由刚体变换R到非刚体变换的Q的回归矩阵a，以及PCA分解shape因素`
- SMPL: A Skinned Multi-Person Linear Model (TOG 2015, Matthew Loper)

  `Shape参数(beta),Pose参数(theta)共同影响Shape和Pose，初始shape T由线性beta、theta结合主元得到；有关节Joints位置由beta回归得到；结合W系数，T和Joints位置及theta对应的旋转矩阵，最终生成模型点的位置。`