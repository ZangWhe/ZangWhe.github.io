---
title: 2020-11-15-Python-Matplotlib
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

### 导入

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

### Figure的组成

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/15/7297f12faa0667f3706318353082da47.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

## Pyplot教程

### pyplot简介

[`matplotlib.pyplot`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html#module-matplotlib.pyplot)是使matplotlib像MATLAB一样工作的函数的集合。每个`pyplot`功能都会对图形进行一些更改：例如，创建图形，在图形中创建绘图区域，在绘图区域中绘制一些线条，用标签装饰绘图等。

> 使用pyplot生成可视化的效果非常快：

```python
plt.plot([1,2,3,4])
plt.ylabel('num')
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/15/7de3260fe8f8ea7e78c0e32906e6d4d5.png" style="zoom:80%;margin-left:10px" />

关于上面这个示例中，x轴范围0-3,y轴范围1-4,原因是如果你向Plot传递单个列表或数组，那么matplotlib假定它是y轴的序列，并自动为你生成从0开始的x值

---

### 格式化plot的样式

> 对于每对x，y参数，都有一个可选的第三个参数，它是表示图的颜色和线型的格式字符串。格式字符串的字母和符号来自MATLAB，您将颜色字符串与线型字符串连接在一起。默认格式字符串是“ b-”，这是一条蓝色实线。

例如，要用红色圆圈绘制以上内容：

```python
plt.plot([1,2,3,4],[1,4,9,16],'ro') #'r':red,'o':点
plt.axis([0,6,0,20])                #确定坐标轴的范围，x轴0-6，y轴0-20
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/15/db2a3f7ecb19275e460762ead8cffa7d.png" style="zoom:80%;margin-left:10px" />

> 格式字符串由颜色，标记物和线条组成
>
> ```
> fmt = '[marker][line][color]'  #其他组合也是允许的，例如[color][marker][line]
> ```

> **每一个参数都是可选的。**

> Markers(标记物)

| 字符  | 描述               |
| ----- | ------------------ |
| `'.'` | 点标记             |
| `','` | 像素标记           |
| `'o'` | 圆圈标记           |
| `'v'` | triangle_down标记  |
| `'^'` | 三角形标记         |
| `'<'` | triangle_left标记  |
| `'>'` | triangle_right标记 |
| `'1'` | tri_down标记       |
| `'2'` | tri_up标记         |
| `'3'` | tri_left标记       |
| `'4'` | tri_right标记      |
| `'s'` | 方形标记           |
| `'p'` | 五边形标记         |
| `'*'` | 星标               |
| `'h'` | 六角形标记         |
| `'H'` | 六角标记           |
| `'+'` | 加号               |
| `'x'` | X标记              |
| `'D'` | 钻石笔             |
| `'d'` | thin_diamond标记   |
| `'|'` | vline标记          |
| `'_'` | 标记线             |

> line(线形)

| 字符   | 描述       |
| ------ | ---------- |
| `'-'`  | 实线样式   |
| `'--'` | 虚线样式   |
| `'-.'` | 点划线样式 |
| `':'`  | 虚线样式   |

> color(颜色)

| 字符  | 颜色 |
| ----- | ---- |
| `'b'` | 蓝色 |
| `'g'` | 绿色 |
| `'r'` | 红   |
| `'c'` | 青色 |
| `'m'` | 品红 |
| `'y'` | 黄色 |
| `'k'` | 黑色 |
| `'w'` | 白色 |

如何参数中只有颜色这一选择项，则可以使用任何[`matplotlib.colors`](https://matplotlib.org/api/colors_api.html#module-matplotlib.colors)规格，例如全名（‘green')或十六进制表示('#008000')