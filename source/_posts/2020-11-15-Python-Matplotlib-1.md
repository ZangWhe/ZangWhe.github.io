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

### Pyplot教程

#### pyplot简介

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

#### plot的样式

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

---

#### 处理多个图形和轴

在下面这个例子中一个figure下创建了两个子图：

```python
import matplotlib.pyplot as plt
import numpy as np


def f(t):
    return np.exp(-t) * np.cos(2*np.pi*t)

t1 = np.arange(0.0, 5.0, 0.1)
t2 = np.arange(0.0, 5.0, 0.02)

plt.figure()
plt.subplot(211)  #211:   2行1列的第一个子图
plt.plot(t1, f(t1), 'bo', t2, f(t2), 'k')   #在其一子图上绘制了两个图形

plt.subplot(212)   #212:   2行1列的第二个子图
plt.plot(t2, np.cos(2*np.pi*t2), 'r--')   
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/17/32e0260e251fb0ddf0e72d5ba651fd2b.png" style="zoom:80%;margin-left:10px" />

同样：可以创建多个figure

```python
plt.figure(1)                # 第一个图形
plt.subplot(211)             # 第一个图形中的第一个子图
plt.plot([1, 2, 3])
plt.subplot(212)             # 第一个图形中的第二个子图
plt.plot([4, 5, 6])


plt.figure(2)                # 第二个图形
plt.plot([4, 5, 6])          # 默认创建一个 subplot(111)

plt.figure(1)             # 此时figure(1)仍然存在，并且此时subplot(212)是figure(1)当前使用
plt.subplot(211)          # 使得subplot(211)是figure（1）当前使用
plt.title('Easy as 1, 2, 3') # 声明subplot(211)的标题

plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/17/74788e34b8c8f82e96ad774108a9e433.png" style="zoom:80%;margin-left:10px" />

---

#### 为图形添加文字说明

[`annotate`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.annotate.html#matplotlib.pyplot.annotate)方法提供了注释方式

**参数**：xy表示注释的位置，xytext是文本的位置。这两个参数都是(x,y)元组

```python
ax = plt.subplot(111)

t = np.arange(0.0, 5.0, 0.01)
s = np.cos(2*np.pi*t)
line, = plt.plot(t, s, lw=2)

plt.annotate('local max', xy=(2, 1), xytext=(3, 1.5),
             arrowprops=dict(facecolor='black', shrink=0.05),
             )

plt.ylim(-2, 2)		#规定y值范围(-2,2)
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/19ab7b6707f8b7acd6dce6401fc2750c.png" style="zoom:80%;margin-left:10px" />

更多详细注释请参见官方文档[基本注释](https://matplotlib.org/tutorials/text/annotations.html#annotations-tutorial)和[高级注释](https://matplotlib.org/tutorials/text/annotations.html#plotting-guide-annotation)。

<br>

---

<br>

### 图片教程

#### 导入

```python
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
```

---

#### 将图像数据导入到NumPy数组

这是我们要处理的图片：

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/eca78bc2a4cd3044e704e56767078adf.png" style="zoom:80%;margin-left:10px" />

让我们打开并输出它：

```python
img = mpimg.imread('C:\\Users\\wangz\\Desktop\\Pic.png') #图片路径
print(img)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/b92eba8f96442abb65015ae5862c0264.png" style="zoom:80%;margin-left:10px" />

---

#### 将NumPy数组绘制成图像

> [`imshow()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.imshow.html#matplotlib.pyplot.imshow)函数将numpy数组中的数据渲染成图像。

```python
imgplot = plt.imshow(img)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/d876abea0674df9600ae45f3e725bf76.png" style="zoom:80%;margin-left:10px" />

> 伪彩色应用于图像

伪彩色是增强对比度和更轻松地可视化数据的有用工具。

伪彩色仅与单通道，灰度，发光度图像有关。我们目前有一个RGB图像。由于R，G和B都是相似的（请参见上方或数据中的内容），我们可以选择一个数据通道：

```python
lum_img = img[:,:,0]   #数组切片，更多相关切片请看个人博客关于NumPy学习
plt.imshow(lum_img)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/f81bafc9654111311ebc0f39d0108936.png" style="zoom:80%;margin-left:10px" />

> 同样，对于亮度图像，将应用默认的颜色图（又名查找表：LUT）。默认名称为viridis,也有其他可供选择:

```python
plt.imshow(lum_img,cmap="hot")    #暖色调显示
```

![image-20201120212946492](C:\Users\wangz\AppData\Roaming\Typora\typora-user-images\image-20201120212946492.png)

> 您还可以使用[`set_cmap()`](https://matplotlib.org/api/cm_api.html#matplotlib.cm.ScalarMappable.set_cmap)方法更改现有打印对象上的颜色图

```python
imgplot = plt.imshow(lum_img)
imgplot.set_cmap('nipy_spectral')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/d14d93979e5c002dede7d045f745d30b.png" style="zoom:80%;margin-left:10px" />

> 可以通过添加颜色条来了解颜色代表什么价值，可通过matplotlib.pyplot.colorbar()函数实现

```python
imgplot = plt.imshow(lum_img)
plt.colorbar()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/dfdb2bb41d08ec8de061672881d7630f.png" style="zoom:80%;margin-left:10px" />

> 如果你想增强图像的对比度，或扩大特定区域的对比度，同时牺牲颜色变化不大或无关紧要的细节。直方图是个好工具。要创建图像数据的直方图，我们使用[`hist()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.hist.html#matplotlib.pyplot.hist)函数。

```python
plt.hist(lum_img.ravel(),bins=256,range=(0.0,1.0),fc='k',ec='k')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/add5f57e923c19a1ee1d71fafbfa2daa.png" style="zoom:80%;margin-left:10px" />

在获取图像的主要的区域[0.0，0.7]后 (如直方图所示)，

我们可以通过传递**clim参数**或者调用**set_clim()**方法修改图像对比度

```python
imgplot = plt.imshow(lum_img,clim=(0.0,0.7))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/d3cf83c9688e336ab13dd9ce35dd1d44.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

如果在文章中发现问题或是对matplotlib有些许疑问欢迎在评论区中留言