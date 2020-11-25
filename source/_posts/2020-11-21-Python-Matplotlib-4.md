---
title: Python-Matplotlib-Artist教程
abbrlink: 41087
date: 2020-11-21 13:57:30
tags:
	- Python
	- Matplotlib
categories: Python
---

## Artist教程

> 使用Artist对象在画布上渲染

<!--more-->

> matplotlib API有三层。

- matplotlib.backend_bases.FigureCanvas是图形被绘制到的区域


- matplotlib.backend_bases.Renderer是知道如何在FigureCanvas上绘制的对象


- [matplotlib.artist.Artist](https://matplotlib.org/api/artist_api.html#matplotlib.artist.Artist)是知道如何使用渲染器在画布上作画的对象。

FigureCanvas和Renderer处理与用户界面工具包(如[wxPython](https://www.wxpython.org/))或绘图语言(如PostScript®)对话的所有细节，而Artist处理所有高层构造，如表示和布局图形、文本和线条。



<br>

> 引言

​	有两种类型的Artist: primitives和containers。

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

| 属性       | 描述                                              |
| ---------- | ------------------------------------------------- |
| alpha      | 透明度 - 范围0-1                                  |
| animated   | 用于促进动画绘制的布尔值                          |
| axes       | Artist对象存在的轴，可能没有                      |
| clip_box   | 剪辑Artist的边界框                                |
| clip_on    | 是否开启剪辑                                      |
| clip_path  | Artist被剪辑的路径                                |
| contains   | 一个选择函数，用于测试Artist是否包含选择的点      |
| figure     | Artist存在的figure示例，可能没有                  |
| label      | 文本标签（例如：用于自动标签）                    |
| picker     | 控制对象选择的python对象                          |
| transform  | 转换                                              |
| visible    | 是否应该绘制Artist的布尔值                        |
| zorder     | 决定绘图顺序的数字                                |
| rasterized | 布尔值;将向量转换为光栅图形 (用于压缩和eps透明度) |

**每个属性都可以通过老式的setter或getter访问。**

例如，将当前的alpha乘以一半：

```python
a = o.get_alpha()
o.set_alpha(0.5*a)
```

**如果要一次设置多个属性，则还可以将set方法与关键字参数一起使用**

例如：

```python
o.set(alpha=0.5,zorder=2)
```

如果你是在python shell上进行交互工作，**检查Artist属性的便捷方法是使用[`matplotlib.artist.getp()`](https://matplotlib.org/api/_as_gen/matplotlib.artist.getp.html#matplotlib.artist.getp)函数**

该函数列出了属性及其值。

这也适用于从Artist派生的类，例如Figure和Rectangle。

对于创建的figure对象，使用上述命令：

```python
#可以自己创建一个figure实例查看
matplotlib.artist.getp(fig.patch)
```

```python
#结果
agg_filter = None
    alpha = None
    animated = False
    antialiased or aa = False
    bbox = Bbox(x0=0.0, y0=0.0, x1=1.0, y1=1.0)
    capstyle = butt
    children = []
    clip_box = None
    clip_on = True
    clip_path = None
    contains = None
    data_transform = BboxTransformTo(     TransformedBbox(         Bbox...
    edgecolor or ec = (1.0, 1.0, 1.0, 0.0)
    extents = Bbox(x0=0.0, y0=0.0, x1=432.0, y1=288.0)
    facecolor or fc = (1.0, 1.0, 1.0, 0.0)
    figure = Figure(432x288)
    fill = True
    gid = None
    hatch = None
    height = 1
    in_layout = False
    joinstyle = miter
    label = 
    linestyle or ls = solid
    linewidth or lw = 0.0
    patch_transform = CompositeGenericTransform(     BboxTransformTo(   ...
    path = Path(array([[0., 0.],        [1., 0.],        [1.,...
    path_effects = []
    picker = None
    rasterized = None
    sketch_params = None
    snap = None
    transform = CompositeGenericTransform(     CompositeGenericTra...
    transformed_clip_path_and_affine = (None, None)
    url = None
    verts = [[  0.   0.]  [432.   0.]  [432. 288.]  [  0. 288....
    visible = True
    width = 1
    window_extent = Bbox(x0=0.0, y0=0.0, x1=432.0, y1=288.0)
    x = 0
    xy = (0, 0)
    y = 0
    zorder = 1
```

**更多关于给定对象的属性列表可查看 [matplotlib.artist](https://matplotlib.org/api/artist_api.html#artist-api)**



### 对象容器

&emsp;既然我们知道了如何检查和设置要配置的给定对象的属性，那么我们需要知道如何获取该对象。

&emsp;在本节中，我们将回顾各种容器对象存储您想要获取的Artist的位置。

---

#### Figure容器

顶层容器Artist是[`matplotlib.figure.Figure`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure),它包含图中的所有内容。图形的背景是一个矩形，存储在figure .patch中。



当你在途中添加子图（[`add_subplot()`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.add_subplot)）和轴（[`add_axes()`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.add_axes)）时，它们将被附加到[`Figure.axes`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.axes)，这些也有创建它们的方法返回

> 举个栗子

```python
fig = plt.figure()

ax1 = fig.add_subplot(211)  #添加一个子图
ax2 = fig.add_axes([0.1,0.1,0.7,0.3])#添加一个新轴，参数分别是[left,bottom,width,height]

ax1

```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/22/6301a5c1d03690a06069cab845adcebe.png" style="zoom:80%;margin-left:10px" />

```python
print(fig.axes)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/22/845809658b4ccf59f69abc810e486494.png" style="zoom:80%;margin-left:10px" />

由于该图保留了“当前轴”（请参见[`Figure.gca`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.gca)和 [`Figure.sca`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.sca)）的概念 以支持pylab / pyplot状态机，66因此您不应直接从轴列表中插入或删除轴，而应使用 [`add_subplot()`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.add_subplot)和 [`add_axes()`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.add_axes)方法插入，以及 [`delaxes()`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.delaxes)方法删除。但是，您可以自由地遍历轴列表或对其进行索引以访问`Axes`要自定义的实例。

这是一个打开所有轴网格的示例：

```python
for ax in fig.axes:
    ax.grid(True)
```

图形还有自己的文本、线条、形状和图像，您可以使用它们直接添加primitives。图形的默认坐标系统将简单地以像素为单位(这通常不是你想要的)，但是你可以通过设置你添加到图形中的Artist的transform属性来控制它。

更有用的是“图形坐标”，其中（0，0）是图形的左下角，而（1，1）是图形的右上角，可以通过将`Artist`变换设置为来获得`fig.transFigure`：

```python
import matplotlib.lines as lines

fig = plt.figure()

l1 = lines.Line2D([0, 1], [0, 1], transform=fig.transFigure, figure=fig)
l2 = lines.Line2D([0, 1], [1, 0], transform=fig.transFigure, figure=fig)
fig.lines.extend([l1, l2])

plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/22/6c744e039bd0c8a201ff28664b0440dc.png" style="zoom:80%;margin-left:10px" />

下面是该图包含的Artist的摘要

| 图形属性 | 描述                                    |
| -------- | --------------------------------------- |
| axes     | 轴的实例 (包括子图)                     |
| patch    | 矩形背景                                |
| images   | 图形图像形状列表-有用的原始像素显示     |
| legends  | 图像图例（和Axes.legends不同）          |
| lines    | 图像Line2D实例(很少使用，看Axes.lines） |
| patches  | 图像的形状（很少使用，看 Axes.patches)  |
| texts    | 图像文本                                |

---

#### Axes容器

&emsp;matplotlib.axes.Axes是matplotlib的中心——它包含图形中使用的绝大多数美工，以及用于创建和添加这些美工到自身的许多辅助方法，以及用于访问和定制其中包含的美工的辅助方法。

&emsp;和图一样，它包含了一个 [`Patch`](https://matplotlib.org/api/_as_gen/matplotlib.patches.Patch.html#matplotlib.patches.Patch)，在笛卡尔坐标系中是一个矩形，在极坐标中是一个圆;这个patch决定了作图区域的形状、背景和边界:

```python
ax = fig.add_subplot(111)
rect = ax.patch  # 一个矩形实例
rect.set_facecolor('green')   #设置背景颜色为绿色
```

当你调用绘图方法，例如规范化 [`plot()`](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.plot.html#matplotlib.axes.Axes.plot)并且传入数组或列表的值为参数时，该方法将创建一个[`matplotlib.lines.Line2D()`](https://matplotlib.org/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D)实例，使用作为关键字参数传递的所有Line2D属性更新该line，并将该line添加到Axes.lines容器，并返回给您:

```python
x,y = np.random.rand(2,100)
line,=ax.plot(x,y,'-',color='blue',linewidth=2)
```

plot返回的是一个lines列表，因为你可以传入多个x,y来绘制。

例如:

```python
print(ax.lines)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/23/0fbc0abe28431d8b944b25ee0dd0492e.png" style="zoom:80%;margin-left:10px" />

同样，创建patches的方法，像[`bar()`](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.bar.html#matplotlib.axes.Axes.bar)创建了矩阵列表，会添加patches到Axes.patches列表中

```python
fig = plt.figure()
ax = fig.add_subplot(111)
n,bins,rectangles = ax.hist(np.random.randn(1000),50)
print(rectangles)
print(len(ax.patches))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/23/7906d217c1f3663dee47e110d9727534.png" style="zoom:80%;margin-left:10px" />

有很多axis辅助方法用于创建primitive Artists并将它们添加到各自的容器中。

> 下面的表格总结了他们的一个小样例，他们创造的Artist类型，以及把他们储存在哪里

| Helper method                  | Artist                           | Container               |
| ------------------------------ | -------------------------------- | ----------------------- |
| ax.annotate - text annotations | Annotate(注释)                   | ax.texts                |
| ax.bar - bar charts            | Rectangle                        | ax.patches              |
| ax.errorbar - error bar plots  | Line2D and Rectangle             | ax.lines and ax.patches |
| ax.fill - shared area          | Polygon(多边形)                  | ax.patches              |
| ax.hist - histograms           | Rectangle                        | ax.patches              |
| ax.imshow - image data         | AxesImage                        | ax.images               |
| ax.legend - axes legends       | Legend(图例)                     | ax.legends              |
| ax.plot - xy plots             | Line2D                           | ax.lines                |
| ax.scatter - scatter charts    | PolygonCollection （多边形集合） | ax.collections          |
| ax.text - text                 | Text                             | ax.texts                |

<br>

> 下面这个是Axes容器的Artist对象的概括：

| Axes attribute | Description                |
| -------------- | -------------------------- |
| artists        | Artist 实例的列表          |
| patch          | Axes的背景的矩阵实例的列表 |
| collections    | 集合实例的列表             |
| images         | 轴图像的列表               |
| legends        | 图例实例的列表             |
| lines          | Line2D实例的列表           |
| patches        | Patch实例列表              |
| texts          | 文本实例列表               |
| xaxis          | matplotlib.axis.XAxis实例  |
| yaxis          | matplotlib.axis.YAxis实例  |

---

#### Axis容器

[`matplotlib.axis.Axis`](https://matplotlib.org/api/axis_api.html#matplotlib.axis.Axis)实例处理刻度线、网格线、刻度标签和axis标签的绘制。

每个Axis对象包含一个label属性(这是pyplot在调用xlabel和ylabel时修改的内容)以及一个主刻度和次要刻度列表。这些刻度是[`axis.XTick`](https://matplotlib.org/api/axis_api.html#matplotlib.axis.XTick)和[`axis.YTick`](https://matplotlib.org/api/axis_api.html#matplotlib.axis.YTick)的实例，其中包含呈现刻度和刻度标签的actual line和文本primitives。

​	因为刻度是根据需要动态创建的(例如，在移动和缩放时)，所以应该通过它们的accessor方法[`axis.Axis.get_major_ticks`](https://matplotlib.org/api/_as_gen/matplotlib.axis.Axis.get_major_ticks.html#matplotlib.axis.Axis.get_major_ticks) and [`axis.Axis.get_minor_ticks`](https://matplotlib.org/api/_as_gen/matplotlib.axis.Axis.get_minor_ticks.html#matplotlib.axis.Axis.get_minor_ticks)访问主要刻度和次要刻度的列表。尽管刻度包含了所有的primitives，并且将在下面覆盖，Axis实例有accessor方法返回刻度行，刻度标签，刻度位置等:

```python
fig,ax = plt.subplots()
axis = ax.xaxis
axis.get_ticklocs()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/23/7803d9942ea0d9e48e135acbf07bf329.png" style="zoom:80%;margin-left:10px" />

```python
axis.get_ticklabels()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/23/6ac56f788e584febaf1cf95e323a9df8.png" style="zoom:80%;margin-left:10px" />

请注意，刻度线是标签的两倍，因为默认情况下，顶部和底部有刻度线，但x轴下方仅是刻度线；但是，可以自定义。

```python
axis.get_ticklines()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/23/f6a8d7ad3ab96cd87247561467f3ac1e.png" style="zoom:80%;margin-left:10px" />

以下是的一些有用的`Axis`的accessor方法的摘要 （这些访问器有相应的setters，例如 [`set_major_formatter()`](https://matplotlib.org/api/_as_gen/matplotlib.axis.Axis.set_major_formatter.html#matplotlib.axis.Axis.set_major_formatter)）

| Accessor 方法       | 描述                                                         |
| ------------------- | ------------------------------------------------------------ |
| get_scale           | axis的比例：如“对数”或“线性”                                 |
| get_view_interval   | The interval instance of the axis view limits                |
| get_data_interval   | The interval instance of the axis data limits                |
| get_gridlines       | 用于轴的网格线列表                                           |
| get_label           | 轴的标签 -文本实例                                           |
| get_ticklabels      | 一个文本实例列表-keyword minor=True\|False                   |
| get_ticklines       | Line2D实例列表- keyword minor=True\|False                    |
| get_ticklocs        | 刻度位置- keyword minor=True\|False                          |
| get_major_locator   | 主要刻度的 [`ticker.Locator`](https://matplotlib.org/api/ticker_api.html#matplotlib.ticker.Locator) 实例 |
| get_major_formatter | 主要刻度的 [`ticker.Formatter`](https://matplotlib.org/api/ticker_api.html#matplotlib.ticker.Formatter)实例 |
| get_minor_locator   | 次要刻度的 [`ticker.Locator`](https://matplotlib.org/api/ticker_api.html#matplotlib.ticker.Locator) 实例 |
| get_minor_formatter | 次要刻度的[`ticker.Formatter`](https://matplotlib.org/api/ticker_api.html#matplotlib.ticker.Formatter)实例 |
| get_major_ticks     | 主要刻度的实例列表                                           |
| get_minor_ticks     | 次要刻度的实例列表                                           |
| grid                | 为主要刻度或次要刻度打开或关闭网格                           |

> 举个栗子

可以自定义轴和刻度属性

```python
fig = plt.figure()
rect = fig.patch   #矩形实例
rect.set_facecolor('lightgoldenrodyellow')

ax1 = fig.add_axes([0.1,0.3,0.4,0.4])
rect = ax1.patch
rect.set_facecolor('lightslategray')

for label in ax1.xaxis.get_ticklabels():
	#label是一个文本实例
    label.set_color('red')
    label.set_rotation(45)
    label.set_fontsize(16)
    
for line in ax1.yaxis.get_ticklines():
	#line是一个Line2D实例
    line.set_color('green')
    line.set_markersize(25)
    line.set_markeredgewidth(3)

plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/23/1ab9b44582b36347143958a8f37dd3e4.png" style="zoom:80%;margin-left:10px" />

#### Tick容器

[`matplotlib.axis.Tick`](https://matplotlib.org/api/axis_api.html#matplotlib.axis.Tick) 是从[`Figure`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure) 到 [`Axes`](https://matplotlib.org/api/axes_api.html#matplotlib.axes.Axes) 再到 [`Axis`](https://matplotlib.org/api/axis_api.html#matplotlib.axis.Axis) 最后到 [`Tick`](https://matplotlib.org/api/axis_api.html#matplotlib.axis.Tick) 的容器对象。

Tick包含了刻度和网格线，以及上下刻度的标签实例。

这些中的每一个都可以作为Tick的属性直接访问

| Tick属性  | 描述        |
| --------- | ----------- |
| tick1line | Line2D 实例 |
| tick2line | Line2D 实例 |
| gridline  | Line2D 实例 |
| label1    | 文本实例    |
| label2    | 文本实例    |

> 举个栗子

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker

np.random.seed(19680801)

fig, ax = plt.subplots()
ax.plot(100*np.random.rand(20))


ax.yaxis.set_major_formatter(ticker.FormatStrFormatter('%0.2f'))

ax.yaxis.set_tick_params(which='major', labelcolor='green',
                         labelleft=False, labelright=True)

plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/23/89cdbacf05816030f8066139b9f4b274.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

如果你发现文章中出现的错误或者有任何疑问欢迎在下方评论区评论

