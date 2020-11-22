---
title: Python-Matplotlib-深入学习
abbrlink: 41087
date: 2020-11-21 13:57:30
tags:
	- Python
	- Matplotlib
categories: Python
---

## 简介

&emsp; 这篇文章介绍了Matplotlib中的一些更复杂的类和函数。并且对于特定的自定义和复杂的可视化很有用

<!--more-->

<br>

---

<br>

## Artist教程

> 使用Artist对象在画布上渲染

> matplotlib API有三层。

- matplotlib.backend_bases.FigureCanvas是图形被绘制到的区域


- matplotlib.backend_bases.Renderer是知道如何在FigureCanvas上绘制的对象


- [matplotlib.artist.Artist](https://matplotlib.org/api/artist_api.html#matplotlib.artist.Artist)是知道如何使用渲染器在画布上作画的对象。

FigureCanvas和Renderer处理与用户界面工具包(如[wxPython](https://www.wxpython.org/))或绘图语言(如PostScript®)对话的所有细节，而Artist处理所有高层构造，如表示和布局图形、文本和线条。

<br>

​	> 有两种类型的Artist: primitives和containers。

​	primitives代表了我们想要在画布上绘制的标准图形对象:[`Line2D`](https://matplotlib.org/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D), [`Rectangle`](https://matplotlib.org/api/_as_gen/matplotlib.patches.Rectangle.html#matplotlib.patches.Rectangle), [`Text`](https://matplotlib.org/api/text_api.html#matplotlib.text.Text), [`AxesImage`](https://matplotlib.org/api/image_api.html#matplotlib.image.AxesImage)等;

​	containers是放置它们的地方 ([`Axis`](https://matplotlib.org/api/axis_api.html#matplotlib.axis.Axis), [`Axes`](https://matplotlib.org/api/axes_api.html#matplotlib.axes.Axes) and [`Figure`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure))。

<br>

​	标准用法是创建一个Figure实例，使用Figure创建一个或多个轴或子图实例，并使用Axes实例方法创建primitives。

> 在下面的示例中，我们使用[`matplotlib.pyplot.figure()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.figure.html#matplotlib.pyplot.figure)创建一个Figure实例.

```python
fig = plt.figure()
ax = fig.add_subplot(2,1,1)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/21/1c272f0ea6f2440708d470c7c08984bf.png" style="zoom:80%;margin-left:10px" />

> 如果要在任意位置创建Axes,只需使用[add_axes()](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.add_axes)方法
>
> 参数：[left,bottom,width,height]

```python
fig2 = plt.figure()
ax2 = fig2.add_axes([0,0,0.7,0.3])
ax3 = fig2.add_axes([1,1,0.7,0.3])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/21/d0ac5fad59709d82828ccc99530f100c.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

### 自定义对象

> 每个matplotlib的Artist对象具有以下属性

