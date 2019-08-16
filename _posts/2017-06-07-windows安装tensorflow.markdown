---
title: Windows 上安装tensorflow 
date: 2017-06-25 23:00:00
categories: other
--- 


Windows 上目前只支持Python 3.5 。 所以要么anaconda 下载的就是3.5 的，要么就创建一个 Python = 3.5 的environment。 

1. 下载安装anaconda3，然后把anaconda3 加入到path 中 (确保conda 能用，可以通过anaconda navigator 进入)

        python  

2. 下载安装cuda 和 cudnn。 cudnn 需要复制粘贴到cuda 的dir下面 
在cmd 里输入 nvcc -V 验证cuda 是否安装完成 （目前cuda 8.0 cudnn 5.1）

        nvcc -V

3. 创建一个 Python 3.5 的环境 然后激活 
        
        conda create -n tensorflow python=3.5 
        activate tensorflow

4.  安装如下TensorFlow -gpu 
        
        pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/windows/gpu/tensorflow_gpu-1.2.0-cp35-cp35m-win_amd64.whl

5. tensorflow 应该已经安装好了 验证TensorFlow

        python 
        >> import tensorflow as tf 
        >> hello = tf.constant('Hello, TensorFlow!')
        >> sess = tf.Session()
        >> print(sess.run(hello))
