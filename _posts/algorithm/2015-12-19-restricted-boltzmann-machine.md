---
layout: post
category : algorithm
title: "受限玻尔兹曼机"
tagline: "Restricted Boltzmann Machine,简称RBM"
tags : [algorithm,deep learning,RBM]
---
{% include JB/setup %}

`受限玻尔兹曼机(Restricted Boltzmann Machine,简称RBM)`是由`Hinton`和`Sejnowski`于`1986年`提出的一种`生成式随机神经网络(generative stochastic neural network)`，该网络由一些`可见单元`(visible unit，对应可见变量，亦即数据样本)和一些`隐藏单元`(hidden unit，对应隐藏变量)构成，`可见变量和隐藏变量都是二元变量`，亦即其状态取{0,1}。整个网络是一个`二部图`，只有`可见单元`和`隐藏单元`之间才会存在`边`，可见单元之间以及隐藏单元之间都不会有边连接，如下图所示：

![21110338-415413c3686645a890cb490a36f8ef70.png](/assets/images/algorithm/21110338-415413c3686645a890cb490a36f8ef70.png)

上图所示的RBM含有12个可见单元(构成一个向量v)和3个隐藏单元(构成一个向量h)，W是一个12*3的矩阵，表示可见单元和隐藏单元之间的边的权重。

## 1. RBM的学习目标-最大化似然(Maximizing likelihood)

RBM是一种基于能量(Energy-based)的模型，其可见变量v和隐藏变量h的联合配置(joint configuration)的能量为：

![21110949-bbc3c4b03f294c4bbd0ed3bbda20e7f6.png](/assets/images/algorithm/21110949-bbc3c4b03f294c4bbd0ed3bbda20e7f6.png)（式子-1）

其中θ是RBM的参数{W, a, b}, W为可见单元和隐藏单元之间的边的权重，b和a分别为可见单元和隐藏单元的偏置(bias)。

有了v和h的联合配置的能量之后，我们就可以得到v和h的联合概率：

![21111309-66ff27074d7e4395b9318ec90da8e2a2.png](/assets/images/algorithm/21111309-66ff27074d7e4395b9318ec90da8e2a2.png)（式子-2）

其中Z(θ)是归一化因子，也称为配分函数(partition function)。根据式子-1，可以将上式写为：

![21111713-7be5f608b8504de89dc72448773e573c.png](/assets/images/algorithm/21111713-7be5f608b8504de89dc72448773e573c.png)（式子-3）

我们希望最大化观测数据的似然函数P(v)，P(v)可由式子-3求P(v,h)对h的边缘分布得到:

![21112100-5814bd3e0606470f81b5b026115d61f3.png](/assets/images/algorithm/21112100-5814bd3e0606470f81b5b026115d61f3.png) (式子-4)

我们通过最大化P(v)来得到RBM的参数，最大化P(v)等同于最大化log(P(v))=L(θ)：

![21112339-69a71593ad54496b9e767433ff7646bf.png](/assets/images/algorithm/21112339-69a71593ad54496b9e767433ff7646bf.png)(式子-5)

## 2. RBM的学习方法-CD(Contrastive Divergence，对比散列)

可以通过随机梯度下降(stichastic gradient descent)来最大化L(θ)，首先需要求得L(θ)对W的导数：

![21112601-bdada787edee432b92f6ca7bfcf943d8.png](/assets/images/algorithm/21112601-bdada787edee432b92f6ca7bfcf943d8.png)(式子-6)


经过简化可以得到：

![21112938-e96b9b93b793418f9f5c17562db559fa.png](/assets/images/algorithm/21112938-e96b9b93b793418f9f5c17562db559fa.png)(式子-7)

后者等于

![21113221-7dd42f87085a4840b2255b71f7a4e070.png](/assets/images/algorithm/21113221-7dd42f87085a4840b2255b71f7a4e070.png)(式子-8)

式子-7中的前者比较好计算，只需要求vihj在全部数据集上的平均值即可，而后者涉及到v，h的全部2|v|+|h|种组合，计算量非常大(基本不可解)。

为了解决式子-8的计算问题，Hinton等人提出了一种高效的学习算法-CD(Contrastive Divergence)，其基本思想如下图所示：

![21113954-0812b82d905c4a609c085b9aecc68e2c.png](/assets/images/algorithm/21113954-0812b82d905c4a609c085b9aecc68e2c.png)


首先根据数据v来得到h的状态，然后通过h来重构(Reconstruct)可见向量v1，然后再根据v1来生成新的隐藏向量h1。因为RBM的特殊结构(层内无连接，层间有连接)， 所以在给定v时，各个隐藏单元hj的激活状态之间是相互独立的，反之，在给定h时，各个可见单元的激活状态vi也是相互独立的，亦即：


![21114405-febede8cfd01499ba72513e249dec2db.png](/assets/images/algorithm/21114405-febede8cfd01499ba72513e249dec2db.png)(式子-9)

重构的可见向量v1和隐藏向量h1就是对P(v,h)的一次抽样，多次抽样得到的样本集合可以看做是对P(v,h)的一种近似，使得式子-7的计算变得可行。

## RBM的权重的学习算法：

1. 取一个样本数据，把可见变量的状态设置为这个样本数据。随机初始化W。
2. 根据式子-9的第一个公式来更新隐藏变量的状态，亦即hj以P(hj=1|v)的概率设置为状态1，否则为0。然后对于每个边vihj，计算Pdata(vihj)=vi*hj(注意，vi和hj的状态都是取{0,1})。
3. 根据h的状态和式子-9的第二个公式来重构v1，并且根据v1和式子-9的第一个公式来求得h1，计算Pmodel(v1ih1j)=v1i*h1j。
4. 更新边vihj的权重Wij为Wij=Wij+L*(Pdata(vihj)=Pmodel(v1ih1j))。
5. 取下一个数据样本，重复1-4的步骤。
6. 以上过程迭代K次。
