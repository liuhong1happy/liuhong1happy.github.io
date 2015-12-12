---
layout: post
category : golang
title: "Ubuntu下安装golang"
tagline: "学习gloang语言的先决条件"
tags : [golang]
---
{% include JB/setup %}

## 环境要求

- ubuntu14.04

- python 2.7

- gcc等编译工具

## golang ppa方式安装

    sudo apt-get install python-dev python-pip
    
    sudo apt-get install -y python-software-properties software-properties-common
    
    sudo add-apt-repository -y ppa:gophers/go
    
    sudo apt-get update
    
    sudo apt-get install -y golang-stable

## gccgo 方式安装

    sudo apt-get install -y gccgo

## golang工作路径环境变量添加

    sudo mkdir $HOME/golang 
    
    sudo export GOPATH=$HOME/golang
    
    sudo export PATH=$PATH:$GOPATH/bin

## 长久保存golang环境变脸

编辑`/etc/environment`

    PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/home/liuhong/golang/bin"
    
    GOPATH="/home/liuhong/golang/bin"　　　　
