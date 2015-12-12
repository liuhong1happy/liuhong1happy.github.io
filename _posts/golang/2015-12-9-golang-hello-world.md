---
layout: post
category : golang
title: "golang's Hello World"
tagline: "最简单的例子"
tags : [golang]
---
{% include JB/setup %}


## 参照上一篇文章安装golang

## 创建包路径

	sudo mkdir -p $GOPATH/src/github.com/user

## 创建包目录

	sudo mkdir $GOPATH/src/github.com/user/hello

## 包目录下创建文件hello.go

```c

package main

import "fmt" 

func main() { 

    fmt.Printf("Hello, world.\n") 

}

```

## 安装包

	go install github.com/user/hello

## 运行包

	hello
	Hello, world.
