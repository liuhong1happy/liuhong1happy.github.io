---
layout: post
category : react-native
title: "react-native-image-crop-picker组件使用"
tagline: "快速开始RN"
tags : [react,react-native,macosx,android]
theme :
  name : twitter
---
{% include JB/setup %}

## 概述

最近弄这个图片上传和裁剪，正是心碎了一盘。最先，采用react-native-image-picker，在android上老是提示包重复，所以选择react-native-image-crop-picker。

但是，react-native-image-crop-picker需要使用Cocoapods安装QBImagePickerController (3.4.0)和RSKImageCropper (1.5.1)。

所以，折腾了两天，搞Cocoapods的安装，所以本文重点讲述怎样安装Cocoapods。

## Cocoapods的安装步骤

1. 安装最新版本ruby(使用rvm，自己搜安装方法)。
2. 更新gem和gem源到淘宝源。
3. 安装Cocoapods

	sudo gem install cocoapods
	
4. 添加Cocoapods Specs的本地git仓库

		pod repo remove master
		mkdir ~/cocoapods/repo/master
		cd ~/cocoapods/repo/master
		git init
		git remote add origin git@git.oschina.net:akuandev/Specs.git
		git branch --set-upstream-to=origin/master master
		git pull
		pod repo add master git@git.oschina.net:akuandev/Specs.git
		pod repo update
		

5. 编写Podfile并执行 `pod install`
