---
layout: post
title:  "Tensorflow Pytorch Installation"
date:   2018-12-21 22:00:13
categories: Learn
permalink: /archivers/installpkgs
---

This article consists of several notes about `tensorflow` and `pytorch` installation.

<!--more-->

# 1. Table about Envs and Pkgs

|Env|Package|Version|Channel| 
|---|---|---|---|
base|
-|python| 3.7
tf|
-|python| 3.5 | 
-|tensorflow-gpu| 1.12 | pip 
face|
-|python| 3.6 |
-|tensorflow-gpu| 1.12 | conda
-|dlib| 19.16 | pip  
pyt|
-|python| 3.5 | 
-|pytorch| 1.0 | conda pytorch
-|face_alignment| 1.0.1 | 
-|tensorflow-gpu| 1.10.0 | conda

# 1. Prerequisite 
- Update GPU Driver (417.35 For `GTX 960`). Not necessary.
- Install `CUDA 9.0` (8.0 is outdated and may cause inconvienient when installing TF on Win 10).
- Install `CUDNN 7`.
- (recommended) Install `Anaconda` and set channels (`C:/users/username/.condarc`)
    ~~~bash
    conda config --add channels channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/  
    conda config --add channels channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
    conda config --set show_channel_urls yes  
    ~~~
# 2. Install Tensorflow 
Install tensorflow in Anaconda envs, install scikit-image, Dlib alongside.

It is recommended to use conda first, **avoid pip** as possible (2 pkgs may be installed when use pip first and conda later$^{*}$).  
~~~bash
conda create -n face python==3.6 # create new env
conda install tensorflow-gpu # numpy scipy mkl six cudnn cudatoolkit
conda install scikit-image # matplotlib Pillow tk qt
# conda install dlib # up/downgrade numpy, scipy, scikit-image matplotlib ect.
pip install dlib # only dlib
python demo.py -i e:\0tmp -o e:\0tmp --isDlib True # test tf & dlib
~~~

$^{*}$ pip 安装时，会检查 dist-info 或 egg-info; conda安装时，则检查 conda-meta.
如果先pip后conda是可以同时装的; 反之，pip会认为已经装了，但是如果强行--ignore-installed还是可以再装一个。同时存在两个同名的pkg容易产生冲突。

# 3. Install Pytorch 
I Failed in Python 3.6, but succeeded when installing in Python 3.5.$^{**}$
~~~bash
conda create -n pyt python==3.5 # create new env
conda install pytorch torchvision -c pytorch  # slow, sucesss in py 3.5
# conda install pytorch # tsinghua cloud/pytorch
# conda install torchvision # when import torch, dll not load, unknown bug.

# install 3d landmark detector, opencv is installed alongside.
conda install -c 1adrianb face_alignment 
~~~

$^{**}$ 首先是在py 3.6 通过清华源安装pytorch（因为比官网命令快），但是import torch 报dll not load 的错误，网上有说是openmp的dll的问题，多次尝试都无法成功。conda新建py3.6环境，再用官网命令依旧不行。最终通过删除相关package，在新建一个py3.5环境，使用官网命令成功。怀疑py3.6.0有问题，有人提到可以直接升级py3.6.0到3.6.1解决。

