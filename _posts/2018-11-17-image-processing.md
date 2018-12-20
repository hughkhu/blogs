---
layout: post
title:  "Image Processing Notes"
date:   2018-11-17 22:00:13
categories: Algorithm
permalink: /archivers/imgprocess
---
<!-- # 图像处理算子笔记 -->
# 1. Harris角点检测
构造大小为$2 \times 2$ 的 $M$ 矩阵：
$$
\begin{aligned}
& E(u,v) = \sum {w(x,y)(I(x+u,y+v) - I(x,y))^2} = \sum {w(x,y) [u, v] M [u,v]^T} \\\\

& M = 
\left[
\begin{matrix}
     I_x^2 & I_xI_y \\
     I_xI_y & I_y^2
\end{matrix}
\right] \\\\

& R = det M-k (trace M)^2
\end{aligned}
$$

- $M$ 特征值都比较大时，即窗口中含有角点

- 特征值一个较大，一个较小，窗口中含有边缘

- 特征值都比较小，窗口处在平坦区域


# 2. Sobel边缘检测
Sobel 算子有两个，一个是检测水平边缘的；另一个是检测垂直边缘的。用于提取边缘，
可以利用快速卷积函数。

$$
\begin{aligned}
& G_x = \left[
    \begin{matrix}
        -1 & 0 & 1 \\
        -2 & 0 & 2 \\
        -1 & 0 & 1
    \end{matrix}
    \right] * I  \\\\
& G_y = 
\left[
\begin{matrix}
     -1 & -2 & -1 \\
     0 & 0 & 0 \\
     1 & 2 & 1
\end{matrix}
\right] * I \\\\
& \theta = \sqrt{\frac{G_y}{G_x}}
\end{aligned}
$$
- 如果以上的角度$\theta$`等于零，即代表图像该处拥有纵向边缘，左方较右方暗。

# 3. Laplace Operator 锐化
图像锐化处理的作用是使灰度反差增强，从而使模糊图像变得更加清晰。图像模糊的实质就是图像受到**平均运算或积分运算**，因此可以对图像进行逆运算，如**微分**运算能够突出**图像细节**，使图像变得更为清晰。由于拉普拉斯是一种微分算子，它的应用可增强图像中灰度突变的区域，减弱灰度的缓慢变化区域。因此，锐化处理可选择拉普拉斯算子对原图像进行处理，产生描述灰度突变的图像，再将拉普拉斯图像与原始图像叠加而产生锐化图像。

$$
\begin{aligned}
&\frac{\partial^2 f }{\partial x^2} =f(x+1,y)+f(x-1,y) - 2f(x,y) 
\\\\
&\nabla^2 f(x,y) = 
\left[
\begin{matrix}
     0 & -1 & 0 \\
     -1 & 4 & -1 \\
     0 & -1 & 0
\end{matrix}
\right] * I(x,y) 
\\\\
& g(x,y) = f(x,y) + k \nabla^2 f(x,y) 
\end{aligned}
$$

- $g(x,y)$ 为锐化后的结果，锐化使得图像细节更加突出。

# 4. LoG - Laplace of Guassian
提出原因：因为Laplace算子虽然解决了一阶微分算子确定阈值的困难，但是不能克服噪声的干扰。

LoG步骤：
1. 对图像进行高斯滤波，在进行Laplace运算。
2. 保留了一阶导数峰值的位置，从中寻找Laplace过零点；
3. 对过零点的精确位置进行插值估计。

$$
\begin{aligned}
& G_{\sigma}(x,y) = \frac{1}{2\pi\sigma}\exp(-\frac{x^2+y^2}{2\sigma^2}) \\\\

& LoG(f)(x,y)=\nabla^2(G_{\sigma}*f) =\nabla^2G_{\sigma}*f  \\\\

& \nabla^2G_{\sigma} = \frac{\partial^2 G_{\sigma} }{\partial x^2} +
\frac{\partial^2 G_{\sigma} }{\partial y^2} =
\frac{-2\sigma^2+x^2+y^2}{2\pi\sigma^6}
\exp(-\frac{x^2+y^2}{ 2\sigma^2})
\end{aligned}
$$

- $\sigma$ 是尺度参数，在图像处理中引入尺度以及建立多尺度空间是一个重要的突破；
- $\sigma$ 越大，图像越模糊，消除噪声的效果越好。

- 常用模板

$$
\left[
\begin{matrix}
     0 & 0 & 1 & 0&0 \\
     0&1 & 2 &1 &0 \\
     1&2 & -16 &2 &1 \\
     0&1 & 2 &1 &0 \\
     0 & 0 & 1 & 0&0 
\end{matrix}
\right]

$$

# 5. DoG - Difference of Guassian

DoG是对LoG的近似。 [DoG Reference](https://blog.csdn.net/u014485485/article/details/78364573)

$$
\begin{aligned}
& \frac{\partial G}{\partial \sigma} = \sigma \nabla^2 G \\\\

& G(x,y,k\sigma) - 
G(x,y,\sigma)  \approx
(k-1)\sigma^2\nabla^2 G \\\\

& DoG(f)(x,y,\sigma_1,\sigma_2) = G(x,y,\sigma_1) - G((x,y,\sigma_2)
\end{aligned}
$$

# 6. HOG - Histogram of Oriented Gradient
方向梯度直方图特征，可结合SVM进行运用。

1. 一般取8x8（其他值也行）的窗口作为cell，cell中每个像素计算梯度方向和梯度模长，构造直方图（一般9个bin），得到9维特征向量。

2. 一般取2x2个cell组成block，那么block为16x16大小，故每个block有2x2x9=36个特征。

3. 滑动每个block，假设stride为8，那么对64x128的图像而言，一共滑动7x15次，故整张图的特征数为36x7x15=3780。