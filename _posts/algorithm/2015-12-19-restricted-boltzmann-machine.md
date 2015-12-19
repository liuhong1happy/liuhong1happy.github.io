---
layout: post
category : algorithm
title: "机器学习算法汇总"
tagline: "人工神经网络、深度学习及其它"
tags : [algorithm,machine learning]
---
{% include JB/setup %}

`受限玻尔兹曼机(Restricted Boltzmann Machine,简称RBM)`是由`Hinton`和`Sejnowski`于`1986年`提出的一种`生成式随机神经网络(generative stochastic neural network)`，该网络由一些`可见单元`(visible unit，对应可见变量，亦即数据样本)和一些`隐藏单元`(hidden unit，对应隐藏变量)构成，`可见变量和隐藏变量都是二元变量`，亦即其状态取{0,1}。整个网络是一个`二部图`，只有`可见单元`和`隐藏单元`之间才会存在`边`，可见单元之间以及隐藏单元之间都不会有边连接，如下图所示：

![21110338-415413c3686645a890cb490a36f8ef70.png](/assets/images/algorithm/21110338-415413c3686645a890cb490a36f8ef70.png)


