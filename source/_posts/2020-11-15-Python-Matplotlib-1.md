---
title: Python-Matplotlib-简介
abbrlink: 28977
date: 2020-11-15 11:38:16
tags:
	- Python
	- Matplotlib
categories: Python
---



## 概述

**Matplotlib:Python可视化**

&emsp;Matplotlib是一个综合库，用于在Python中创建静态，动画和交互式可视化。

<!--more-->

<br>

---

<br>

## 安装

> 安装官方发行版

&emsp;Matplotlib及其依赖项可用于macOS, Windows和Linux发行版的轮包:

```shell
python -m pip install -U pip
python -m pip install -U matplotlib
```

&emsp;如果此命令导致从源代码编译Matplotlib，并且编译出现问题，则可以添加`--prefer-binary`以选择最新版本的Matplotlib，对于该版本，您的OS和Python已预编译了。

---

> 安装第三方发行版

**科学的Python发行版**

&emsp;[Anaconda](https://www.anaconda.com/)和[ActiveState](https://www.activestate.com/activepython/downloads)是Windows，macOS和常见Linux平台的出色选择。[WinPython](https://winpython.github.io/)是Windows用户的选项。所有这些发行版都包括Matplotlib和*许多*其他有用的（数据）科学工具。

**Linux:使用包管理器**

&emsp;如果您使用的是Linux，您可能更喜欢使用包管理器。Matplotlib几乎适用于所有主要的Linux发行版。

- Debian / Ubuntu: `sudo apt-get install python3-matplotlib`
- Fedora: `sudo dnf install python3-matplotlib`
- Red Hat: `sudo yum install python3-matplotlib`
- Arch: `sudo pacman -S python-matplotlib`

<br>

---

<br>

## 简介

### 使用指南

#### 导入

```python
import matplotlib.pyplot as plt
import numpy as np     #matplotlib常与numpy库搭配使用
```

> 在这里举个简单的例子：

&emsp;用坐标轴创建图形最简单的方法是使用[`pyplot.subplots`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplots.html#matplotlib.pyplot.subplots)。我们可以用 [`Axes.plot`](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.plot.html#matplotlib.axes.Axes.plot)绘制坐标轴上的一些数据:

```python
fig,ax = plt.subplots()       #创建一个包含单个坐标轴的图形。
ax.plot([1,2,3,4],[1,4,2,3])  #在坐标轴上绘制一些数据
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/15/7384d398ec67aafa2de878a4c7ff9413.png" style="zoom:80%;margin-left:10px" />

#### Figure的组成

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/15/7297f12faa0667f3706318353082da47.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

如果在文章中发现问题或是对matplotlib有些许疑问欢迎在评论区中留言