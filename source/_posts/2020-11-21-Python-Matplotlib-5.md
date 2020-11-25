---
title: Python-Matplotlib-图例指南
tags:
  - Python
  - Matplotlib
categories: Python
abbrlink: 15990
date: 2020-11-25 16:48:45
---

## 图例指南

&emsp;在Matplotlib中灵活地生成图例

&emsp;在阅读这一章节前请熟悉关于 [`legend()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend)的讲解

<!--more-->

> 一些常用用语：

- **图例条目**

图例由一个或多个图例条目组成。一项仅由一个键和一个标签组成。

- **图例键**

每个图例标签左侧的彩色/图案标记。

- **图例标签**

描述键所代表的文本。

- **图例句柄**

用于在图例中生成适当条目的原始对象。

（也不知道这样子翻译的对不对，先放一下英文版，等明白了再回来改）

- legend entry

  A legend is made up of one or more legend entries. An entry is made up of exactly one key and one label.

- legend key

  The colored/patterned marker to the left of each legend label.

- legend label

  The text which describes the handle represented by the key.

- legend handle

  The original object which is used to generate an appropriate entry in the legend.

---

### 控制图例条目

调用无参的[`legend()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend)会自动获取图例handles和它们的关联标签

这个功能等效于：

```python
#等效于ax.legend()
handles, labels = ax.get_legend_handles_labels()
ax.legend(handles, labels)
```

该[`get_legend_handles_labels()`](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.get_legend_handles_labels.html#matplotlib.axes.Axes.get_legend_handles_labels)函数返回存在于轴上的handles或artists，可用于生成结果图例的条目——（要注意的是，并非所有的Artist都可以添加到图例中，这种情况下“proxy（代理）”就需要创建）

带有空字符串作为标签或标签以“ _”开头的artists将被忽略。

要完全控制添加到图例中的内容，通常可以将适当的handles直接传递给[`legend()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend):

```python
line_up, = plt.plot([1,2,3],label='Line 2')
line_down, = plt.plot([3,2,1],label='Line 1')
plt.legend(handles=[line_up,line_down])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/e39feee687989169c388c49c688e344b.png" style="zoom:80%;margin-left:10px" />

在某些情况下，无法设置handles的标签，因此可以将标签列表传递给[`legend()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend):

```python
line_up, = plt.plot([1,2,3],label='Line 2')
line_down, = plt.plot([3,2,1],label='Line 1')
plt.legend([line_up,line_down],['Line Up','Line Down'])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/103fee29e96cd5aa9e3627150d5503c0.png" style="zoom:80%;margin-left:10px" />

---

### 创建专门用于添加图例的Artist(又名代理艺术家)

并不是所有的handles都能自动转换为图例条目，所以总是有必要创建一个artist。图例handles不必存在于图形或轴上才能使用。

```python
import matplotlib.patches as mpatches

red_patch = mpatches.Patch(color='red',label='The red data')
plt.legend(handles=[red_patch])
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/c5ac844fe89a9cd085597448e109685e.png" style="zoom:80%;margin-left:10px" />

有许多受支持的图例handles。除了创建颜色patch之外，我们还可以创建带有标记的线：

```python
import matplotlib.lines as mlines

blue_line = mlines.Line2D([],[],color='blue',marker='*',markersize=15,label='Blue Star')
plt.legend(handles=[blue_line])
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/9ac2fbb7519ce88a7bfcd4ead0e9e02a.png" style="zoom:80%;margin-left:10px" />

---

### 图例位置

图例的位置可以通过关键字**loc**来指定。请在官方文档[`legend()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend)查看更多细节 

bbox_to_anchor关键字为手动图例的位置提供了很大程度的控制。

例如，如果你想让坐标轴图例位于图形的右上角而不是坐标轴的角落，只需指定角落的位置和该位置的坐标系统:

```python
plt.plot([1,2,3],[3,2,1],label='Line')
#plt.gcf().transFigure获取当前figure
plt.legend(bbox_to_anchor=(1, 1),
           bbox_transform=plt.gcf().transFigure)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/35c5d4cbbbc48b25091c67bf521e5f47.png" style="zoom:80%;margin-left:10px" />

更多自定义图例放置的例子:

```python
plt.subplot(211)
plt.plot([1,2,3],label="Line 1")
plt.plot([3,2,1],label="Line 2")
plt.legend(bbox_to_anchor=(0.,1.02,1.,.102),loc='lower left',ncol=2,mode="expand",borderaxespad=0.)

plt.subplot(223)
plt.plot([1,2,3],label="Line 1")
plt.plot([3,2,1],label="Line 2")
plt.legend(bbox_to_anchor=(1.05,1),loc='upper left',borderaxespad=0.)

plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/078bbd773ea2b5b201452c9aecb9cc7b.png" style="zoom:80%;margin-left:10px" />

---

### 同一个Axes下多个图例

手动将图例添加到当前Axes下：

```python
line1, = plt.plot([1,2,3],label="Line 1",linestyle='--')
line2, = plt.plot([3,2,1],label="Line 2",linewidth=5)
#为第一条线创建图例
first_legend = plt.legend(handles=[line1],loc='upper right')
#将first_legend手动地添加到当前Axes
ax = plt.gca().add_artist(first_legend)
#为第二条线创建图例
plt.legend(handles=[line2],loc='lower right')

plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/cd0973359c7db5967e599c14527ace09.png" style="zoom:80%;margin-left:10px" />

---

### 图例Handlers

为了创建图例条目，handles被作为参数提供给适当的HandlerBase子类。

使用自定义Handlers的最简单示例是实例化一个现有的[`legend_handler.HandlerBase`](https://matplotlib.org/api/legend_handler_api.html#matplotlib.legend_handler.HandlerBase)的子类。

为了简单起见，我们选择[`legend_handler.HandlerLine2D`](https://matplotlib.org/api/legend_handler_api.html#matplotlib.legend_handler.HandlerLine2D)，它接受numpoints参数（numpoints也是legend()函数上的一个关键字）。

然后，我们可以将实例到Handler的映射作为关键字传递给legend。

```python
from matplotlib.legend_handler import HandlerLine2D

line1, = plt.plot([3,2,1],marker='o',label='Line 1')
line2, = plt.plot([1,2,3],marker='o',label='Line 2')

plt.legend(handler_map={line1: HandlerLine2D(numpoints=3)})
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/90539974421a6fca5a2dc65692585ef8.png" style="zoom:80%;margin-left:10px" />

除了用于errorbar、stem plot和histograms等复杂图形类型的Handlers外,默认的handler_map还有一个特殊的元组handler([`legend_handler.HandlerTuple`](https://matplotlib.org/api/legend_handler_api.html#matplotlib.legend_handler.HandlerTuple)),它简单地为给定元组中的每个项绘制一个又一个的handles。

下面的例子演示了将两个图例键组合在一起:

```python
from numpy.random import randn

z = randn(10)

red_dot, = plt.plot(z, "ro", markersize=15)
# 白色十字图案放在前五个数据上显示
white_cross, = plt.plot(z[:5], "w+", markeredgewidth=3, markersize=15)

plt.legend([red_dot, (red_dot, white_cross)], ["Attr A", "Attr A+B"])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/2be1df404bf519ee9d238e605d88a29e.png" style="zoom:80%;margin-left:10px" />

[`legend_handler.HandlerTuple`](https://matplotlib.org/api/legend_handler_api.html#matplotlib.legend_handler.HandlerTuple) 类也可以用来为同一个条目分配几个图例键:

```python
from matplotlib.legend_handler import HandlerLine2D, HandlerTuple

p1, = plt.plot([1, 2.5, 3], 'r-d')
p2, = plt.plot([3, 2, 1], 'k-o')

l = plt.legend([(p1, p2)], ['Two keys'], numpoints=1,
               handler_map={tuple: HandlerTuple(ndivide=None)})
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/b040655da0667b35b05ba9e485cd997a.png" style="zoom:80%;margin-left:10px" />

---

### 实现自定义的图例handler

可以实现自定义handler来将任何handle转换为图例键(handles不一定需要是matplotlib artists对象)。

handler必须实现一个legend_artist方法，该方法为图例返回一个artist对象来使用。

legend_artist所需的签名，记录在[`legend_artist`](https://matplotlib.org/api/legend_handler_api.html#matplotlib.legend_handler.HandlerBase.legend_artist)中。

```python
import matplotlib.patches as mpatches


class AnyObject:
    pass


class AnyObjectHandler:
    def legend_artist(self, legend, orig_handle, fontsize, handlebox):
        x0, y0 = handlebox.xdescent, handlebox.ydescent
        width, height = handlebox.width, handlebox.height
        patch = mpatches.Rectangle([x0, y0], width, height, facecolor='red',
                                   edgecolor='black', hatch='xx', lw=3,
                                   transform=handlebox.get_transform())
        handlebox.add_artist(patch)
        return patch


plt.legend([AnyObject()], ['My first handler'],
           handler_map={AnyObject: AnyObjectHandler()})
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/603d9465d641ab9fbc054b2be2210135.png" style="zoom:80%;margin-left:10px" />

或者，如果我们想要全局地接受AnyObject实例，而不需要一直手动设置handler_map关键字，我们可以用:

```python
from matplotlib.legend import Legend
Legend.update_default_handler_map({AnyObject: AnyObjectHandler()})
```

虽然这里的功能很明显，但请记住，已经实现了许多handlers，并且您想要实现的可能已经很容易地通过现有的类实现了。

例如，产生椭圆的图例键，而不是矩形的:

```python
from matplotlib.legend_handler import HandlerPatch


class HandlerEllipse(HandlerPatch):
    def create_artists(self, legend, orig_handle,
                       xdescent, ydescent, width, height, fontsize, trans):
        center = 0.5 * width - 0.5 * xdescent, 0.5 * height - 0.5 * ydescent
        p = mpatches.Ellipse(xy=center, width=width + xdescent,
                             height=height + ydescent)
        self.update_prop(p, orig_handle, legend)
        p.set_transform(trans)
        return [p]


c = mpatches.Circle((0.5, 0.5), 0.25, facecolor="green",
                    edgecolor="red", linewidth=3)
plt.gca().add_patch(c)

plt.legend([c], ["An ellipse, not a rectangle"],
           handler_map={mpatches.Circle: HandlerEllipse()})
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/24/0068644f6e1423bf18d9aa56a5a08ae5.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

如果你发现文章中出现的错误或者有任何疑问欢迎在下方评论区评论